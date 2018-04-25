---
title: Remove-CsRgsWorkflow
TOCTitle: Remove-CsRgsWorkflow
ms:assetid: 9626df55-e3ed-478a-a485-f2a9abcf493b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398765(v=OCS.15)
ms:contentKeyID: 49301397
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsRgsWorkflow

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Elimina un flusso di lavoro esistente di Response Group. I flussi di lavoro determinano le azioni da eseguire quando l'applicazione Response Group riceve una chiamata telefonica. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsRgsWorkflow -Instance <Workflow> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

L'esempio 1 rimuove tutti i flussi di lavoro di Response Group dal servizio ApplicationServer:atl-cs-001.litwareinc.com. A tale scopo, nel comando viene innanzitutto chiamato **Get-CsRgsWorkflow** per restituire una raccolta di tutti i flussi di lavoro trovati in ApplicationServer:atl-cs-001.litwareinc.com. Questa raccolta viene quindi inviata tramite pipe a **Remove-CsRgsWorkflow**, che elimina ogni flusso di lavoro presente nella raccolta.

    Get-CsRgsWorkflow -Identity Service:ApplicationServer:atl-cs-001.litwareinc.com | Remove-CsRgsWorkflow

## ESEMPIO 2

Il comando mostrato nell'esempio 2 elimina un singolo flusso di lavoro di Response Group: il flusso di lavoro denominato "Help Desk Workflow", posizionato nel servizio ApplicationServer:atl-cs-001.litwareinc.com. A tale scopo, viene innanzitutto utilizzato **Get-CsRgsWorkflow** per restituire il flusso di lavoro denominato Help Desk Workflow dal servizio ApplicationServer:atl-cs-001.litwareinc.com. Il flusso di lavoro viene quindi inviato tramite pipe a **Remove-CsRgsWorkflow**, che lo elimina.

    Get-CsRgsWorkflow service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk Workflow" | Remove-CsRgsWorkflow

## ESEMPIO 3

Nell'esempio 3 vengono eliminati tutti i flussi di lavoro relativi all'inglese americano dal servizio ApplicationServer:atl-cs-001.litwareinc.com. A tale scopo, viene innanzitutto utilizzato **Get-CsRgsWorkflow** per recuperare tutti i flussi di lavoro trovati in ApplicationServer:atl-cs-001.litwareinc.com. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i flussi di lavoro in cui la lingua è uguale all'inglese americano (en-us). La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsRgsWorkflow**, che elimina ogni elemento presente nella raccolta.

    Get-CsRgsWorkflow service:ApplicationServer:atl-cs-001.litwareinc.com | Where-Object {$_.Language -eq "en-us"} | Remove-CsRgsWorkflow

## ESEMPIO 4

Il comando mostrato nell'esempio 4 elimina tutti i flussi di lavoro di Response Group contenuti nel servizio ApplicationServer:atl-cs-001.litwareinc.com che hanno un valore configurato per la proprietà CustomMusicOnHoldFile. A tale scopo, nel comando viene innanzitutto utilizzato **Get-CsRgsWorkflow** per restituire una raccolta di tutti i flussi di lavoro trovati in ApplicationServer:atl-cs-001.litwareinc.com. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i flussi di lavoro in cui la proprietà CustomMusicOnHoldFile non è uguale a un valore Null. Se la proprietà non è uguale a un valore Null, significa che per questo flusso di lavoro è stata definita una musica personalizzata. La raccolta filtrata viene quindi inviata tramite pipe a **Remove-CsRgsWorkflow**, che rimuove ogni elemento presente nella raccolta.

    Get-CsRgsWorkflow service:ApplicationServer:atl-cs-001.litwareinc.com | Where-Object {$_.CustomMusicOnHoldFile -ne $Null} | Remove-CsRgsWorkflow

## Descrizione dettagliata

