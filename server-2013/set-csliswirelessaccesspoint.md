---
title: Set-CsLisWirelessAccessPoint
TOCTitle: Set-CsLisWirelessAccessPoint
ms:assetid: 9c491f8d-c4c0-48e5-afc2-0153864dab41
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412723(v=OCS.15)
ms:contentKeyID: 49301449
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsLisWirelessAccessPoint

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un punto di accesso wireless (WAP) per il server Informazioni percorso, crea un'associazione tra un punto WAP e una posizione (creando una nuova posizione, se questa non esiste) oppure modifica un punto WAP esistente e la posizione a esso associata. L'associazione tra WAP e posizione viene utilizzata in un'implementazione di VoIP aziendale con il servizio di chiamate di emergenza Enhanced 9-1-1 (E9-1-1) per segnalare la posizione del chiamante all'operatore del servizio di emergenza. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsLisWirelessAccessPoint -BSSID <String> [-City <String>] [-CompanyName <String>] [-Country <String>] [-Description <String>] [-HouseNumber <String>] [-HouseNumberSuffix <String>] [-Location <String>] [-PostalCode <String>] [-PostDirectional <String>] [-PreDirectional <String>] [-State <String>] [-StreetName <String>] [-StreetSuffix <String>] <COMMON PARAMETERS>

    Set-CsLisWirelessAccessPoint -BSSID <String> [-Description <String>] <COMMON PARAMETERS>

    Set-CsLisWirelessAccessPoint -City <String> -CompanyName <String> -Country <String> -HouseNumber <String> -HouseNumberSuffix <String> -Location <String> -PostalCode <String> -PostDirectional <String> -PreDirectional <String> -State <String> -StreetName <String> -StreetSuffix <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

L'Esempio 1 crea o aggiorna una voce località LIS WAP. Il comando in questo esempio include un solo parametro (obbligatorio): BSSID. Il valore di BSSID è l'identificatore del WAP ( nel formato MAC address), in questo caso 99-99-99-99-99-99.

Si noti che in questo esempio non è inclusa alcuna informazione sull'indirizzo. È possibile creare una voce WAP sul Location Information Server senza associarle nessun indirizzo. Tuttavia, le chiamate di emergenza instradate attraverso questo WAP potrebbero non contenere informazioni sufficienti all'operatore del servizio di emergenza per identificare una località.

IMPORTANTE: Se esiste già una località LIS WAP con questo BSSID, questa verrà sostituita con i valori contenuti in questo comando. Ciò significa che se questo WAP era associato ad un indirizzo (una località fisica), questa associazione non esisterà più perché non sono state incluse le informazioni di località in questo comando. La località esisterà ancora nel database delle località, ma non sarà associata a questo WAP.

    Set-CsLisWirelessAccessPoint -BSSID 99-99-99-99-99-99

## ESEMPIO 2

L'Esempio 2 aggiorna il WAP creato nell'Esempio 1 aggiungendo le informazioni dell'indirizzo. In realtà si elimina la voce esistente e la si sostituisce con questa nuova voce. Se l'indirizzo non esiste nel database delle località, questo cmdlet creerà quella località.

    Set-CsLisWirelessAccessPoint -BSSID 99-99-99-99-99-99 -Location "30/1000" -HouseNumber 1234 -PreDirectional NE -StreetName First -StreetSuffix Avenue -City Redmond -State WA -Country US -PostalCode 99999

## Descrizione dettagliata

Enhanced 9-1-1 consente all'operatore del servizio di emergenza di identificare la località di un chiamante senza dover richiedere questa informazione al chiamante. Nel caso in cui una persona stia chiamando tramite una connessione VoIP (Voice over Internet Protocol), queste informazioni possono essere dedotte da diversi elementi della connessione. L'amministratore della connessione VoIP deve configurare una mappa delle località (chiamata wiremap) che consente di determinare la località di un chiamante. Questo cmdlet consente all'amministratore di mappare una località fisica al WAP attraverso il quale la chiamata è stata instradata.

Il parametro BSSID è il solo parametro richiesto per questo cmdlet. Se si fornisce un valore di BSSID che già esiste, questo cmdlet aggiornerà la località per quel WAP basandosi sul parametro di località fornito. Se il BSSID non esiste, verrà creata una nuova località WAP.

Se una località con un indirizzo esattamente corrispondente ai parametri di indirizzo immessi ora (compresi i valori null) non esiste nel database delle località, verrà creata una nuova località basata sui parametri immessi con questo cmdlet. È possibile ottenere un elenco di località utilizzando il cmdlet **Get-CsLisLocation**. Il cmdlet **Set-CsLisWirelessAccessPoint** non richiede i parametri di località; è possibile creare una voce WAP senza associarvi una località. Con questo cmdlet è anche possibile creare una località non valida. Una località valida comprende, come minimo, i valori relativi a Location, HouseNumber, StreetName, City, State e Country. Se non si forniscono tutti questi parametri, le chiamate ricevute dal WAP di riferimento potrebbero non contenere le informazioni necessarie all'operatore del servizio di emergenza. Si raccomanda di essere il più specifici possibile con i parametri di località e di compilarne quanti più possibile.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsLisWirelessAccessPoint** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsLisWirelessAccessPoint"}

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
<td><p><em>BSSID</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>BSSID (Basic Service Set Identifier) del punto di accesso wireless. Questo valore deve essere nel formato nn-nn-nn-nn-nn-nn, ad esempio 12-34-56-78-90-ab. Se non esiste una voce con il valore BSSID specificato, verrà creata una nuova località WAP. Se esiste già una voce con il BSSID specificato, tale voce verrà sostituita.</p></td>
</tr>
<tr class="even">
<td><p><em>City</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>La città in cui si trova la località.</p>
<p>Lunghezza massima: 64 caratteri.</p></td>
</tr>
<tr class="odd">
<td><p><em>CompanyName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome della società in questa località.</p>
<p>Lunghezza massima: 60 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Country</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il paese/area geografica in cui si trova questa località.</p>
<p>Lunghezza massima: 2 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Una descrizione dettagliata della località di questo WAP.</p></td>
</tr>
<tr class="odd">
<td><p><em>HouseNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il numero civico della località. Il valore indica il numero civico in cui si trova la società.</p>
<p>Lunghezza massima: 10 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>HouseNumberSuffix</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Informazioni aggiuntive sul numero civico, quali 1/2 o A. Ad esempio, 1234 1/2 Oak Street o 1234 A Elm Street.</p>
<p>Nota: Per designare un numero di appartamento o di ufficio, si deve utilizzare il parametro Location. Ad esempio, -Location &quot;Suite 100/Office 150&quot;.</p>
<p>Lunghezza massima: 5 caratteri</p></td>
</tr>
<tr class="odd">
<td><p><em>Location</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome della località. Normalmente questo valore è il nome di una località più specifico dell'indirizzo stradale, quale un numero di ufficio, ma può essere qualunque valore di stringa.</p>
<p>Lunghezza massima: 20 caratteri</p></td>
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

Accetta input tramite pipeline da oggetti punto di accesso wireless LIS.

## Tipi restituiti

Questo cmdlet consente di creare o modificare un oggetto di tipo System.Management.Automation.PSCustomObject.

## Vedere anche

#### Ulteriori risorse

[Remove-CsLisWirelessAccessPoint](remove-csliswirelessaccesspoint.md)  
[Get-CsLisWirelessAccessPoint](get-csliswirelessaccesspoint.md)  
[Get-CsLisLocation](get-cslislocation.md)

