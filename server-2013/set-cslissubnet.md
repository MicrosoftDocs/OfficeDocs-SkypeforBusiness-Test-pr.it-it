---
title: Set-CsLisSubnet
TOCTitle: Set-CsLisSubnet
ms:assetid: e51ef9ec-c307-4046-b64b-f23b354713fc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399016(v=OCS.15)
ms:contentKeyID: 49302272
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsLisSubnet

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una subnet del server Informazioni percorso, crea un'associazione tra una subnet e una posizione (creando una nuova posizione se questa non esiste) o modifica una subnet esistente e la relativa posizione associata. L'associazione tra subnet e posizione viene utilizzata in un'implementazione di VoIP aziendale con il servizio di chiamate di emergenza Enhanced 9-1-1 (E9-1-1) per segnalare la posizione del chiamante all'operatore del servizio di emergenza. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsLisSubnet -Subnet <String> [-Description <String>] <COMMON PARAMETERS>

    Set-CsLisSubnet -Subnet <String> [-City <String>] [-CompanyName <String>] [-Country <String>] [-Description <String>] [-HouseNumber <String>] [-HouseNumberSuffix <String>] [-Location <String>] [-PostalCode <String>] [-PostDirectional <String>] [-PreDirectional <String>] [-State <String>] [-StreetName <String>] [-StreetSuffix <String>] <COMMON PARAMETERS>

    Set-CsLisSubnet -City <String> -CompanyName <String> -Country <String> -HouseNumber <String> -HouseNumberSuffix <String> -Location <String> -PostalCode <String> -PostDirectional <String> -PreDirectional <String> -State <String> -StreetName <String> -StreetSuffix <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene creata o aggiornata una voce di posizione della subnet LIS. Il comando nell'esempio include solo un parametro (obbligatorio): Subnet. Il valore del parametro Subnet riportato nell'esempio è un indirizzo IPv4, 192.10.10.0.

Si noti che in questo esempio non sono incluse informazioni sull'indirizzo. È possibile creare una voce di subnet in Location Information Server senza associarla a un indirizzo. Tuttavia, le chiamate di emergenza instradate tramite questa subnet non possono (in base alle posizioni di porta o commutatore che sono state definite) contenere informazioni sufficienti all'operatore del servizio di emergenza per identificare una posizione.

IMPORTANTE: Se esiste già una posizione subnet LIS con questo valore Subnet, questa verrà sostituita dai valori utilizzati nel comando. Ciò significa che se la subnet era associata a un indirizzo (una posizione fisica), tale associazione non esiste più poiché nel comando non sono incluse informazioni sull'indirizzo. La posizione esisterà ancora nel database delle posizioni, ma non sarà associata a questa subnet.

    Set-CsLisSubnet -Subnet 192.10.10.0

## Descrizione dettagliata

La funzionalità per le chiamate di emergenza consente a un operatore di servizi di emergenza di identificare la posizione del chiamante senza doverla richiedere a quest'ultimo. Nel caso in cui la chiamata venga effettuata tramite connessione VoIP (Voice over Internet Protocol), questa informazione deve essere estratta in base a diversi fattori di connessione. L'amministratore VoIP deve configurare una mappa di posizioni (detta mappa reticolare) che permetta di determinare la posizione di un chiamante. Il cmdlet consente all'amministratore di eseguire il mapping delle posizioni fisiche alla subnet tramite cui il client è connesso.

Il parametro Subnet è l'unico parametro obbligatorio per questo cmdlet. Se si immette un valore Subnet che esiste già, con il cmdlet verrà aggiornata la posizione per tale subnet in base ai parametri della posizione forniti. Se non esiste, verrà creato un nuovo percorso per la subnet.

