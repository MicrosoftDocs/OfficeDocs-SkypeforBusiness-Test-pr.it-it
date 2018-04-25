---
title: New-CsRgsQueue
TOCTitle: New-CsRgsQueue
ms:assetid: e013533b-6845-44c6-ae5e-e75187b43181
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398989(v=OCS.15)
ms:contentKeyID: 49302229
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRgsQueue

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova coda di Response Group. Con l'applicazione Response Group, le chiamate telefoniche vengono inserite in una coda e i chiamanti vengono lasciati in attesa finché un agente di Response Group non è disponibile per rispondere alla chiamata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsRgsQueue -Name <String> -Parent <RgsIdentity> [-AgentGroupIDList <Collection>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-OverflowAction <CallAction>] [-OverflowCandidate <NewestCall | OldestCall>] [-OverflowThreshold <Int16>] [-TimeoutAction <CallAction>] [-TimeoutThreshold <Int32>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene creata una nuova coda di Response Group per il servizio ApplicationServer:atl-cs-001.litwareinc.com. Nel primo comando dell'esempio viene utilizzato **New-CsRgsCallAction** per creare un'azione di chiamata per la coda. In questo esempio ogni volta che viene superata la soglia di overflow, le chiamate vengono trasferite automaticamente alla segreteria telefonica. Questa condizione viene configurata impostando il parametro Action su TransferToVoicemailUri e la proprietà URI sull'URI SIP della segreteria telefonica "sip:+14255551298@litwareinc.com".

Una volta che l'azione di chiamata è stata configurata e archiviata nella variabile $x, viene quindi utilizzato **New-CsRgsQueue** per creare una nuova coda denominata Help Desk. Oltre a specificare l'oggetto OverflowAction, questo comando configura i valori per le proprietà OverflowCandidate e OverflowThreshold.

    $x = New-CsRgsCallAction -Action TransferToVoicemailUri -Uri "sip:+14255551298@litwareinc.com"
    
    New-CsRgsQueue -Parent service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk" -OverflowCandidate "OldestCall" -OverflowAction $x -OverflowThreshold 25

## Descrizione dettagliata

Quando qualcuno chiama un numero di telefono associato all'applicazione Response Group, in genere avviene quanto segue: la chiamata viene trasferita a una domanda a cui il chiamante deve rispondere per continuare (ad esempio, "Premere 1 per supporto hardware; premere 2 per supporto software") oppure viene messa in coda finché l'agente non è disponibile per rispondere.

Invece di avere una singola coda per tutte le chiamate telefoniche, l'applicazione Response Group consente di creare più code che è possibile associare a flussi di lavoro e gruppi di agenti di Response Group diversi. Questo significa che le code possono rispondere diversamente a eventi come ad esempio un determinato numero di chiamate da mettere in coda contemporaneamente o chiamanti lasciati in attesa per un determinato intervallo di tempo.

Il cmdlet **New-CsRgsQueue** consente agli amministratori di creare facilmente nuove code di Reponse Group.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsRgsQueue** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRgsQueue"}

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
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome univoco da assegnare alla coda. La combinazione della proprietà Parent e della proprietà Name consente di identificare in modo univoco le code di Response Group senza dover fare riferimento al relativo identificatore univoco globale (GUID).</p></td>
</tr>
<tr class="even">
<td><p><em>Parent</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>Servizio in cui sarà ospitata la nuova coda. Ad esempio: -Parent &quot;service:ApplicationServer:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>AgentGroupIDList</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Collections.ObjectModel.Collection</p></td>
<td><p>Identità dei gruppi di agenti di Response Group da aggiungere alla coda. Le identità dei gruppi di agenti possono essere recuperate utilizzando il cmdlet <strong>Get-CsRgsAgentGroup</strong>. Per informazioni dettagliate, vedere la sezione relativa agli esempi in questo argomento.</p>
<p>Se una chiamata viene instradata a una coda a cui non è assegnato alcun gruppo di agenti o a cui sono assegnati gruppi di agenti vuoti, la chiamata verrà disconnessa automaticamente.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire informazioni aggiuntive sulla coda di Response Group.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>OverflowAction</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.CallAction</p></td>
<td><p>Azione da eseguire se viene raggiunta la soglia di overflow. L'oggetto OverflowAction deve essere creato utilizzando il cmdlet <strong>New-CsRgsCallAction</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>OverflowCandidate</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.OverflowCandidate</p></td>
<td><p>Indica su quale chiamata agire quando si raggiunge la soglia di overflow. La proprietà OverflowCandidate deve essere impostata su uno dei seguenti valori:</p>
<p>NewestCall</p>
<p>OldestCall</p>
<p>Il valore predefinito è NewestCall.</p></td>
</tr>
<tr class="even">
<td><p><em>OverflowThreshold</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int16</p></td>
<td><p>Numero di chiamate simultanee che possono restare in coda prima che venga attivata l'azione di overflow. L'OverflowThreshold può essere un valore intero compreso tra 0 e 1000 inclusi. Il valore predefinito è NULL, il che significa che in una coda può essere presente simultaneamente un numero illimitato di chiamate.</p></td>
</tr>
<tr class="odd">
<td><p><em>TimeoutAction</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.CallAction</p></td>
<td><p>Azione da eseguire se viene raggiunta la soglia di timeout. L'oggetto TimeoutAction deve essere creato utilizzando il cmdlet <strong>New-CsRgsCallAction</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>TimeoutThreshold</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Quantità di tempo (in secondi) durante la quale una chiamata può restare nella coda prima che si verifichi il relativo timeout. A questo punto, il sistema eseguirà l'azione specificata dal parametro TimeoutAction.</p>
<p>La soglia di timeout può essere un valore intero compreso tra 10 e 65535 secondi (circa 18 ore) inclusi; il valore predefinito è NULL, il che significa che non c'è timeout relativo alla chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. **New-CsRgsQueue** non accetta l'input da pipeline.

## Tipi restituiti

**New-CsRgsQueue** crea nuove istanze dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.Queue.

## Vedere anche

#### Ulteriori risorse

[Get-CsRgsQueue](get-csrgsqueue.md)  
[Remove-CsRgsQueue](remove-csrgsqueue.md)  
[Set-CsRgsQueue](set-csrgsqueue.md)

