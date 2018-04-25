---
title: Remove-CsLisLocation
TOCTitle: Remove-CsLisLocation
ms:assetid: 24e49a83-01a9-48ce-b940-fb0503f52077
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425722(v=OCS.15)
ms:contentKeyID: 49299953
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsLisLocation

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una località dal database di configurazione delle località per il servizio di chiamate di emergenza Enhanced 9-1-1 (E9-1-1). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsLisLocation [-City <String>] [-CompanyName <String>] [-Country <String>] [-HouseNumber <String>] [-HouseNumberSuffix <String>] [-Location <String>] [-PostalCode <String>] [-PostDirectional <String>] [-PreDirectional <String>] [-State <String>] [-StreetName <String>] [-StreetSuffix <String>] <COMMON PARAMETERS>

    Remove-CsLisLocation -City <String> -CompanyName <String> -Country <String> -HouseNumber <String> -HouseNumberSuffix <String> -Location <String> -PostalCode <String> -PostDirectional <String> -PreDirectional <String> -State <String> -StreetName <String> -StreetSuffix <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'Esempio 1 viene rimossa una località denominata Bldg30NEWing. Questo comando consente di specificare i valori per i parametri Location, HouseNumber, StreetName, City, State e Country. Ciò significa che queste sono le uniche proprietà della località da eliminare che contengono valori non Null. Se i valori del parametro non vengono forniti per tutte le proprietà non Null, la località non verrà eliminata. Verrà richiesto di immettere qualsiasi parametro non specificato nel comando, ma se i parametri contengono valori Null, è possibile premere Invio ad ogni richiesta.

    Remove-CsLisLocation -Location Bldg30NEWing -HouseNumber 1000 -StreetName Main -City Redmond -State WA -Country US

## ESEMPIO 2

In questo esempio verranno rimosse tutte le località a cui non fanno riferimento un punto di accesso wireless, un commutatore, una subnet o una porta LIS. Il comando innanzitutto chiama il cmdlet **Get-CsLisLocation**, specificando il parametro Unreferenced. Viene così restituita una raccolta di tutte le località a cui non fanno riferimento un punto di accesso wireless, un commutatore, una subnet o una porta LIS. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsLisLocation**, che rimuove ogni località della raccolta.

    Get-CsLisLocation -Unreferenced | Remove-CsLisLocation

## Descrizione dettagliata

E9-1-1 consente agli utenti che rispondono alle chiamate di emergenza di determinare la posizione geografica del chiamante senza dover chiedere al chiamante tale informazione. In Lync Server la località viene determinata in base al mapping del punto di accesso wireless, del commutatore, della subnet o della porta del chiamante con una località specifica. Questo cmdlet rimuove una località dal database di configurazione delle località. Tutte le proprietà di una località combinate rendono la località univoca. È necessario pertanto immettere tutte le proprietà non Null della località per rimuoverla. Se non vengono immesse tutte le proprietà non Null della località che si desidera rimuovere (e nessun'altra località include solo le proprietà specificate), non verrà rimossa alcuna località. In questo caso non verrà visualizzato un messaggio di errore, ma non verrà eseguita alcuna azione.

Questo cmdlet non rimuoverà le località associate a un punto di accesso wireless, un commutatore, una subnet o una porta LIS (Location Information Server). Se si tenta di rimuovere una località a cui fa riferimento uno di questo dispositivi, verrà visualizzato un errore. È necessario rimuovere tutti i riferimenti prima di rimuovere la località. È possibile utilizzare i cmdlet **Remove-CsLisPort**, **Remove-CsLisSubnet**, **Remove-CsLisSwitch** e **Remove-CsLisWirelessAccessPoint** per rimuovere tali riferimenti.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Remove-CsLisLocation** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsLisLocation"}

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
<td><p>La città in cui si trova la località.</p></td>
</tr>
<tr class="even">
<td><p><em>CompanyName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il nome della società in questa località.</p></td>
</tr>
<tr class="odd">
<td><p><em>Country</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il paese/area geografica in cui si trova la località. Questo valore conterrà due caratteri o meno.</p></td>
</tr>
<tr class="even">
<td><p><em>HouseNumber</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il numero civico della località. Il valore indica il numero civico in cui si trova la società.</p></td>
</tr>
<tr class="odd">
<td><p><em>HouseNumberSuffix</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Informazioni aggiuntive sul numero civico, quali 1/2 o A. Ad esempio, 1234 1/2 Oak Street o 1234 A Elm Street.</p></td>
</tr>
<tr class="even">
<td><p><em>Location</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il nome della località.</p></td>
</tr>
<tr class="odd">
<td><p><em>PostalCode</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il CAP associato alla località.</p></td>
</tr>
<tr class="even">
<td><p><em>PostDirectional</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>L'indicazione direzionale del nome della via. Ad esempio, NE o NW per Main Street NE o 7th Avenue NW.</p></td>
</tr>
<tr class="odd">
<td><p><em>PreDirectional</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>L'indicazione direzionale del nome che precede il nome della via. Ad esempio, NE o NW per NE Main Street o NW 7th Avenue.</p></td>
</tr>
<tr class="even">
<td><p><em>State</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Lo stato o la provincia associata alla località. Questo valore conterrà due o un numero inferiore di caratteri.</p></td>
</tr>
<tr class="odd">
<td><p><em>StreetName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il nome della via della località.</p></td>
</tr>
<tr class="even">
<td><p><em>StreetSuffix</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il tipo di via indicato nel nome, ad esempio, Via, Viale o Corso.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
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

Accetta input tramite pipeline da oggetti località LIS.

## Tipi restituiti

Questo cmdlet non restituisce alcun oggetto o valore. Consente di rimuovere un oggetto di tipo System.Management.Automation.PSCustomObject.

## Vedere anche

#### Ulteriori risorse

[Set-CsLisLocation](set-cslislocation.md)  
[Get-CsLisLocation](get-cslislocation.md)  
[Remove-CsLisPort](remove-cslisport.md)  
[Remove-CsLisSubnet](remove-cslissubnet.md)  
[Remove-CsLisSwitch](remove-cslisswitch.md)  
[Remove-CsLisWirelessAccessPoint](remove-csliswirelessaccesspoint.md)  
[Get-CsLisCivicAddress](get-csliscivicaddress.md)

