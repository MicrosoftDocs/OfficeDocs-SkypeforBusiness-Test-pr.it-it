---
title: Get-CsRgsAgentGroup
TOCTitle: Get-CsRgsAgentGroup
ms:assetid: 2e3c7004-9017-48a4-91d8-5c271fb8a1ab
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425793(v=OCS.15)
ms:contentKeyID: 49300049
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsRgsAgentGroup

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui gruppi di agenti di Response Group configurati per l'utilizzo nell'organizzazione. Un gruppo di agenti è una raccolta di agenti assegnati alla coda di Response Group. Gli agenti sono gli utenti designati per rispondere alle chiamate indirizzate a una coda. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsRgsAgentGroup [-Identity <RgsIdentity>] [-Name <String>] [-Owner <RgsIdentity>] [-ShowAll <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituiti tutti i gruppi di agenti di Response Group configurati per l'utilizzo nell'organizzazione. A tale scopo, viene chiamato **Get-CsRgsAgentGroup** senza alcun parametro.

    Get-CsRgsAgentGroup

## ESEMPIO 2

Il comando illustrato nell'esempio 2 restituisce tutti i gruppi di agenti di Response Group configurati per l'utilizzo nel servizio ApplicationServer:atl-cs-001.litwareinc.com.

    Get-CsRgsAgentGroup -Identity service:ApplicationServer:atl-cs-001.litwareinc.com

## ESEMPIO 3

Il comando mostrato nell'esempio 3 restituisce un singolo gruppo di agenti di Response Group, ovvero il gruppo denominato Help Desk, trovato nel servizio ApplicationServer:atl-cs-001.litwareinc.com.

    Get-CsRgsAgentGroup -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"

## ESEMPIO 4

Nell'esempio 4 vengono restituite informazioni per tutti i gruppi di agenti di Response Group nel servizio ApplicationServer:atl-cs-001.litwareinc.com, purché tali gruppi utilizzino il metodo di routing round robin. A tale scopo, nel comando viene innanzitutto utilizzato **Get-CsRgsAgentGroup** per restituire una raccolta di tutti i gruppi di agenti in ApplicationServer:atl-cs-001.litwareinc.com. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i gruppi in cui la proprietà RoutingMethod è uguale a "RoundRobin".

    Get-CsRgsAgentGroup -Identity service:ApplicationServer:atl-cs-001.litwareinc.com | Where-Object {$_.RoutingMethod -eq "RoundRobin"}

## ESEMPIO 5

Il comando utilizzato nell'esempio 5 è una variante di quello dell'esempio 3. In questo caso, vengono però restituite informazioni per tutti i gruppi di agenti di Response Group nel servizio ApplicationServer:atl-cs-001.litwareinc.com che non utilizzano il metodo di routing round robin. A tale scopo, nel comando viene innanzitutto chiamato **Get-CsRgsAgentGroup** per restituire una raccolta di tutti i gruppi di agenti in ApplicationServer:atl-cs-001.litwareinc.com. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i gruppi di agenti in cui la proprietà RoutingMethod non è uguale a "RoundRobin".

    Get-CsRgsAgentGroup -Identity Service:ApplicationServer:atl-cs-001.litwareinc.com | Where-Object {$_.RoutingMethod -ne "RoundRobin"}

## Descrizione dettagliata

Quando viene chiamato un numero di telefono associato all'applicazione Response Group, quest'ultima innanzitutto determina il flusso di lavoro corrispondente al numero di telefono chiamato. A seconda della configurazione del flusso di lavoro, la chiamata può essere instradata a un insieme di domande del sistema IVR (Interactive Voice Response), in cui al chiamante vengono poste una o più domande, ad esempio "La domanda riguarda il supporto hardware o software?"). In alternativa, la chiamata può essere messa in una coda di Response Group; qui il chiamante viene lasciato in attesa finché una persona designata non sia disponibile per rispondere alla chiamata. Le persone designate a rispondere alle chiamate sono dette agenti e un insieme di agenti raccolto viene chiamato gruppo di agenti di Response Group. I gruppi di agenti sono associati ai flussi di lavoro e a questo genere di responsabilità: il personale del supporto tecnico può essere raggruppato nel gruppo di agenti Help Desk, mentre gli agenti del servizio clienti possono essere raggruppati nel gruppo di agenti Customer Support.

Il cmdlet **Get-CsRgsAgentGroup** consente di restituire informazioni sui gruppi di agenti di Response Group attualmente in uso nell'organizzazione, incluse le informazioni sugli utenti assegnati a ciascun gruppo di agenti.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsRgsAgentGroup** i membri dei seguenti gruppi: RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsRgsAgentGroup"}

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
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>Rappresenta l'identità del servizio in cui è ospitato il gruppo di agenti di Response Group o l'identità completa del gruppo di agenti vero e proprio. Se si specifica l'identità di servizio (ad esempio, servizio:ApplicationServer:atl-cs-001.litwareinc.com), tutti i gruppi di agenti ospitati nel servizio saranno restituiti. Se si specifica l'identità del gruppo, verrà restituito solo il gruppo di agenti specificato. L'identità di un gruppo di agenti è costituita dall'identità del servizio seguita da un identificatore univoco globale (GUID), ad esempio service:ApplicationServer:atl-cs-001.litwareinc.com /1987d3c2-4544-489d-bbe3-59f79f530a83.</p>
<p>Un modo alternativo per restituire un singolo gruppo consiste nello specificare l'identità del servizio e nell'includere il parametro Name e il nome del gruppo di agenti. Ciò consente di recuperare un gruppo specifico senza conoscere il GUID assegnato al gruppo stesso.</p>
<p>Se chiamato senza alcun parametro, <strong>Get-CsRgsAgentGroup</strong> restituisce una raccolta di tutti i gruppi di agenti configurati per l'utilizzo nell'organizzazione.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome univoco assegnato al gruppo di agenti nel momento stesso in cui il gruppo è stato creato.</p></td>
</tr>
<tr class="odd">
<td><p><em>Owner</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>Nome di dominio completo del pool &quot;proprietario&quot; del gruppo di agenti. L'ID del pool proprietario e l'ID del pool di un gruppo di agenti in genere coincidono. Se tuttavia è necessario spostare temporaneamente un gruppo, ad esempio in una procedura di ripristino di emergenza, l'ID del pool cambia. L'ID del proprietario invece continuerà a puntare al pool originale.</p></td>
</tr>
<tr class="even">
<td><p><em>ShowAll</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, mostra tutti i gruppi di agenti di Response Group, inclusi quelli in cui l'ID del pool proprietario e l'ID del pool sono diversi. Per impostazione predefinita, Get-CsRgsAgentGroup restituisce informazioni solo sui gruppi di agenti in cui l'ID del pool proprietario e l'ID del pool sono identici.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa. **Get-CsRgsAgentGroup** accetta un valore stringa che rappresenta l'identità del numero di agenti di Response Group.

## Tipi restituiti

**Get-CsRgsAgentGroup** restituisce istanze dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.AgentGroup.

## Vedere anche

#### Ulteriori risorse

[New-CsRgsAgentGroup](new-csrgsagentgroup.md)  
[Remove-CsRgsAgentGroup](remove-csrgsagentgroup.md)  
[Set-CsRgsAgentGroup](set-csrgsagentgroup.md)

