---
title: Set-CsRgsAgentGroup
TOCTitle: Set-CsRgsAgentGroup
ms:assetid: 48944530-29ec-4f5d-893f-37d3fd4aeb66
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425955(v=OCS.15)
ms:contentKeyID: 49300406
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsRgsAgentGroup

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un gruppo di agenti esistente di Response Group. Un gruppo di agenti è una raccolta di agenti assegnati alla coda di Response Group. Gli agenti sono gli utenti designati per rispondere alle chiamate indirizzate a una coda specifica. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsRgsAgentGroup -Instance <AgentGroup> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

I comandi mostrati nell'esempio 1 modificano la proprietà RoutingMethod del gruppo di agenti di Response Group denominato Help Desk e trovato nel servizio ApplicationServer:atl-cs-001.litwareinc.com. Per eseguire questa attività, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsRgsAgentGroup** per recuperare il gruppo di agenti Help Desk (-Name "Help Desk") da ApplicationServer:atl-cs-001.litwareinc.com. Dopo il recupero, l'oggetto del gruppo di agenti viene archiviato in una variabile denominata $x.

Il secondo comando dell'esempio modifica il valore della proprietà RoutingMethod. Nel comando finale dell'esempio viene utilizzato il cmdlet **Set-CsRgsAgentGroup** per scrivere le modifiche nel gruppo di agenti Help Desk effettivo.

    $x = Get-CsRgsAgentGroup -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    $x.RoutingMethod = "RoundRobin"
    Set-CsRgsAgentGroup -Instance $x

## ESEMPIO 2

L'esempio 2 mostra come modificare il gruppo di distribuzione assegnato al gruppo di agenti di Response Group. A tale scopo, viene innanzitutto utilizzato **Get-CsRgsAgentGroup** per restituire il gruppo di agenti da modificare. In questo esempio si tratta del gruppo Help Desk (-Name "Help Desk") trovato nel servizio ApplicationServer:atl-cs-001.litwareinc.com. Dopo che **Get-CsRgsAgentGroup** restituisce tale gruppo, l'oggetto risultante viene archiviato in una variabile denominata $x.

Il secondo comando nell'esempio assegna un nuovo valore (helpdesk@litwareinc.com) alla proprietà DistributionGroupAddress. Dopo l'assegnazione del nuovo valore, viene quindi utilizzato **Set-CsRgsAgentGroup** per scrivere le modifiche nel gruppo di agenti Help Desk in ApplicationServer:atl-cs-001.litwareinc.com.

    $x = Get-CsRgsAgentGroup -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    $x.DistributionGroupAddress = "helpdesk@litwareinc.com"
    Set-CsRgsAgentGroup -Instance $x

## ESEMPIO 3

I comandi mostrati nell'esempio 3 aggiungono un nuovo agente al gruppo di agenti Help Desk di Response Group. A tale scopo, nell'esempio viene innanzitutto utilizzato **Get-CsRgsAgentGroup** per restituire il gruppo Help Desk (-Name "Help Desk") dal servizio ApplicationServer:atl-cs-001.litwareinc.com. L'oggetto recuperato viene archiviato in una variabile denominata $x.

Nel secondo comando, il metodo Aggiungi viene utilizzato per aggiungere un nuovo agente alla proprietà AgentsByUri; ciò avviene specificando l'indirizzo SIP del nuovo agente ("sip:kenmyer@litwareinc.com"). Nel terzo comando viene utilizzato **Set-CsRgsAgentGroup** per scrivere le modifiche, ovvero l'aggiunta del nuovo agente, nel gruppo Help Desk. Si noti che, se **Set-CsRgsAgentGroup** non viene chiamato, le modifiche verranno apportate solo in memoria e non verranno applicate al gruppo di agenti effettivo.

    $x = Get-CsRgsAgentGroup -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    $x.AgentsByUri.Add("sip:kenmyer@litwareinc.com")
    Set-CsRgsAgentGroup -Instance $x

## ESEMPIO 4

Nell'esempio 4, un agente viene rimosso dal gruppo di agenti Help Desk di Response Group trovato nel servizio ApplicationServer:atl-cs-001.litwareinc.com. A tale scopo, nell'esempio viene innanzitutto utilizzato **Get-CsRgsAgentGroup** per restituire il gruppo Help Desk (-Name "Help Desk") da ApplicationServer:atl-cs-001.litwareinc.com. L'oggetto del gruppo di agenti recuperato viene archiviato in una variabile denominata $x.