Se nel database delle posizioni non esiste una posizione con un indirizzo che corrisponde esattamente ai parametri immessi qui (inclusi i valori NULL), verrà creato un nuovo indirizzo in base ai parametri immessi con questo cmdlet. Per recuperare un elenco delle posizioni, è possibile chiamare il cmdlet **Get-CsLisLocation**. Il cmdlet **Set-CsLisSubnet** non richiede parametri relativi alla posizione. È possibile creare una voce di subnet senza associarla a una posizione. È inoltre possibile creare una posizione non valida con questo cmdlet. Una posizione valida è costituita almeno dai parametri Location, HouseNumber, StreetName, City, State e Country. Se tali parametri non vengono forniti, le chiamate che provengono dalla subnet specificata possono non contenere le informazioni necessarie all'operatore del servizio di emergenza (a seconda che siano disponibili impostazioni valide per un commutatore, una porta o un punto di accesso wireless che possono essere utilizzate al posto delle impostazioni della subnet). È consigliabile essere più specifici possibile con i parametri della posizione e completarne il maggior numero possibile.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsLisSubnet** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsLisSubnet"}

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
<td><p><em>Subnet</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>L'indirizzo IP della subnet. Il valore dovrebbe essere immesso come un indirizzo IPv4 (cifre separate da punti come 192.0.2.0).</p></td>
</tr>
<tr class="even">
<td><p><em>City</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>La città della posizione.</p>
<p>Lunghezza massima: 64 caratteri.</p></td>
</tr>
<tr class="odd">
<td><p><em>CompanyName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome della società in questa posizione.</p>
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
<td><p>Il paese/area geografica in cui si trova la posizione.</p>
<p>Lunghezza massima: 2 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Una descrizione dettagliata della posizione della subnet.</p></td>
</tr>
<tr class="odd">
<td><p><em>HouseNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il numero civico della posizione. Nel caso di una società, è il numero della via in cui questa ha sede.</p>
<p>Lunghezza massima: 10 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>HouseNumberSuffix</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Informazioni aggiuntive sul numero civico, come 1/2 o A. Ad esempio: 1234 1/2 Oak Street o 1234 A Elm Street.</p>
<p>Nota: per indicare un numero di appartamento o di un ufficio, è necessario utilizzare il parametro Location. Ad esempio: -Location &quot;Suite 100/Office 150&quot;.</p>
<p>Lunghezza massima: 5 caratteri</p></td>
</tr>
<tr class="odd">
<td><p><em>Location</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome della posizione. Generalmente questo valore è il nome di una posizione più specifica rispetto all'indirizzo civico, quale un numero di ufficio, ma può essere qualsiasi valore stringa.</p>
<p>Lunghezza massima: 20 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>PostalCode</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il codice postale associato a questa posizione.</p>
<p>Lunghezza massima: 10 caratteri</p></td>
</tr>
<tr class="odd">
<td><p><em>PostDirectional</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>La designazione direzionale di una via. Esempio: NE o NW per Main Street NE o 7th Avenue NW.</p>
<p>Lunghezza massima: 2 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>PreDirectional</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>La designazione direzionale per un nome di una via che precede il nome della via. Ad esempio, NE o NW per NE Main Street o NW 7th Avenue.</p>
<p>Lunghezza massima: 2 caratteri</p></td>
</tr>
<tr class="odd">
<td><p><em>State</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Lo stato o la provincia associato a questa posizione.</p>
<p>Lunghezza massima: 2 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>StreetName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome della via per questa posizione.</p>
<p>Lunghezza massima: 60 caratteri</p></td>
</tr>
<tr class="odd">
<td><p><em>StreetSuffix</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il tipo di via indicato nel nome, ad esempio Street, Avenue o Court.</p>
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

Accetta l'input da pipeline di oggetti subnet LIS.

## Tipi restituiti

Questo cmdlet consente di creare o modificare un oggetto di tipo System.Management.Automation.PSCustomObject.

## Vedere anche

#### Ulteriori risorse

[Remove-CsLisSubnet](remove-cslissubnet.md)  
[Get-CsLisSubnet](get-cslissubnet.md)  
[Get-CsLisLocation](get-cslislocation.md)

