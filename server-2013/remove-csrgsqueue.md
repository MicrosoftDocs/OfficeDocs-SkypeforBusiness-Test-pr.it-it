---
title: Remove-CsRgsQueue
TOCTitle: Remove-CsRgsQueue
ms:assetid: 7613e72c-f330-4560-88d4-a7386cd18975
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398576(v=OCS.15)
ms:contentKeyID: 49301013
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsRgsQueue

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Elimina una coda esistente di Response Group. Con l'applicazione Response Group, le chiamate telefoniche vengono inserite in una coda e i chiamanti vengono lasciati in attesa finché un agente di Response Group non è disponibile per rispondere alla chiamata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsRgsQueue -Instance <Queue> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 elimina tutte le code di Response Group trovate nel servizio ApplicationServer:atl-cs-001.litwareinc.com. A tale scopo, nel comando viene innanzitutto utilizzato **Get-CsRgsQueue** per restituire una raccolta di tutte le code trovate in ApplicationServer:atl-cs-001.litwareinc.com. Questa raccolta viene quindi inviata tramite pipe a **Remove-CsRgsQueue**, che elimina ogni coda presente nella raccolta.

    Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com | Remove-CsRgsQueue

## ESEMPIO 2

Nell'esempio 2 viene eliminata una singola coda di Response Group, ovvero la coda denominata "Help Desk Queue", trovata nel servizio ApplicationServer:atl-cs-001.litwareinc.com. Per eliminare questa coda, viene chiamato **Get-CsRgsQueue** con i parametri Identity e Name. La singola coda restituita da questa chiamata viene quindi inviata tramite pipe a **Remove-CsRgsQueue**, che la elimina.

    Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk Queue" | Remove-CsRgsQueue

## ESEMPIO 3

Nell'esempio 3 vengono eliminate tutte le code di Response Group trovate nel servizio ApplicationServer:atl-cs-001.litwareinc.com, code la cui proprietà OverflowCandidate è impostata su NewestCall. A tale scopo, viene innanzitutto chiamato **Get-CsRgsQueue** per restituire una raccolta di tutte le code di Response Group trovate in ApplicationServer:atl-cs-001.litwareinc.com. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le code in cui la proprietà OverflowCandidate è uguale a "NewestCall". La raccolta filtrata viene quindi inviata tramite pipe a **Remove-CsRgsQueue**, che elimina ogni coda presente nella raccolta.

    Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com | Where-Object {$_.OverflowCandidate -eq "NewestCall"} | Remove-CsRgsQueue

## Descrizione dettagliata

Quando qualcuno chiama un numero di telefono associato all'applicazione Response Group, in genere avviene quanto segue: la chiamata viene trasferita a una domanda a cui il chiamante deve rispondere per proseguire (ad esempio, "Premere 1 per supporto hardware; premere 2 per supporto software") oppure viene messa in coda finché un agente di Response Group non è disponibile per rispondere.

Invece di avere una singola coda per tutte le chiamate telefoniche, l'applicazione Response Group consente di creare più code che è possibile associare a flussi di lavoro e gruppi di agenti di Response Group diversi. Questo significa che le code possono rispondere diversamente a eventi come ad esempio un determinato numero di chiamate da mettere in coda contemporaneamente o chiamanti lasciati in attesa per un determinato intervallo di tempo.

Oltre a creare nuove code, è possibile rimuovere le code esistenti. Questa è la funzione del cmdlet **Remove-CsRgsQueue**. Per impostazione predefinita, se si tenta di rimuovere una coda attualmente assegnata a un flusso di lavoro attivo, verrà visualizzato un prompt. In tale prompt verrà richiesto di confermare se si desidera eliminare la coda e Windows PowerShell verrà sospeso senza eliminare alcuna coda finché non si risponde al prompt. Per non visualizzare il prompt ed eliminare le code utilizzate da un flusso di lavoro attivo, aggiungere il parametro Force. Ad esempio:

Get-CsRgsQueue –Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" | Remove-CsRgsQueue –Force

**Remove-CsRgsQueue** verifica sempre se una coda viene utilizzata da un flusso di lavoro attivo prima di eliminarla. Non verifica però se la coda viene utilizzata da un'altra coda, ad esempio di timeout o di overflow. Potrebbe perciò accadere di eliminare una coda necessaria a un'altra coda. È pertanto consigliabile utilizzare il cmdlet **Get-CsRgsQueue** per verificare le proprietà OverflowAction e TimeoutAction delle altre code di Response Group prima di eseguire **Remove-CsRgsQueue** per eliminare una coda.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsRgsQueue** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsRgsQueue"}

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
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.Queue</p></td>
<td><p>Riferimento all'oggetto che punta alla coda da rimuovere. Quando gli oggetti flusso di lavoro vengono inviati tramite pipe a <strong>Remove-CsRgsQueue</strong>, è possibile omettere il parametro Instance.</p>
<p>Per utilizzare il parametro Instance, sono necessari comandi analoghi al seguente:</p>
<p>$x = Get-CsRgsQueue –Identity ApplicationServer:atl-cs-001.litwareinc.com /1987d3c2-4544-489d-bbe3-59f79f530a83</p>
<p>Remove-CsRgsQueue –Instance $x</p>
<p>Si noti che è possibile rimuovere una sola coda alla volta quando si utilizza il parametro Instance. Ciò significa che il riferimento all'oggetto ($x) non può contenere più oggetti coda.</p></td>
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
<td><p>Forza l'eliminazione di una coda di Response Group. Se questo parametro è presente, la coda verrà eliminata senza avviso, anche se è assegnata a un flusso di lavoro attivo. Se questo parametro non è presente, verrà richiesto di confermare l'eliminazione di qualsiasi coda attualmente utilizzata da un flusso di lavoro attivo.</p></td>
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

Oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.Queue. **Remove-CsRgsQueue** accetta le istanze da pipeline dell'oggetto coda di Response Group.

## Tipi restituiti

**Remove-CsRgsQueue** elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.Queue.

## Vedere anche

#### Ulteriori risorse

[Get-CsRgsQueue](get-csrgsqueue.md)  
[New-CsRgsQueue](new-csrgsqueue.md)  
[Set-CsRgsQueue](set-csrgsqueue.md)

