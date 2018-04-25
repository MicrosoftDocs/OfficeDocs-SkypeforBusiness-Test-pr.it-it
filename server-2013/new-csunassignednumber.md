---
title: New-CsUnassignedNumber
TOCTitle: New-CsUnassignedNumber
ms:assetid: 81b5d355-56d4-4325-8518-653de8e1fab4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398651(v=OCS.15)
ms:contentKeyID: 49301153
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsUnassignedNumber

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo intervallo di numeri non assegnati e le regole di routing che si applicano a tali numeri. Con l'esecuzione di questo cmdlet viene aggiunta una voce alla tabella di routing dei numeri non assegnati. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsUnassignedNumber -AnnouncementName <String> -AnnouncementService <String> -Identity <XdsGlobalRelativeIdentity> -NumberRangeEnd <String> -NumberRangeStart <String> <COMMON PARAMETERS>

    New-CsUnassignedNumber -ExUmAutoAttendantPhoneNumber <String> -Identity <XdsGlobalRelativeIdentity> -NumberRangeEnd <String> -NumberRangeStart <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Priority <Int32>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con questo esempio viene creato un intervallo di numeri non assegnati denominato UNSet1. Vengono utilizzati i parametri NumberRangeStart (+14255551000) e NumberRangeEnd (+14255551100) per definire l'intervallo di numeri non assegnati a cui si applica l'annuncio specificato. Infine, viene specificato l'annuncio fornendo prima il parametro AnnouncementService con l'ID di servizio del servizio Annunci e poi passando il valore "Welcome Announcement" al parametro AnnouncementName. È importante ricordare che l'annuncio con tale nome deve già essere esistente nel sistema.

    New-CsUnassignedNumber -Identity UNSet1 -NumberRangeStart "+14255551000" -NumberRangeEnd "+14255551100" -AnnouncementService ApplicationServer:redmond.litwareinc.com -AnnouncementName "Welcome Announcement"

## ESEMPIO 2

Con questo esempio viene creato un intervallo di numeri non assegnati denominato UNSet2. Come nell'esempio 1, vengono utilizzati i parametri NumberRangeStart (+14255552100) e NumberRangeEnd (+14255552200) per definire l'intervallo di numeri non assegnati a cui si applica l'annuncio specificato. Tuttavia, invece di utilizzare il servizio Annunci, in questo esempio l'intervallo di numeri utilizza l'Operatore automatico di Messaggistica unificata di Exchange. L'Operatore automatico è un singolo numero designato come numero principale per l'organizzazione, che guida gli utenti attraverso istruzioni vocali per aiutarli a raggiungere l'utente desiderato. Per completare il comando viene passato un numero di telefono al parametro ExUmAutoAttendantPhoneNumber. La Messaggistica unificata di Exchange deve essere già configurata e il numero deve corrispondere al numero di telefono di un oggetto contatto esistente in Servizi di dominio Active Directory. Il contatto deve essere un Operatore automatico (la proprietà AutoAttendant del contatto deve essere True).

    New-CsUnassignedNumber -Identity UNSet2 -NumberRangeStart "+14255552100" -NumberRangeEnd "+14255552200" -ExUmAutoAttendantPhoneNumber "+12065551234"

## ESEMPIO 3

L'esempio 3 è pressoché identico all'esempio 2. Consente di creare un intervallo di numeri non assegnati denominato UNSet2. In questo esempio è stato però aggiunto il parametro Priority, in questo caso con valore 2. Se è stato un definito un intervallo di numeri non assegnato che si sovrappone al presente e tale intervallo di numeri ha una priorità superiore (definita da un numero inferiore, ad esempio 1), le chiamate saranno instradate in base alle impostazioni di tale intervallo e non del presente.

    New-CsUnassignedNumber -Identity UNSet2 -NumberRangeStart "+14255552100" -NumberRangeEnd "+14255552200" -ExUmAutoAttendantPhoneNumber "+12065551234" -Priority 2

## Descrizione dettagliata

I numeri non assegnati sono numeri di telefono che sono stati assegnati a un'organizzazione, ma che non sono stati assegnati a utenti o telefoni specifici. Lync Server può essere configurato per instradare le chiamate alle destinazioni appropriate quando viene chiamato un numero non assegnato. Questo cmdlet crea le impostazioni che definiscono tale routing.

