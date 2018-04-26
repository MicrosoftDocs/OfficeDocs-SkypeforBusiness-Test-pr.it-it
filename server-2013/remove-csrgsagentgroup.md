---
title: Remove-CsRgsAgentGroup
TOCTitle: Remove-CsRgsAgentGroup
ms:assetid: dc185da9-0ae0-4f89-8ef8-7cb680d5dc51
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398969(v=OCS.15)
ms:contentKeyID: 49302198
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsRgsAgentGroup

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un gruppo di agenti esistente di Response Group. Un gruppo di agenti è una raccolta di agenti assegnati alla coda di Response Group. Gli agenti sono gli utenti designati per rispondere alle chiamate indirizzate a una coda specifica. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsRgsAgentGroup -Instance <AgentGroup> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 elimina tutti i gruppi di agenti di Response Group configurati per l'utilizzo nel servizio ApplicationServer:atl-cs-001.litwareinc.com. A tale scopo, nel comando viene innanzitutto utilizzato **Get-CsRgsAgentGroup** per restituire tutti i gruppi di agenti per ApplicationServer:atl-cs-001.litwareinc.com. Questi gruppi vengono quindi inviati tramite pipe al cmdlet **Remove-CsRgsAgentGroup**, che li rimuove.

    Get-CsRgsAgentGroup -Identity service:ApplicationServer:atl-cs-001.litwareinc.com | Remove-CsRgsAgentGroup

## ESEMPIO 2

Nell'esempio 2, viene rimosso un gruppo di agenti di Response Group: il gruppo denominato Help Desk. A tale scopo, viene innanzitutto utilizzato **Get-CsRgsAgentGroup** per restituire il gruppo di agenti Help Desk (-Name "Help Desk") da ApplicationServer:atl-cs-001.litwareinc.com. Il gruppo viene quindi inviato tramite pipe a **Remove-CsRgsAgentGroup**, che rimuove il gruppo dal servizio.

    Get-CsRgsAgentGroup -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk" | Remove-CsRgsAgentGroup

## ESEMPIO 3

Nell'esempio 3 vengono eliminati tutti i gruppi di agenti di Response Group in ApplicationServer:atl-cs-001.litwareinc.com che non utilizzano il metodo di routing round robin. A tale scopo, viene innanzitutto chiamato **Get-CsRgsAgentGroup** per restituire una raccolta di tutti i gruppi di agenti trovati nel servizio ApplicationServer:atl-cs-001.litwareinc.com. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i gruppi in cui la proprietà RoutingMethod non è uguale a (-ne) RoundRobin. La raccolta filtrata viene quindi inviata tramite pipe a **Remove-CsRgsAgentGroup**, che elimina ogni elemento presente nella raccolta.

    Get-CsRgsAgentGroup -Identity service:ApplicationServer:atl-cs-001.litwareinc.com | Where-Object {$_.RoutingMethod -ne "RoundRobin"} | Remove-CsRgsAgentGroup

## Descrizione dettagliata

Quando viene chiamato un numero di telefono associato all'applicazione Response Group, il servizio innanzitutto determina quale flusso di lavoro corrisponde al numero chiamato. A seconda della configurazione del flusso di lavoro, la chiamata può essere instradata a un insieme di domande del sistema IVR (Interactive Voice Response), in cui al chiamante vengono poste una o più domande, ad esempio "La domanda riguarda il supporto hardware o software?"). In alternativa, la chiamata può essere inserita in una coda di Response Group, dove il chiamante resterà in attesa finché qualcuno non sarà disponibile per rispondere alla chiamata. Le persone designate a rispondere alle chiamate sono dette agenti, e un gruppo di agenti viene chiamato gruppo di agenti di Response Group. I gruppi di agenti sono associati ai flussi di lavoro, e quindi associati a questo genere di responsabilità; ad esempio, il personale del supporto tecnico può essere raggruppato nel gruppo di agenti Help Desk mentre gli agenti del servizio clienti possono essere raggruppati nel gruppo di agenti Customer Support.

È possibile creare nuovi gruppi di agenti utilizzando il cmdlet **New-CsRgsAgentGroup**. Per eliminare un gruppo di agenti, è possibile chiamare il cmdlet **Remove-CsRgsAgentGroup**. Questo cmdlet elimina l'intero gruppo e quindi tutti gli agenti presenti nel gruppo. Se si desidera rimuovere solo un singolo agente da un gruppo, utilizzare invece il cmdlet **Set-CsRgsAgentGroup**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsRgsAgentGroup** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsRgsAgentGroup"}

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
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.AgentGroup</p></td>
<td><p>Riferimento all'oggetto che punta al gruppo di agenti da rimuovere. Quando gli oggetti flusso di lavoro vengono inviati tramite pipe a <strong>Remove-CsRgsAgentGroup</strong>, è possibile omettere il parametro Instance.</p>
<p>Per utilizzare il parametro Instance, sono necessari comandi analoghi al seguente:</p>
<p>$x = Get-CsRgsAgentGroup –Identity ApplicationServer:atl-cs-001.litwareinc.com /1987d3c2-4544-489d-bbe3-59f79f530a83</p>
<p>Remove-CsRgsAgentGroup –Instance $x</p>
<p>Si noti che è possibile rimuovere un solo gruppo di agenti alla volta quando si utilizza il parametro Instance. Ciò significa che il riferimento all'oggetto ($x) non può contenere più oggetti gruppo di agenti.</p></td>
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
<td><p>Forza la rimozione del gruppo di agenti. Se questo parametro è presente, il gruppo di agenti verrà eliminato senza avviso, anche se è utilizzato da un flusso di lavoro attivo. Se questo parametro non è presente, verrà richiesto di confermare l'eliminazione di qualsiasi gruppo di agenti attualmente utilizzato da un flusso di lavoro attivo.</p></td>
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

Oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.AgentGroup. **Remove-CsRgsAgentGroup** accetta le istanze da pipeline dell'oggetto gruppo di agenti di Response Group.

## Tipi restituiti

**Remove-CsRgsAgentGroup** elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.AgentGroup.

## Vedere anche

#### Ulteriori risorse

[Get-CsRgsAgentGroup](get-csrgsagentgroup.md)  
[New-CsRgsAgentGroup](new-csrgsagentgroup.md)  
[Set-CsRgsAgentGroup](set-csrgsagentgroup.md)