I flussi di lavoro sono un elemento chiave dell'applicazione Response Group. Ciascun flusso di lavoro è associato univocamente a un numero di telefono; quando qualcuno chiama questo numero, il flusso di lavoro determina il modo in cui la chiamata verrà gestita. Ad esempio, la chiamata può essere instradata a una serie di domande del sistema IVR (Interactive Voice Response), mediante cui si avvisa il chiamante che è necessario immettere ulteriori informazioni ("Premere 1 per supporto hardware. Premere 2 per supporto software.") In alternativa, la chiamata può essere messa in una coda e il chiamante può essere lasciato in attesa finché un agente non sia disponibile per rispondere alla chiamata. La disponibilità di agenti che rispondano alle chiamate è determinata anche dal flusso di lavoro: i flussi di lavoro sono utilizzati per mantenere sia l'orario di ufficio (i giorni della settimana e le ore del giorno in cui gli agenti sono disponibili per rispondere alle chiamate) sia i periodi di vacanza (giorni in cui non ci sono agenti disponibili per rispondere alle chiamate).

È possibile creare nuovi flussi di lavoro utilizzando il cmdlet **New-CsRgsWorkflow**. Dopo che tali flussi di lavoro sono stati creati, è possibile eliminarli successivamente tramite **Remove-CsRgsWorkflow**. Si noti che, quando si elimina un flusso di lavoro, questo viene completamente rimosso dall'applicazione Response Group. Se si desidera disabilitare temporaneamente un flusso di lavoro, non utilizzare **Remove-CsRgsWorkflow**. Utilizzare invece il cmdlet **Set-CsRgsWorkflow** per disabilitare e quindi riabilitare più tardi il flusso di lavoro.

Se si tenta di eliminare un flusso di lavoro attivo, **Remove-CsRgsWorkflow** richiederà di confermare che si desidera effettivamente eliminare il flusso di lavoro. **Remove-CsRgsWorkflow** non eseguirà altre operazioni finché non si risponde al prompt. Per non visualizzare il prompt ed eliminare direttamente un flusso di lavoro attivo, utilizzare il parametro Force. Ad esempio:

Get-CsRgsWorkflow –Identity "service:ApplicationServer:atl-cs-001.litwareinc.com " | Remove-CsRgsWorkflow –Force

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsRgsWorkflow** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsRgsWorkflow"}

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
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.Workflow</p></td>
<td><p>Riferimento oggetto che punta al flusso di lavoro da rimuovere. Quando gli oggetti flusso di lavoro vengono inviati tramite pipe a <strong>Remove-CsRgsWorkflow</strong>, è possibile omettere il parametro Instance.</p>
<p>Per utilizzare il parametro Instance, sono necessari comandi analoghi al seguente:</p>
<p>$x = Get-CsRgsWorkflow –Identity ApplicationServer:atl-cs-001.litwareinc.com /1987d3c2-4544-489d-bbe3-59f79f530a83</p>
<p>Remove-CsRgsWorkflow –Instance $x</p>
<p>Si noti che è possibile rimuovere un solo flusso di lavoro alla volta quando si utilizza il parametro Instance. Ciò significa che il riferimento oggetto ($x) non può contenere più oggetti flusso di lavoro.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Forza la rimozione del flusso di lavoro. Se questo parametro è presente, il flusso di lavoro sarà eliminato senza avviso, anche se è attualmente attivo. Se questo parametro non è presente, verrà richiesto di confermare l'eliminazione di ogni flusso di lavoro attivo.</p></td>
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

Oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.Workflow**. Remove-CsRgsWorkflow** accetta le istanze da pipeline dell'oggetto flusso di lavoro di Response Group.

## Tipi restituiti

**Remove-CsRgsWorkflow** elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.Workflow.

## Vedere anche

#### Ulteriori risorse

[Get-CsRgsWorkflow](get-csrgsworkflow.md)  
[New-CsRgsWorkflow](new-csrgsworkflow.md)  
[Set-CsRgsWorkflow](set-csrgsworkflow.md)

