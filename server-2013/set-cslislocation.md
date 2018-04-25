---
title: Set-CsLisLocation
TOCTitle: Set-CsLisLocation
ms:assetid: 955cdce0-250d-48b7-8891-5355d801911f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398757(v=OCS.15)
ms:contentKeyID: 49301366
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsLisLocation

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova posizione o modifica una posizione esistente nel database di configurazione delle posizioni per il servizio di chiamate di emergenza Enhanced 9-1-1 (E9-1-1). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsLisLocation -Instance <PSObject> [-City <String>] [-CompanyName <String>] [-Country <String>] [-HouseNumber <String>] [-HouseNumberSuffix <String>] [-Location <String>] [-PostalCode <String>] [-PostDirectional <String>] [-PreDirectional <String>] [-State <String>] [-StreetName <String>] [-StreetSuffix <String>] <COMMON PARAMETERS>

    Set-CsLisLocation -City <String> -CompanyName <String> -Country <String> -HouseNumber <String> -HouseNumberSuffix <String> -Location <String> -PostalCode <String> -PostDirectional <String> -PreDirectional <String> -State <String> -StreetName <String> -StreetSuffix <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con l'esempio 1 viene creata una nuova posizione denominata Bldg30NEWing. Questo comando specifica tutti i parametri per cui è obbligatorio un valore per la creazione di una posizione. In questo esempio l'indirizzo della posizione è 1000 Main, Redmond, WA, US. Tale indirizzo viene immesso specificando il parametro HouseNumber con il valore 1000, il parametro StreetName con il valore Main, il parametro City con il valore Redmond e il parametro Country con il valore US.

Se si esegue un comando solo con i parametri mostrati, verrà richiesto di immettere ulteriori parametri. È tuttavia possibile premere INVIO a ogni richiesta senza specificare valori per creare la posizione.

    Set-CsLisLocation -Location Bldg30NEWing -HouseNumber 1000 -StreetName Main -City Redmond -State WA -Country US

## ESEMPIO 2

Questo esempio è simile all'esempio 1 in quanto crea una nuova posizione. Tuttavia, in questo esempio il comando specifica tutti i parametri per il cmdlet. In questo modo si evitano i messaggi di richiesta che seguivano il comando nell'esempio 1, perché in questo esempio tutti i valori che si desidera lasciare vuoti sono impostati su stringhe vuote.

    Set-CsLisLocation -Location "Suite 100/Office 20" -CompanyName "Litware, Inc." -HouseNumber 1234 -HouseNumberSuffix "" -PreDirectional "" -StreetName Main -StreetSuffix St -PostDirectional "" -City Redmond -State WA -PostalCode 99999 -Country US

## ESEMPIO 3

In questo esempio viene modificata la posizione creata nell'esempio 1. La prima riga dell'esempio inizia con una chiamata al cmdlet **Get-CsLisLocation**. Viene restituita una raccolta di tutte le posizioni definite nella distribuzione di Lync Server. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** recupera tutti gli elementi della raccolta in cui la proprietà Location è uguale (-ceq, con distinzione tra maiuscole e minuscole) a Bldg30NEWing. L'oggetto corrispondente a questo criterio viene assegnato alla variabile $a.

Nella riga 2 viene chiamato il cmdlet **Set-CsLisLocation**. Il primo parametro è il parametro Instance. A questo parametro viene passata la variabile ($a) contenente l'oggetto recuperato nella riga 1, ovvero l'oggetto che si desidera modificare. Viene quindi specificato il parametro StreetSuffix, a cui viene passato il valore Street. In questo modo il valore della proprietà StreetSuffix della posizione nella variabile $a viene cambiato in Street.

Tenere presente che, poiché Location non è una proprietà univoca, il cmdlet **Where-Object** può restituire più posizioni. In questo caso, l'esempio non funzionerà. Per modificare più posizioni contemporaneamente, vedere l'esempio 4.

    $a = Get-CsLisLocation | Where-Object {$_.Location -ceq "Bldg30NEWing"}
    Set-CsLisLocation -Instance $a -StreetSuffix Street

## ESEMPIO 4

Con l'esempio 4 viene modificata la proprietà StreetSuffix di uno o più oggetti posizione. L'esempio inizia in modo molto simile all'esempio 3. Viene innanzitutto chiamato il cmdlet **Get-CsLisLocation** per recuperare tutte le posizioni. Questa raccolta di posizioni viene quindi inviata tramite pipe al cmdlet **Where-Object**, che circoscrive la raccolta alle posizioni la cui proprietà Location è uguale a NorthCampus. Questa nuova raccolta viene archiviata nella variabile $a. Nella riga 2 il contenuto di $a viene inviato tramite pipe al cmdlet **Set-CsLisLocation**. Questo cmdlet esegue un'iterazione nei diversi oggetti (o posizioni) archiviati in $a, modificandoli. In questo caso la modifica prevede il cambiamento della proprietà StreetSuffix di ogni oggetto in Avenue.

I comandi in questo esempio possono essere eseguiti anche senza l'utilizzo di una variabile. È sufficiente inviare tramite pipe i risultati del cmdlet **Where-Object** al cmdlet **Set-CsLisLocation**:

Get-CsLisLocation | Where-Object {$\_.Location -ceq "NorthCampus"} | Set-CsLisLocation -StreetSuffix Avenue

    $a = Get-CsLisLocation | Where-Object {$_.Location -ceq "NorthCampus"}
    $a | Set-CsLisLocation -StreetSuffix Avenue

