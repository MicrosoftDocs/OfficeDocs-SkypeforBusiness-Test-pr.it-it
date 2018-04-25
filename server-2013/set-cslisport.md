---
title: Set-CsLisPort
TOCTitle: Set-CsLisPort
ms:assetid: 8a8a8f95-9366-4d87-bf2a-9767e5eb9996
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398700(v=OCS.15)
ms:contentKeyID: 49301255
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsLisPort

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una porta del server Informazioni percorso, crea un'associazione tra una porta e una posizione (creando una nuova posizione se questa non esiste) o modifica una porta esistente e la relativa posizione associata. L'associazione tra porta e posizione viene utilizzata in un'implementazione di VoIP aziendale con il servizio di chiamate di emergenza Enhanced 9-1-1 (E9-1-1) per segnalare la posizione del chiamante all'operatore del servizio di emergenza. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsLisPort -ChassisID <String> -PortID <String> [-City <String>] [-CompanyName <String>] [-Country <String>] [-Description <String>] [-HouseNumber <String>] [-HouseNumberSuffix <String>] [-Location <String>] [-PortIDSubType <InterfaceAlias | InterfaceName | LocallyAssigned>] [-PostalCode <String>] [-PostDirectional <String>] [-PreDirectional <String>] [-State <String>] [-StreetName <String>] [-StreetSuffix <String>] <COMMON PARAMETERS>

    Set-CsLisPort -ChassisID <String> -PortID <String> [-Description <String>] [-PortIDSubType <InterfaceAlias | InterfaceName | LocallyAssigned>] <COMMON PARAMETERS>

    Set-CsLisPort -City <String> -CompanyName <String> -Country <String> -HouseNumber <String> -HouseNumberSuffix <String> -Location <String> -PostalCode <String> -PostDirectional <String> -PreDirectional <String> -State <String> -StreetName <String> -StreetSuffix <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'Esempio 1 viene creata o aggiornata una voce località della porta LIS. Il comando in questo esempio include tre parametri: ChassisID, PortID e PortIDSubtype. Il valore per ChassisID è l'indirizzo MAC 99-99-99-99-99-99, il valore per PortID è 4200 e il valore per PortIDSubType è 1. Si noti che il valore 1 per PortIDSubType viene convertito in un valore per InterfaceAlias. È possibile che questo parametro e questo valore siano stati immessi nel modo seguente: -PortIDSubType InterfaceAlias. Questi tre parametri sono obbligatori per creare un'istanza univoca della località per la porta.

Si noti che in questo esempio non è inclusa alcuna informazione sull'indirizzo. È possibile creare una voce per la porta su Location Information Server senza associarla ad un indirizzo. Tuttavia, le chiamate di emergenza instradate attraverso questa porta potrebbero non contenere (a seconda delle località per lo switch o la subnet specificate) informazioni sufficienti all'operatore del servizio di emergenza per identificare una località.

IMPORTANTE: Se esiste già una località per la porta LIS con questa combinazione, questa verrà sostituita con i valori contenuti in questo comando. Ciò significa che se questa porta era associata ad un indirizzo (una località fisica), questa associazione non esisterà più perché non sono state incluse le informazioni di località in questo comando. La località esisterà ancora nel database delle località, ma non sarà associata a questa porta.

    Set-CsLisPort -ChassisID 99-99-99-99-99-99 -PortID 4200 -PortIDSubType 1

## ESEMPIO 2

Nell'Esempio 2 viene aggiornata la porta creata nell'Esempio 1 aggiungendo le informazioni sull'indirizzo. Se l'indirizzo non esiste nel database delle località, questo cmdlet creerà quella località.

    Set-CsLisPort -ChassisID 99-99-99-99-99-99 -PortID 4200 -PortIdSubType 1 -Location "30/1000" -HouseNumber 1234 -PreDirectional NE -StreetName First -StreetSuffix Avenue -City Redmond -State WA -Country US -PostalCode 99999

## ESEMPIO 3

