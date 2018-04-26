---
title: Remove-CsRgsHolidaySet
TOCTitle: Remove-CsRgsHolidaySet
ms:assetid: 6e1f4ec3-2f8a-4ab1-810b-3d64eecd2031
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398521(v=OCS.15)
ms:contentKeyID: 49300911
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsRgsHolidaySet

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un set di festività esistente di Response Group. Un set di festività di Response Group è una raccolta di festività. È ad esempio possibile disporre di un set di festività per una coda per gli Stati Uniti (ovvero un set che può includere la festività del 4 luglio) e un set diverso per una coda per la Francia. Quest'ultima coda può definire una festività per la presa della Bastiglia, ma non per il 4 luglio. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsRgsHolidaySet -Instance <HolidaySet> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 rimuove il set di festività "2010 Holidays" dal servizio ApplicationServer:atl-cs-001.litwareinc.com. A tale scopo, nel comando viene innanzitutto chiamato **Get-CsRgsHolidaySet** con due parametri: il parametro Identity che specifica la posizione del set di festività e il parametro Name che specifica il nome del set. L'oggetto restituito viene quindi inviato tramite pipe a **Remove-CsRgsHolidaySet**, che elimina il set di festività 2010 Holidays.

    Get-CsRgsHolidaySet -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "2010 Holidays" | Remove-CsRgsHolidaySet

## ESEMPIO 2