Dopo che il gruppo di agenti è stato recuperato, il metodo Rimuovi viene utilizzato per rimuovere un agente (l'agente con l'indirizzo SIP "sip:kenmyer@litwareinc.com") dal gruppo. Nel terzo comando viene quindi chiamato **Set-CsRgsAgentGroup** per scrivere le modifiche, ovvero per rimuovere l'agente dal gruppo. Se **Set-CsRgsAgentGroup** non viene chiamato, le modifiche verranno apportate solo in memoria e non verranno applicate al gruppo di agenti effettivo. L'agente verrà rimosso soltanto se viene chiamato **Set-CsRgsAgentGroup**.

    $x = Get-CsRgsAgentGroup -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    $x.AgentsByUri.Remove("sip:kenmyer@litwareinc.com")
    Set-CsRgsAgentGroup -Instance $x

## Descrizione dettagliata

Quando viene chiamato un numero di telefono associato all'applicazione Response Group, il servizio innanzitutto determina quale flusso di lavoro corrisponde al numero di telefono chiamato. A seconda della configurazione del flusso di lavoro, la chiamata può essere instradata a un insieme di domande del sistema IVR (Interactive Voice Response), in cui al chiamante vengono poste una o più domande, ad esempio "La domanda riguarda il supporto hardware o software?"). In alternativa, la chiamata può essere inserita in una coda di Response Group, dove il chiamante verrà lasciato in attesa finché una persona designata non sarà disponibile per rispondere alla chiamata. Le persone designate a rispondere alle chiamate sono dette agenti, e un gruppo di agenti viene chiamato gruppo di agenti di Response Group. I gruppi di agenti sono associati ai flussi di lavoro nonché a questo genere di responsabilità: il personale del supporto tecnico può essere raggruppato nel gruppo di agenti Help Desk, mentre gli agenti del servizio clienti possono essere raggruppati nel gruppo di agenti Customer Support.

È possibile creare nuovi gruppi di agenti utilizzando il cmdlet **New-CsRgsAgentGroup**. Se si desidera modificare un gruppo di agenti dopo averlo creato, utilizzare il cmdlet **Set-RgsAgentGroup**. Tra l'altro, questo cmdlet può essere utilizzato per aggiungere e rimuovere singoli agenti da un gruppo. Si noti che **Set-CsRgsAgentGroup** non modifica direttamente le proprietà di un gruppo di agenti. Se si desidera modificare un gruppo, è necessario innanzitutto creare un riferimento oggetto al gruppo. A tale scopo, chiamare **Get-CsRgsAgentGroup** per recuperare il gruppo e quindi archiviare in una variabile l'oggetto restituito. Dopo la creazione del riferimento oggetto, si modificano le proprietà del gruppo in memoria. Al termine delle modifiche, è quindi necessario chiamare **Set-CsRgsAgentGroup** per scriverle nel gruppo di agenti effettivo di Response Group. Se **Set-CsRgsAgentGroup** non viene chiamato, le modifiche esisteranno solo in memoria e scompariranno non appena si chiuderà Windows PowerShell o si eliminerà la variabile del riferimento oggetto.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsRgsAgentGroup** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsRgsAgentGroup"}

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
<td><p>Riferimento oggetto al gruppo di agenti di Response Group Service da modificare. Un riferimento oggetto in genere viene recuperato utilizzando il cmdlet <strong>Get-CsRgsAgentGroup</strong> e assegnando il valore restituito a una variabile. Questo comando ad esempio restituisce un riferimento oggetto al gruppo di agenti Help Desk e archivia tale riferimento in una variabile denominata $x:</p>
<p>$x = Get-CsRgsAgentGroup -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name &quot;Help Desk &quot;</p>
<p></p></td>
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

Oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.AgentGroup. **Set-CsRgsAgentGroup** accetta le istanze da pipeline dell'oggetto gruppo di agenti di Response Group.

## Tipi restituiti

**Set-CsRgsAgentGroup** non restituisce alcun oggetto o valore. Invece, il cmdlet modifica istanze esistenti dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.AgentGroup.

## Vedere anche

#### Ulteriori risorse

[Get-CsRgsAgentGroup](get-csrgsagentgroup.md)  
[New-CsRgsAgentGroup](new-csrgsagentgroup.md)  
[Remove-CsRgsAgentGroup](remove-csrgsagentgroup.md)

