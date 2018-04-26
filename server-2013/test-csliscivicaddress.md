---
title: Test-CsLisCivicAddress
TOCTitle: Test-CsLisCivicAddress
ms:assetid: 4079e767-3339-40c9-b7cd-08ec6c9d2c25
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425914(v=OCS.15)
ms:contentKeyID: 49300318
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsLisCivicAddress

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica uno o più indirizzi civici rispetto allo stradario generale. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsLisCivicAddress [-City <String>] [-Confirm [<SwitchParameter>]] [-Country <String>] [-HouseNumber <String>] [-HouseNumberSuffix <String>] [-PostalCode <String>] [-PostDirectional <String>] [-PreDirectional <String>] [-State <String>] [-StreetName <String>] [-StreetSuffix <String>] [-UpdateValidationStatus <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Questo comando convalida l'indirizzo con le proprietà che corrispondono ai valori specificati in questi parametri rispetto allo stradario generale. Si noti l'inclusione del parametro UpdateValidationStatus alla fine per aggiornare la proprietà MSAGValid dell'indirizzo.

    Test-CsLisCivicAddress -HouseNumber 1234 -HouseNumberSuffix "" -PreDirectional "" -StreetName Main -StreetSuffix St -PostDirectional "" -City Redmond -State WA -PostalCode 99999 -Country US -UpdateValidationStatus

## ESEMPIO 2

In questo esempio viene illustrato come verificare tutti gli indirizzi civici LIS. L'esempio inizia con una chiamata al cmdlet **Get-CsLisCivicAddress** per recuperare tutti gli indirizzi civici definiti nel database delle posizioni. Questi indirizzi vengono inviati tramite pipe al cmdlet **Test-CsLisCivicAddress**, che utilizza il servizio Web del provider del routing di rete del servizio per chiamate di emergenza (E9-1-1) per convalidare ogni indirizzo.

    Get-CsLisCivicAddress | Test-CsLisCivicAddress -UpdateValidationStatus

## Descrizione dettagliata

In un'implementazione di VoIP aziendale con Enhanced 9-1-1 (E9-1-1), le posizioni degli utenti sono determinate sulla base di mappe di posizione che mappano una subnet, una porta, uno switch o un punto di accesso wireless a una posizione. In assenza di una connessione a una posizione mappata, è possibile richiedere all'utente di immettere la sua posizione manualmente. Gli indirizzi di queste posizioni devono essere convalidati rispetto allo stradario informatico dal provider del routing di rete del servizio di chiamate di emergenza. Questo cmdlet utilizza il servizio Web di tale provider per convalidare gli indirizzi mappati. È possibile configurare un provider di servizi chiamando il cmdlet **Set-CsLisServiceProvider**.

Se si desidera aggiornare la proprietà MSAGValid dell'indirizzo civico, è necessario includere il parametro UpdateValidationStatus nella chiamata al cmdlet **Test-CsLisCivicAddress**. Utilizzare il cmdlet **Get-CsLisCivicAddress** per recuperare gli indirizzi civici.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Test-CsLisCivicAddress** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsLisCivicAddress"}

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
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>La città della posizione.</p>
<p>Lunghezza massima: 64 caratteri.</p></td>
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
<td><p><em>HouseNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il numero civico della posizione. Nel caso di una società è il numero nella via in cui ha sede la società.</p>
<p>Lunghezza massima: 10 caratteri</p></td>
</tr>
<tr class="odd">
<td><p><em>HouseNumberSuffix</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Informazioni aggiuntive sul numero civico, come 1/2 o A. Ad esempio: 1234 1/2 Oak Street o 1234 A Elm Street.</p>
<p>Lunghezza massima: 5 caratteri</p></td>
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
<td><p>La designazione direzionale per un nome di una via che precede il nome della via. Esempio: NE o NW per NE Main Street o NW 7th Avenue.</p>
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
<td><p><em>UpdateValidationStatus</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se si include questo parametro la proprietà MSAGValid dell'indirizzo civico viene modificata in base al risultato della convalida dell'indirizzo con questo cmdlet. Se l'indirizzo è valido, MSAGValid viene impostato su True. Se si omette questo parametro, il valore di MSAGValid resta invariato.</p></td>
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

Consente di accettare l'input da pipeline contenente un oggetto indirizzo civico LIS (Location Information Server).

## Tipi restituiti

Questo cmdlet non restituisce un valore.

## Vedere anche

#### Ulteriori risorse

[Get-CsLisCivicAddress](get-csliscivicaddress.md)