Prima di eseguire il cmdlet, il sistema deve disporre di annunci già definiti o di un Operatore automatico di Messaggistica unificata di Exchange già configurato. Per determinare se sono presenti annunci, chiamare il cmdlet **Get-CsAnnouncement**. Per creare un nuovo annuncio, chiamare il cmdlet **New-CsAnnouncement**. Per verificare le impostazioni dell'Operatore automatico di Messaggistica unificata di Exchange, eseguire il cmdlet **Get-CsExUmContact**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **New-CsUnassignedNumber** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsUnassignedNumber"}

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
<td><p><em>AnnouncementName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il nome dell'annuncio che sarà utilizzato per gestire le chiamate a questo intervallo di numeri.</p></td>
</tr>
<tr class="even">
<td><p><em>AnnouncementService</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il nome di dominio completo (FQDN) o l'ID del servizio del servizio Annunci. Questo parametro è obbligatorio solo se non è stato specificato un valore per il parametro ExUmAutoAttendantPhoneNumber.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExUmAutoAttendantPhoneNumber</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il numero di telefono dell'operatore automatico di Messaggistica unificata di Exchange cui instradare le chiamate nell'intervallo. Questo campo è obbligatorio solo se non si utilizza un servizio Annunci (caso in cui non vengono forniti valori per i parametri AnnouncementService o AnnouncementName). Il contatto dell'operatore automatico di Messaggistica unificata di Exchange deve essere già configurato per assegnare un valore a tale parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome univoco per l'intervallo di numeri non assegnati da creare. Tutti gli intervalli dei numeri non assegnati hanno ambito globale, quindi il nome specificato deve essere univoco nell'intera distribuzione di Lync Server.</p></td>
</tr>
<tr class="odd">
<td><p><em>NumberRangeEnd</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>L'ultimo numero nell'intervallo di numeri non assegnati. Deve essere maggiore o uguale al numero fornito per NumberRangeStart. Per specificare un intervallo composto da un solo numero, utilizzare lo stesso numero per NumberRangeStart e NumberRangeEnd.</p>
<p>Questo numero deve corrispondere all'espressione regolare (tel:)?(\+)?[1-9]\d{0,17}(;ext=[1-9]\d{0,9})?. Significa che il numero può iniziare con la stringa tel: (se questa non viene specificata, verrà aggiunta automaticamente), un segno più (+) e una cifra compresa tra 1 e 9. Il numero di telefono può contenere fino a 17 cifre e può essere seguito da un interno nel formato ;ext= seguito dal numero dell'interno.</p></td>
</tr>
<tr class="even">
<td><p><em>NumberRangeStart</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il primo numero nell'intervallo di numeri non assegnati. Deve essere minore o uguale al valore fornito per NumberRangeEnd.</p>
<p>Questo numero deve corrispondere all'espressione regolare (tel:)?(\+)?[1-9]\d{0,17}(;ext=[1-9]\d{0,9})?. Significa che il numero può iniziare con la stringa tel: (se questa non viene specificata, verrà aggiunta automaticamente), un segno più (+) e una cifra compresa tra 1 e 9. Il numero di telefono può contenere fino a 17 cifre e può essere seguito da un interno nel formato ;ext= seguito dal numero dell'interno.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di eliminare qualsiasi richiesta di conferma altrimenti visualizzata prima di apportare le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>È possibile che gli intervalli di numeri non assegnati si sovrappongono. Se un numero appartiene a più intervalli, viene applicato l'intervallo con la priorità più alta.</p></td>
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

Nessuno.

## Tipi restituiti

Consente di creare un oggetto di tipo Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange.

## Vedere anche

#### Ulteriori risorse

[Remove-CsUnassignedNumber](remove-csunassignednumber.md)  
[Set-CsUnassignedNumber](set-csunassignednumber.md)  
[Get-CsUnassignedNumber](get-csunassignednumber.md)  
[New-CsAnnouncement](new-csannouncement.md)  
[Get-CsAnnouncement](get-csannouncement.md)  
[Get-CsExUmContact](get-csexumcontact.md)