In questo esempio vengono aggiornate tutte le località definite per le porte con un indirizzo MAC (ChassisID) 99-99-99-99-99-88. Nella prima riga di questo esempio viene chiamato il cmdlet **Get-CsLisPort**, che recupera tutte le porte definite nel servizio LIS. La raccolta di porte viene quindi inviata tramite pipe al cmdlet **Where-Object**, che trova tutti gli elementi nella raccolta con ChassisID uguale a (-eq) 99-99-99-99-99-88. Tale raccolta con ChassisID 99-99-99-99-99-88 viene assegnata alla variabile $a.

A questo punto, il contenuto della variabile $a (la raccolta di porte LIS con ChassisID 99-99-99-99-99-88) viene inviato tramite pipe al cmdlet **Set-CsLisPort**. Questo cmdlet prenderà ogni elemento nella raccolta e lo aggiornerà con i valori nei parametri specificati (Location, HouseNumber, StreetName, StreetSuffix, City, State, Country e PostalCode).

    $a = Get-CsLisPort | Where-Object {$_.ChassisID -eq "99-99-99-99-99-88"}
    $a | Set-CsLisPort -Location "30/1000" -HouseNumber 1234 -StreetName First -StreetSuffix Avenue -City Redmond -State WA -Country US -PostalCode 99999

## Descrizione dettagliata

Enhanced 9-1-1 consente all'operatore del servizio di emergenza di identificare la località di un chiamante senza dover richiedere questa informazione al chiamante. Nel caso in cui una persona stia chiamando tramite una connessione VoIP (Voice over Internet Protocol), queste informazioni possono essere dedotte da diversi elementi della connessione. L'amministratore della connessione VoIP deve configurare una mappa delle località (chiamata wiremap) che consente di determinare la località di un chiamante. Questo cmdlet consente all'amministratore di mappare località fisiche alla porta attraverso cui si connette il client.

La combinazione di ChassisID, PortID e PortIDSubType crea una località della porta univoca. Se si immette una combinazione ChassisID/PortID/PortIDSubType che già esiste, questo cmdlet aggiornerà la località per quella porta basandosi sui parametri di località forniti. Se la combinazione non esiste, verrà creata una nuova località per la porta.

Se una località con un indirizzo esattamente corrispondente ai parametri di indirizzo immessi ora (compresi i valori null) non esiste nel database delle località, verrà creata una nuova località basata sui parametri immessi con questo cmdlet. È possibile ottenere un elenco di località utilizzando il cmdlet **Get-CsLisLocation**. Il cmdlet **Set-CsLisPort** non necessita e non chiede l'immissione di un parametro di località; è possibile creare una voce per la porta senza associarla ad una località. Con questo cmdlet è anche possibile creare una località non valida. Una località valida comprende, come minimo, i valori relativi a Location, HouseNumber, StreetName, City, State e Country. Se tutti questi parametri non vengono specificati, le chiamate ricevute dalla porta potrebbero non contenere le informazioni richieste dall'operatore del servizio di emergenza (a seconda che siano disponibili o meno le impostazioni valide per uno switch, una subnet o un punto di accesso wireless che possono essere utilizzate al posto delle impostazioni della porta). Si raccomanda di essere il più specifici possibile con i parametri di località e di compilarne quanti più possibile.

Uno dei parametri obbligatori del cmdlet è ChassisID. ChassisID è l'indirizzo MAC dello switch di rete della porta. Se questo switch non esiste nel database delle località, questo cmdlet lo creerà. È possibile recuperare switch esistenti utilizzando il cmdlet **Get-CsLisSwitch**. Tenere presente che anche se verrà creata una nuova voce di switch, tale switch non verrà associato automaticamente alle informazioni sulla località immesse utilizzando il cmdlet **Set-CsLisPort** è necessario impostare la località con il cmdlet **Set-CsLisSwitch**.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsLisPort** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsLisPort"}