## Descrizione dettagliata

Il servizio E9-1-1 consente a chi risponde alle chiamate di emergenza di determinare la posizione geografica del chiamante senza dovergli richiedere tali informazioni. In Lync Server la posizione viene determinata in base al mapping di porta, subnet, commutatore o punto di accesso wireless del chiamante a una posizione specifica. Questa mappa è nota come mappa delle posizioni (wiremap). Questo cmdlet aggiunge un nuovo indirizzo o modifica un indirizzo esistente nell'elenco delle posizioni archiviate nel relativo database di configurazione nel server LIS (Location Information Server). Le posizioni vengono quindi confrontate con un elenco di indirizzi validi forniti dal provider dei servizi di emergenza che collabora con la società.

La combinazione di tutti i parametri obbligatori (diversi da Instance) per questo cmdlet costituisce una voce univoca. La modifica di uno qualsiasi di questi parametri provocherà la creazione di una nuova posizione, anziché la modifica di una posizione esistente. Anche se tutti questi parametri sono obbligatori, alcuni possono contenere valori null. I parametri che devono contenere valori diversi da null sono Location, HouseNumber, StreetName, City, State e Country. Per modificare un valore esistente è necessario utilizzare il parametro Instance (o inviare tramite pipe un'istanza al cmdlet).

Oltre a utilizzare questo cmdlet per creare una posizione, viene creata automaticamente una posizione anche quando viene immesso un nuovo indirizzo per la porta, la subnet, il commutatore o il punto di accesso wireless. Queste informazioni possono essere immesse mediante i cmdlet **Set-CsLisPort**, **Set-CsLisSubnet**, **Set-CsLisSwitch** e **Set-CsLisWirelessAccessPoint**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Set-CsLisLocation** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsLisLocation"}

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
<td><p><em>City</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>La città della posizione.</p>
<p>Lunghezza massima: 64 caratteri.</p></td>
</tr>
<tr class="even">
<td><p><em>CompanyName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il nome della società in questa posizione.</p>
<p>Lunghezza massima: 60 caratteri</p></td>
</tr>
<tr class="odd">
<td><p><em>Country</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il paese/area geografica in cui si trova la posizione.</p>
<p>Lunghezza massima: 2 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>HouseNumber</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il numero civico della posizione. Nel caso di una società è il numero nella via in cui ha sede la società.</p>
<p>Lunghezza massima: 10 caratteri</p></td>
</tr>
<tr class="odd">
<td><p><em>HouseNumberSuffix</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Informazioni aggiuntive sul numero civico, come 1/2 o A. Ad esempio: 1234 1/2 Oak Street o 1234 A Elm Street.</p>
<p>Nota: per indicare un numero di appartamento o di un ufficio, è necessario utilizzare il parametro Location. Ad esempio: -Location &quot;Suite 100/Office 150&quot;.</p>
<p>Lunghezza massima: 5 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSObject</p></td>
<td><p>Un riferimento a un oggetto posizione. Questo oggetto deve includere le proprietà richieste per creare una posizione. È possibile recuperare un oggetto di questo tipo chiamando il cmdlet <strong>Get-CsLisLocation</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Location</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il nome della posizione. Generalmente questo valore è il nome di una posizione più specifica rispetto all'indirizzo civico, quale un numero di ufficio, ma può essere qualsiasi valore stringa.</p>
<p>Lunghezza massima: 20 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>PostalCode</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il codice postale associato a questa posizione.</p>
<p>Lunghezza massima: 10 caratteri</p></td>
</tr>
<tr class="odd">
<td><p><em>PostDirectional</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>La designazione direzionale di una via. Esempio: NE o NW per Main Street NE o 7th Avenue NW.</p>
<p>Lunghezza massima: 2 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>PreDirectional</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>La designazione direzionale per un nome di una via che precede il nome della via. Esempio: NE o NW per NE Main Street o NW 7th Avenue.</p>
<p>Lunghezza massima: 2 caratteri</p></td>
</tr>
<tr class="odd">
<td><p><em>State</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Lo stato o la provincia associato a questa posizione.</p>
<p>Lunghezza massima: 2 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>StreetName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il nome della via per questa posizione.</p>
<p>Lunghezza massima: 60 caratteri</p></td>
</tr>
<tr class="odd">
<td><p><em>StreetSuffix</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il tipo di via indicato nel nome, ad esempio Street, Avenue o Court.</p>
<p>Lunghezza massima: 10 caratteri</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Consente di accettare l'input da pipeline di oggetti posizione LIS.

## Tipi restituiti

Questo cmdlet non restituisce un valore o un oggetto. Crea o modifica un oggetto di tipo System.Management.Automation.PSCustomObject.

## Vedere anche

#### Ulteriori risorse

[Remove-CsLisLocation](remove-cslislocation.md)  
[Get-CsLisLocation](get-cslislocation.md)  
[Set-CsLisPort](set-cslisport.md)  
[Set-CsLisSubnet](set-cslissubnet.md)  
[Set-CsLisSwitch](set-cslisswitch.md)  
[Set-CsLisWirelessAccessPoint](set-csliswirelessaccesspoint.md)  
[Get-CsLisCivicAddress](get-csliscivicaddress.md)

