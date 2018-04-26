---
title: Set-CsRgsQueue
TOCTitle: Set-CsRgsQueue
ms:assetid: c1656757-c1d9-4e63-947d-99bd331da210
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412947(v=OCS.15)
ms:contentKeyID: 49301881
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsRgsQueue

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una coda esistente di Response Group. Con l'applicazione Response Group, le chiamate telefoniche vengono inserite in una coda e i chiamanti vengono lasciati in attesa finché un agente di Response Group non è disponibile per rispondere alla chiamata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsRgsQueue -Instance <Queue> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 la proprietà OverflowCandidate viene modificata per la coda Help Desk di Response Group, trovata nel servizio ApplicationServer:atl-cs-001.litwareinc.com. A tale scopo, nel primo comando dell'esempio viene utilizzato **Get-CsRgsQueue** per recuperare la coda specificata (-Name "Help Desk") da ApplicationServer:atl-cs-001.litwareinc.com. La coda recuperata viene quindi archiviata in una variabile denominata $x.

Dopo che la coda è stata recuperata, il secondo comando nell'esempio imposta il valore della proprietà OverflowCandidate di questa coda virtuale su NewestCall. Al termine dell'esecuzione di questo comando, nel comando finale dell'esempio viene utilizzato **Set-CsRgsQueue** per scrivere queste modifiche nella coda Help Desk effettiva. Si noti che, fino a questo punto, le modifiche sono state effettuate solo in memoria. Finché non viene chiamato **Set-CsRgsQueue**, la coda di Response Group effettiva in ApplicationServer:atl-cs-001.litwareinc.com non verrà modificata.

    $x = Get-CsRgsQueue -Identity Service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    $x.OverflowCandidate = "NewestCall"
    Set-CsRgsQueue -Instance $x

## ESEMPIO 2

I comandi mostrati nell'esempio 2 illustrano come creare una nuova azione di chiamata di Response Group e assegnano quindi l'azione alla coda esistente di Response Group. Per eseguire questa attività, il primo passaggio consiste nell'utilizzare **Get-CsRgsQueue** per recuperare la coda di Response Group Help Desk Overflow Queue da ApplicationServer:atl-cs-001.litwareinc.com. Le informazioni da questa coda vengono quindi archiviate in una variabile denominata $x.

Una volta recuperata la coda, viene utilizzato il cmdlet **New-CsRgsPrompt** per creare un prompt di sintesi vocale, che viene archiviato in una variabile denominata $w. Viene quindi utilizzato il cmdlet, **New-CsRgsCallAction** per creare una nuova azione di chiamata. L'azione di chiamata viene assegnata a tre parametri: Prompt che corrisponde al prompt utilizzato dall'azione di chiamata, Action che indica che cosa accade se la nuova azione di chiamata viene attivata (il valore TransferToQueue indica che la chiamata verrà trasferita a una coda di Response Group diversa) e QueueID che indica la coda alternativa a cui verrà trasferita la chiamata ($x.Identity, che rappresenta l'identità della coda Help Desk Overflow Queue). La nuova azione di chiamata viene creata in memoria e archiviata nella variabile denominata $y.

Il comando successivo recupera la coda da modificare. In questo esempio, si tratta della coda Help Desk in ApplicationServer:atl-cs-001.litwareinc.com. Dopo che Get-CsRgsQueue restituisce questo gruppo, l'oggetto coda viene archiviato in una variabile denominata $z.

Al termine, è possibile assegnare la nuova azione di chiamata alla coda Help Desk. A tale scopo, impostare il valore della proprietà OverflowAction su $y, la variabile che contiene l'azione di chiamata appena creata.

Dopo che l'azione di chiamata è stata assegnata, nel comando finale dell'esempio viene chiamato **Set-CsRgsQueue** per scrivere le modifiche nell'istanza effettiva della coda Help Desk in ApplicationServer:atl-cs-001.litwareinc.com.

    $x = Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk Overflow Queue"
    $w = New-CsRgsPrompt -TextToSpeechPrompt "Please hold while we transfer your call."
    $y = New-CsRgsCallAction -Prompt $w -Action TransferToQueue -QueueID $x.Identity
    $z = Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    $z.OverflowAction = $y
    Set-CsRgsQueue -Instance $z

## Descrizione dettagliata

Quando qualcuno chiama un numero di telefono associato all'applicazione Response Group, in genere avviene quanto segue: la chiamata viene trasferita a una domanda a cui il chiamante deve rispondere per continuare (ad esempio, "Premere 1 per supporto hardware; premere 2 per supporto software") oppure viene messa in coda finché l'agente non è disponibile per rispondere.

Invece di avere una singola coda per tutte le chiamate telefoniche, l'applicazione Response Group consente di creare più code che è possibile associare a flussi di lavoro e gruppi di agenti di Response Group diversi. A loro volta, le code possono rispondere diversamente ad eventi come il numero X di chiamate da mettere simultaneamente in coda, o ai chiamanti messi in attesa per un determinato numero di secondi.

Il cmdlet **Set-CsRgsQueue** consente di modificare una coda esistente di Response Group. **Set-CsRgsQueue** non consente però di modificare direttamente la coda. Ad esempio, il cmdlet non include parametri per modificare la soglia o l'azione di overflow. Se si desidera modificare una coda, è innanzitutto necessario creare un riferimento oggetto alla coda stessa utilizzando **Get-CsRgsQueue** per recuperare la coda a cui si è interessati e quindi archiviare tale coda in una variabile. Le modifiche alla coda sono quindi eseguite in memoria assegnando nuovi valori alle proprietà della coda. Dopo aver apportato tutte le modifiche, chiamare **Set-CsRgsQueue** per scrivere le modifiche nella coda di Response Group effettiva. Se **Set-CsRgsQueue** non viene chiamato, le modifiche verranno apportate solo in memoria e scompariranno non appena si chiuderà Windows PowerShell o si eliminerà la variabile del riferimento oggetto.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsRgsQueue** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsRgsQueue"}

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
<td><p>Riferimento oggetto alla coda di Response Group da modificare. Un riferimento oggetto in genere viene recuperato utilizzando il cmdlet <strong>Get-CsRgsQueue</strong> e assegnando il valore restituito a una variabile. Questo comando ad esempio restituisce un riferimento oggetto alla coda Help Desk e archivia tale riferimento in una variabile denominata $x:</p>
<p>$x = Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name &quot;Help Desk&quot;</p></td>
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
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
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

Oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.Queue. **Set-CsRgsQueue** accetta le istanze da pipeline dell'oggetto coda di Response Group.

## Tipi restituiti

**Set-CsRgsQueue** non restituisce alcun oggetto o valore. Invece, il cmdlet modifica istanze esistenti dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.Queue.

## Vedere anche

#### Ulteriori risorse

[Get-CsRgsQueue](get-csrgsqueue.md)  
[New-CsRgsQueue](new-csrgsqueue.md)  
[Remove-CsRgsQueue](remove-csrgsqueue.md)