## Parametri


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Obbligatorio</th>
<th>Tipo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ChassisID</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>L'indirizzo MAC dello switch della porta. Questo valore deve essere nel formato nn-nn-nn-nn-nn-nn, ad esempio 12-34-56-78-90-ab, o come un indirizzo IP. Se la combinazione di ChassisID, PortID e PortIDSubType è univoca, verrà creata una nuova località per la porta. Se questa combinazione non è univoca, la località per la porta con tale combinazione verrà aggiornata con i valori del parametro forniti con il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>PortID</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>L'ID della porta associato alla località.</p></td>
</tr>
<tr class="odd">
<td><p><em>City</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>La città della località per questa porta.</p>
<p>Lunghezza massima: 64 caratteri.</p></td>
</tr>
<tr class="even">
<td><p><em>CompanyName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome della società in questa località.</p>
<p>Lunghezza massima: 60 caratteri</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Country</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>La nazione/regione in cui si trova la porta.</p>
<p>Lunghezza massima: 2 caratteri</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Una descrizione dettagliata della località della porta.</p></td>
</tr>
<tr class="even">
<td><p><em>HouseNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il numero civico della località per la porta. Il valore indica il numero civico in cui si trova la società.</p>
<p>Lunghezza massima: 10 caratteri</p></td>
</tr>
<tr class="odd">
<td><p><em>HouseNumberSuffix</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Informazioni aggiuntive sul numero civico, quali 1/2 o A. Ad esempio, 1234 1/2 Oak Street o 1234 A Elm Street.</p>
<p>Si noti che per designare un numero di appartamento o di ufficio, si deve utilizzare il parametro Location. Ad esempio, -Location &quot;Suite 100/Office 150&quot;.</p>
<p>Lunghezza massima: 5 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>Location</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome della località. Normalmente questo valore è il nome di una località più specifico dell'indirizzo stradale, quale un numero di ufficio, ma può essere qualunque valore di stringa.</p>
<p>Lunghezza massima: 20 caratteri</p></td>
</tr>
<tr class="odd">
<td><p><em>PortIDSubType</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Lis.PortIDSubType</p></td>
<td><p>Il sottotipo della porta. Questo valore può essere immesso come valore numerico o come stringa, ma è necessario che sia un sottotipo valido. I sottotipi validi sono:</p>
<p>1: InterfaceAlias</p>
<p>5: InterfaceName</p>
<p>7: LocallyAssigned</p>
<p>Valore predefinito: 7 (LocallyAssigned)</p></td>
</tr>
<tr class="even">
<td><p><em>PostalCode</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il CAP associato alla località.</p>
<p>Lunghezza massima: 10 caratteri</p></td>
</tr>
<tr class="odd">
<td><p><em>PostDirectional</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>L'indicazione direzionale del nome della via. Ad esempio, NE o NW per Main Street NE o 7th Avenue NW.</p>
<p>Lunghezza massima: 2 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>PreDirectional</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>L'indicazione direzionale del nome che precede il nome della via. Ad esempio, NE o NW per NE Main Street o NW 7th Avenue.</p>
<p>Lunghezza massima: 2 caratteri</p></td>
</tr>
<tr class="odd">
<td><p><em>State</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Lo stato o la provincia associata alla località.</p>
<p>Lunghezza massima: 2 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>StreetName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome della via della località.</p>
<p>Lunghezza massima: 60 caratteri</p></td>
</tr>
<tr class="odd">
<td><p><em>StreetSuffix</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il tipo di via indicato nel nome, ad esempio, Via, Viale o Corso.</p>
<p>Lunghezza massima: 10 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Accetta input tramite pipeline da oggetti porta LIS.

## Tipi restituiti

Questo cmdlet consente di creare o modificare un oggetto di tipo System.Management.Automation.PSCustomObject.

## Vedere anche

#### Ulteriori risorse

[Remove-CsLisPort](remove-cslisport.md)  
[Get-CsLisPort](get-cslisport.md)  
[Get-CsLisLocation](get-cslislocation.md)  
[Get-CsLisSwitch](get-cslisswitch.md)

