---
title: Set-CsDialInConferencingAccessNumber
TOCTitle: Set-CsDialInConferencingAccessNumber
ms:assetid: 2b640607-ee83-4962-865d-ed74ddd17649
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425770(v=OCS.15)
ms:contentKeyID: 49300022
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsDialInConferencingAccessNumber

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica i valori delle proprietà di un numero di accesso a conferenze telefoniche con accesso esterno esistente. Le conferenze telefoniche con accesso esterno consentono agli utenti di utilizzare un normale telefono, un cellulare o un altro dispositivo sulla rete PSTN (Public Switched Telephone Network) per partecipare alla parte audio di una conferenza. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsDialInConferencingAccessNumber -Identity <UserIdParameter> [-DisplayName <String>] [-DisplayNumber <String>] [-LineUri <String>] [-PrimaryLanguage <String>] [-Regions <MultiValuedProperty>] [-ScopeToGlobal <SwitchParameter>] [-ScopeToSite <SwitchParameter>] [-SecondaryLanguages <MultiValuedProperty>] <COMMON PARAMETERS>

    Set-CsDialInConferencingAccessNumber -Identity <UserIdParameter> -Priority <Int32> -ReorderedRegion <String> <COMMON PARAMETERS>

    Set-CsDialInConferencingAccessNumber -Instance <AccessNumber> [-ScopeToGlobal <SwitchParameter>] [-ScopeToSite <SwitchParameter>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 consente di modificare la proprietà DisplayName del numero di accesso alla conferenza telefonica con accesso esterno con Identity sip:RedmondDialIn@litwareinc.com. In questo esempio, il nome visualizzato è impostato su "Redmond Dial-In Access Number".

    Set-CsDialInConferencingAccessNumber -Identity "sip:RedmondDialIn@litwareinc.com" -DisplayName "Redmond Dial-In Access Number"

## ESEMPIO 2

Nell'Esempio 2, il numero di accesso alla conferenza telefonica con accesso esterno con Identity sip:RedmondDialIn@litwareinc.com è stato modificato con l'inclusione di due aree: Redmond e Seattle. Per ottenere questo risultato, viene utilizzato il parametro Region, seguito dalle due aree (due stringhe separate da virgole). Si noti che questo comando avrà esito negativo se le due aree Redmond e Seattle non sono già state definite nei dial plan.

    Set-CsDialInConferencingAccessNumber -Identity "sip:RedmondDialIn@litwareinc.com" -Regions "Redmond", "Seattle"

## ESEMPIO 3

Nell'esempio 3 tutti i numeri di accesso a conferenze telefoniche con accesso esterno in cui la lingua principale è il francese vengono modificati in modo da utilizzare il francese canadese come lingua secondaria. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsDialInConferencingAccessNumber** per restituire una raccolta di tutti i numeri di accesso esterno configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i numeri di accesso in cui la proprietà PrimaryLanguage è uguale a "fr-FR" (francese). Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsDialInConferencingAccessNumber**, che imposta il valore della proprietà SecondaryLanguages su "fr-CA" (francese canadese).

    Get-CsDialInConferencingAccessNumber | Where-Object {$_.PrimaryLanguage -eq "fr-FR"}| Set-CsDialInConferencingAccessNumber -SecondaryLanguages "fr-CA"

## ESEMPIO 4

Il comando riportato nell'esempio 4 cambia il nome visualizzato in Active Directory per il numero di accesso a conferenze telefoniche con accesso esterno specificato. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsDialInConferencingAccessNumber** e il parametro Filter per restituire il numero di accesso esterno in cui la proprietà DisplayName è uguale a "Default DialIn Access Number". Il numero di accesso così ottenuto viene quindi inviato tramite pipe al cmdlet **Set-CsDialInConferencingAccessNumber**, che cambia il nome visualizzato impostandolo su Litwareinc Conferencing.

    Get-CsDialInConferencingAccessNumber -Filter {DisplayName -eq "Default DialIn Access Number"} | Set-CsDialInConferencingAccessNumber -DisplayName "Litwareinc Conferencing"

## ESEMPIO 5

Nell'esempio 5 sia il numero visualizzato sia l'URI (Uniform Resource Identifier) di linea vengono modificati per il numero di accesso a conferenze telefoniche con accesso esterno specificato. Per recuperare il numero da modificare, il comando innanzitutto utilizza il cmdlet **Get-CsDialInConferencingAccessNumber** e il parametro Filter. Il valore di filtro associato restituisce solo i dati relativi al numero di accesso in cui la proprietà LineUri è uguale a TEL:+14255558715. Il numero di accesso così ottenuto viene quindi inviato tramite pipe al cmdlet **Set-CsDialInConferencingAccessNumber**, che ne modifica le proprietà DisplayNumber e LineUri.

    Get-CsDialInConferencingAccessNumber -Filter {LineUri -eq "TEL:+14255558715"} | Set-CsDialInConferencingAccessNumber -DisplayNumber "1-425-555-1298" -LineUri "tel:+14255551298"

## ESEMPIO 6

Nell'esempio 6 viene assegnata una coppia di lingue secondarie a tutti i numeri di accesso a conferenze telefoniche con accesso esterno che non utilizzano l'inglese americano come lingua principale. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsDialInConferencingAccessNumber** per restituire una raccolta di tutti i numeri di accesso a conferenze telefoniche con accesso esterno configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i numeri in cui la proprietà PrimaryLanguage è diversa da en-US (inglese americano). La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsDialInConferencingAccessNumber**, che utilizza il parametro -SecondaryLanguages per assegnare a ogni numero della raccolta le lingue secondarie francese (fr-FR) e italiano (it-IT).

    Get-CsDialInConferencingAccessNumber | Where-Object {$_.PrimaryLanguage -ne "en-US"} | Set-CsDialInConferencingAccessNumber -SecondaryLanguages "fr-FR","it-IT"

## ESEMPIO 7

Il comando riportato nell'esempio 7 assegna al numero di accesso "sip:RedmondDialIn@litwareinc.com" la priorità più alta nell'area di Redmond; questo numero verrà visualizzato per primo negli inviti alle riunioni e sulla pagina Web della conferenza con accesso esterno. Per impostare la priorità, viene utilizzato il parametro Priority con il valore 0. Il numero di accesso con priorità più alta ha il valore 0, il successivo ha il valore 1 e così via. Inoltre, viene incluso il parametro ReorderedRegion per indicare che le priorità dei numeri di accesso devono essere modificate nell'area di Redmond.

    Get-CsDialInConferencingAccessNumber -Identity ""sip:RedmondDialIn@litwareinc.com"" -Priority 0 -ReorderedRegion Redmond

## Descrizione dettagliata

Le conferenze telefoniche con accesso esterno consentono agli utenti di utilizzare qualsiasi tipo di telefono, ad esempio una linea terrestre standard, un telefono cellulare o un telefono VoIP (Voice over Internet Protocol), per partecipare alla parte audio di una conferenza. In questo modo, anche gli utenti che non dispongono di un computer o di una connessione Internet possono partecipare alla riunione. Gli utenti connessi tramite chiamata in ingresso possono usufruire delle funzionalità audio complete: possono parlare ad altri partecipanti e ascoltare tutto ciò che accade. Non sono però in grado di vedere diapositive, video o altri contributi visivi.

Per offrire agli utenti le funzionalità delle conferenze telefoniche con accesso esterno, è necessario creare numeri di accesso alle conferenze telefoniche con accesso esterno, ovvero numeri di telefono che gli utenti possono comporre per collegarsi a una riunione. I numeri di accesso alle conferenze telefoniche con accesso esterno vengono creati utilizzando il cmdlet **New-CsDialInConferencingAccessNumber**. Quando viene creato un nuovo numero di accesso a conferenze telefoniche con accesso esterno, di fatto viene creato un nuovo oggetto contatto in Servizi di dominio Active Directory. Questo oggetto contatto viene utilizzato per rappresentare il numero di accesso e tutte le relative proprietà.

Dopo la creazione di un numero di accesso a conferenze telefoniche con accesso esterno, è possibile utilizzare il cmdlet **Set-CsDialInConferencingAccessNumber** per modificarne le proprietà. Ad esempio, è possibile cambiare il numero di telefono stesso (LineUri) o il nome visualizzato dell'oggetto contatto che rappresenta il numero. Il cmdlet **Set-CsDialInConferencingAccessNumber** inoltre consente di modificare l'ambito del numero. Ad esempio, è possibile utilizzare questo cmdlet per riassegnare all'ambito del sito un numero precedentemente assegnato all'ambito globale.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsDialInConferencingAccessNumber** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsDialInConferencingAccessNumber"}

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
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>L'indirizzo SIP dell'oggetto contatto che rappresenta il numero di conferenza telefonica con accesso esterno. Quando si specifica l'identità, è necessario includere il prefisso &quot;sip:&quot;; ad esempio: -Identity &quot; sip:RedmondDialIn@litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.AccessNumber</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Int32</p></td>
<td><p>Consente di cambiare l'ordine in cui i numeri di conferenza telefonica con accesso esterno vengono presentati agli utenti negli inviti alle riunioni o quando accedono alla pagina Web Impostazioni conferenza telefonica con accesso esterno. I numeri più bassi hanno una priorità più alta. Per fare in modo che un numero venga visualizzato all'inizio dell'elenco, impostare la priorità su 0. Si noti che, se si modifica la priorità di un determinato numero, è necessario utilizzare anche il parametro ReorderedRegion per indicare l'area in cui la nuova priorità deve essere applicata.</p></td>
</tr>
<tr class="even">
<td><p><em>ReorderedRegion</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Utilizzato con il parametro Priority quando si cambia la priorità di un numero di conferenza telefonica con accesso esterno in un'area. Il parametro ReorderedRegion indica l'area in cui deve essere applicato il riordino della priorità, ad esempio: -ReorderedRegion &quot;Redmond&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome visualizzato in Active Directory per il nuovo oggetto contatto. Si tratta del nome che verrà visualizzato anche in Lync.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Numero di telefono visualizzato negli inviti alle riunioni e sulla pagina Impostazioni conferenza telefonica con accesso esterno. È possibile formattare la proprietà DisplayNumber a propria discrezione: ad esempio, 1-800-555-1234; 1-(800)-555-1234; o 1.800.555.1234.</p></td>
</tr>
<tr class="even">
<td><p><em>LineUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Numero di telefono della conferenza telefonica con accesso esterno. ﻿Specificare il LineUri utilizzando la seguente sintassi: il prefisso tel: seguito dal segno più (+) seguito dal prefisso internazionale, dal prefisso locale e dal numero telefonico. Ad esempio: tel:+18005551234. Si noti che non sono consentiti spazi, trattini, parentesi e altri caratteri.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di passare attraverso la pipeline un oggetto contatto che rappresenta il numero di accesso alla conferenza telefonica con accesso esterno modificato. Per impostazione predefinita, il cmdlet <strong>Set-CsDialInConferencingAccessNumber</strong> non passa alcun oggetto attraverso la pipeline.</p></td>
</tr>
<tr class="even">
<td><p><em>PrimaryLanguage</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Lingua principale utilizzata per gli annunci di conferenza telefonica con accesso esterno. La lingua deve essere configurata utilizzando uno dei codici della lingua disponibili per la conferenza telefonica con accesso esterno, ad esempio, en-US per inglese Stati Uniti o fr-FR per francese. Per visualizzare un elenco dei codici della lingua disponibili, al prompt di Windows PowerShell digitare il comando seguente:</p>
<p>Get-CsDialInConferencingLanguageList | Select-Object -ExpandProperty Languages.</p></td>
</tr>
<tr class="odd">
<td><p><em>Regions</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.MultiValuedProperty</p></td>
<td><p>Aree di dial plan associate al numero di accesso. Se un'area non è inclusa in almeno un dial plan, non può essere associata a un numero di accesso alla conferenza telefonica con accesso esterno. Per specificare più aree, utilizzare le virgole per separarle: -Regions &quot;Northwest&quot;, &quot;Southwest&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>ScopeToGlobal</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, il numero di conferenza telefonica con accesso esterno verrà assegnato all'ambito globale.</p></td>
</tr>
<tr class="odd">
<td><p><em>ScopeToSite</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, il numero di conferenza telefonica con accesso esterno verrà assegnato all'ambito del sito in cui risiede il pool di registrazione dell'oggetto contatto.</p></td>
</tr>
<tr class="even">
<td><p><em>SecondaryLanguages</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.MultiValuedProperty</p></td>
<td><p>Raccolta facoltativa di lingue utilizzabili per gli annunci della conferenza telefonica con accesso esterno. Le lingue secondarie devono essere configurate sotto forma di elenco di codici delimitati da virgole; ad esempio, la sintassi seguente imposta francese canadese e francese come lingue secondarie: -SecondaryLanguages &quot;fr-CA&quot;, &quot;fr-FR&quot;.</p>
<p>Un numero di accesso può essere associato a un massimo di quattro lingue secondarie.</p></td>
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

Oggetto Microsoft.Rtc.Management.Xds.AccessNumber. Il cmdlet **Set-CsDialInConferencingAccessNumber** accetta l'input da pipeline dell'oggetto numero di accesso.

## Tipi restituiti

Il cmdlet **Set-CsDialInConferencingAccessNumber** non restituisce oggetti o valori. Il cmdlet invece configura le istanze dell'oggetto Microsoft.Rtc.Management.Xds.AccessNumber.

## Vedere anche

#### Ulteriori risorse

[Get-CsDialInConferencingAccessNumber](get-csdialinconferencingaccessnumber.md)  
[New-CsDialInConferencingAccessNumber](new-csdialinconferencingaccessnumber.md)  
[Remove-CsDialInConferencingAccessNumber](remove-csdialinconferencingaccessnumber.md)