Nell'esempio 2 vengono eliminati tutti i set di festività nel servizio ApplicationServer:atl-cs-001.litwareinc.com che includono Capodanno (New Year's Day). A tale scopo, nel comando viene innanzitutto utilizzato **Get-CsRgsHolidaySet** per restituire una raccolta di tutti i set di festività trovati nel servizio ApplicationServer:atl-cs-001.litwareinc.com. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Select-Object**, che esegue due operazioni: 1) seleziona la proprietà Identity per ogni set di festività e 2) "espande" il valore della proprietà HolidayList. Quando si espande un valore, vengono restituite le proprietà dell'oggetto sottostante. Nel caso di una festività, si tratta di proprietà come Name, StartDate ed EndDate. Le informazioni selezionate (l'identità dei set di festività e i valori delle proprietà delle festività) vengono quindi inviate tramite pipe al cmdlet **Where-Object**, che seleziona i set che includono una festività il cui nome è uguale a (-eq) "New Year's Day". La raccolta filtrata di set di festività viene quindi inviata tramite pipe a **Remove-CsRgsHolidaySet**, che elimina ogni set di festività che include Capodanno (New Year's Day).

    Get-CsRgsHolidaySet -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com"  | Select-Object Identity -ExpandProperty HolidayList | Where-Object {$_.Name -eq "New Year's Day"}  | Remove-CsRgsHolidaySet 

## ESEMPIO 3

Il comando mostrato nell'esempio 3 elimina dal servizio ApplicationServer:atl-cs-001.litwareinc.com tutti i set di festività a cui sono state assegnate meno di 5 festività. A tale scopo, nel comando viene innanzitutto chiamato **Get-CsRgsHolidaySet** per restituire una raccolta di tutti i set di festività trovati in ApplicationServer:atl-cs-001.litwareinc.com. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i set di festività in cui il numero di festività assegnate ($\_.Holidays.Count) è minore di 5. Tali set di festività vengono quindi inviati tramite pipe al cmdlet **Remove-CsRgsHolidaySet**, che li elimina.

    Get-CsRgsHolidaySet -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com"  | Where-Object {$_.HolidayList.Count -lt 5} | Remove-CsRgsHolidaySet

## Descrizione dettagliata

Allo scopo di garantire ai chiamanti la migliore esperienza di utilizzo possibile, l'applicazione Response Group consente di stabilire chiaramente quando gli agenti di Response Group sono disponibili per rispondere alle chiamate e quando non lo sono. Con l'applicazione Response Group, è infatti possibile definire gli orari d'ufficio, che indicano i giorni della settimana e le ore del giorno in cui gli agenti sono a disposizione per rispondere alle chiamate. Ad esempio, se l'organizzazione è aperta in genere dal lunedì al venerdì dalle 09.00 alle 17.00, sarà possibile configurare gli orari d'ufficio in maniera tale che indichino che gli agenti sono disponibili dal lunedì al venerdì dalle 09.00 alle 17.00 e, di conseguenza, che non sono disponibili il giovedì alle 20.00 o la domenica alle 14.30.

In molte organizzazioni vi sono tuttavia eccezioni alla settimana lavorativa tipica. Negli Stati Uniti ad esempio un'organizzazione può essere chiusa a Natale o durante il Giorno del Ringraziamento. Per gestire tali chiusure atipiche, l'applicazione Response Group consente di designare come festività determinati giorni, ovvero giorni in cui l'organizzazione è di solito aperta ma, per qualche ragione, in questo caso non lo è. Le singole festività (create utilizzando il cmdlet **New-CsRgsHoliday**) sono raccolte in set di festività. Le festività relative agli Stati Uniti ad esempio possono essere raccolte in un set denominato US\_Holidays, mentre le festività relative al Giappone in un set denominato Japanese\_Holidays. Dopo essere state raccolte, le festività e i relativi set possono essere assegnati ai flussi di lavoro di Response Group.

Il cmdlet **Remove-CsRgsHolidaySet** consente agli amministratori di rimuovere set di festività di Response Group. Per impostazione predefinita, se si tenta di rimuovere un set di festività attualmente assegnato a un flusso di lavoro attivo, il cmdlet sospenderà l'operazione e chiederà se si è certi di voler eliminare il flusso di lavoro. Il comando non proseguirà e il set di festività non verrà rimosso finché non si risponde al prompt. Per non visualizzare il prompt e rimuovere un set di festività anche se al momento è utilizzato da un flusso di lavoro attivo, aggiungere il parametro Force:

Get-CsRgsHolidaySet -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "Festività 2010" | Remove-CsRgsHolidaySet –Force

Si noti che, quando si chiama **Remove-CsRgsHolidaySet**, viene rimosso e non è più disponibile per l'utilizzo l'intero set di festività. Se si desidera semplicemente rimuovere una singola festività da un set di festività, ad esempio perché alla fine la propria azienda ha deciso di restare aperta il Giorno del ringraziamento, utilizzare **Set-CsRgsHolidaySet** per rimuovere solo la festività specificata.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsRgsHolidaySet** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsRgsHolidaySet"}

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
<td><p><em>Instance</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.HolidaySet</p></td>
<td><p>Riferimento all'oggetto che punta al set di festività da rimuovere. Quando gli oggetti flusso di lavoro vengono inviati tramite pipe a <strong>Remove-CsRgsHolidaySet</strong>, è possibile omettere il parametro Instance.</p>
<p>Per utilizzare il parametro Instance, sono necessari comandi analoghi al seguente:</p>
<p>$x = Get-CsRgsHolidaySet –Identity ApplicationServer:atl-cs-001.litwareinc.com /1987d3c2-4544-489d-bbe3-59f79f530a83</p>
<p>Remove-CsRgsHolidaySet –Instance $x</p>
<p>Si noti che è possibile rimuovere un solo set di festività alla volta quando si utilizza il parametro Instance. Ciò significa che il riferimento all'oggetto ($x) non può contenere più oggetti set di festività.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Questo parametro è utilizzato solo a scopo di test.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Forza la rimozione del set di festività. Se questo parametro è presente, il set di festività sarà eliminato senza avviso, anche se è utilizzato da un flusso di lavoro attivo. Se questo parametro non è presente, verrà richiesto di confermare l'eliminazione di ogni set di festività attualmente assegnato a un flusso di lavoro attivo.</p></td>
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

Oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.HolidaySet. **Remove-CsRgsHolidaySet** accetta le istanze da pipeline dell'oggetto set di festività di Response Group.

## Tipi restituiti

**Remove-CsRgsHolidaySet** elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.HolidaySet.

## Vedere anche

#### Ulteriori risorse

[Get-CsRgsHolidaySet](get-csrgsholidayset.md)  
[New-CsRgsHolidaySet](new-csrgsholidayset.md)  
[Set-CsRgsHolidaySet](set-csrgsholidayset.md)

