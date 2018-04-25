---
title: Get-CsRgsWorkflow
TOCTitle: Get-CsRgsWorkflow
ms:assetid: 2ae2e10b-65ac-40f9-96a2-5adb01e8a69d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425766(v=OCS.15)
ms:contentKeyID: 49300010
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsRgsWorkflow

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui flussi di lavoro di Response Group. I flussi di lavoro determinano le azioni da eseguire quando l'applicazione Response Group riceve una chiamata telefonica. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsRgsWorkflow [-Identity <RgsIdentity>] [-Name <String>] [-Owner <RgsIdentity>] [-ShowAll <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituite informazioni su tutti i flussi di lavoro configurati per l'utilizzo nell'organizzazione. A tale scopo, viene chiamato **Get-CsRgsWorkflow** senza alcun parametro.

    Get-CsRgsWorkflow

## ESEMPIO 2

Nell'esempio 2 vengono restituite informazioni su tutti i flussi di lavoro dell'applicazione Response Group trovati nel servizio ApplicationServer:atl-cs-001.litwareinc.com.

    Get-CsRgsWorkflow -Identity service:ApplicationServer:atl-cs-001.litwareinc.com

## ESEMPIO 3

Il comando mostrato nell'esempio 3 visualizza informazioni dettagliate sulla proprietà DefaultAction per ogni flusso di lavoro di Response Group trovato nel servizio ApplicationServer:atl-cs-001.litwareinc.com. Per eseguire questa attività, viene innanzitutto utilizzato **Get-CsRgsWorkflow** per restituire informazioni su tutti i flussi di lavoro trovati in ApplicationServer:atl-cs-001.litwareinc.com. Le informazioni vengono quindi inviate tramite pipe al cmdlet **Select-Object**, che espande il valore archiviato nella proprietà DefaultAction. Quando si espande il valore di DefaultAction, sono visibili le singole proprietà dell'oggetto incorporato archiviato nella proprietà DefaultAction.

    Get-CsRgsWorkflow -Identity service:ApplicationServer:atl-cs-001.litwareinc.com | Select-Object -ExpandProperty DefaultAction

## ESEMPIO 4

Nell'esempio 4 vengono restituite informazioni su un singolo flusso di lavoro di Response Group, ovvero il flusso di lavoro European Sales Supports trovato in ApplicationServer:atl-cs-001.litwareinc.com.

    Get-CsRgsWorkflow -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "European Sales Support"

## ESEMPIO 5

Il comando mostrato nell'esempio 5 restituisce informazioni su tutti i flussi di lavoro di Response Group che utilizzano l'inglese americano come lingua principale. A tale scopo, viene innanzitutto chiamato **Get-CsRgsWorkflow** per restituire una raccolta di tutti i flussi di lavoro trovati nel servizio ApplicationServer:atl-cs-001.litwareinc.com. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i flussi di lavoro in cui la proprietà Language è uguale all'inglese americano (en-US).

    Get-CsRgsWorkflow -Identity service:ApplicationServer:atl-cs-001.litwareinc.com | Where-Object {$_.Language -eq "en-Us"}

## ESEMPIO 6

Nell'esempio 6 vengono restituiti tutti i flussi di lavoro presenti in ApplicationServer:atl-cs-001.litwareinc.com la cui proprietà CustomMusicOnHoldFile è stata impostata su un valore Null. In altre parole, il comando restituisce informazioni sui flussi di lavoro a cui non è stata assegnata musica personalizzata. Per ottenere questo risultato, il comando utilizza innanzitutto **Get-CsRgsWorkflow** per restituire una raccolta di tutti i flussi di lavoro trovati nel servizio ApplicationServer:atl-cs-001.litwareinc.com. I dati restituiti vengono quindi inviati tramite pipe a **Where-Object**, che seleziona solo gli elementi in cui la proprietà CustomMusicOnHoldFile è uguale a un valore Null.

    Get-CsRgsWorkflow service:ApplicationServer:atl-cs-001.litwareinc.com | Where-Object {$_.CustomMusicOnHoldFile -eq $Null}

## Descrizione dettagliata

I flussi di lavoro sono forse l'elemento chiave dell'applicazione Response Group. Ciascun flusso di lavoro è associato univocamente a un numero di telefono; quando qualcuno chiama questo numero, il flusso di lavoro determina il modo in cui la chiamata verrà gestita. Ad esempio, la chiamata può essere instradata a una serie di domande del sistema IVR (Interactive Voice Response), mediante cui si avvisa il chiamante che è necessario immettere ulteriori informazioni ("Premere 1 per supporto hardware. Premere 2 per supporto software."). In alternativa, la chiamata può essere messa in una coda e il chiamante può essere lasciato in attesa finché un agente non sia disponibile per rispondere alla chiamata. La disponibilità di agenti che rispondano alle chiamate è determinata anche dal flusso di lavoro: i flussi di lavoro sono utilizzati per configurare sia l'orario di ufficio (i giorni della settimana e le ore del giorno in cui gli agenti sono disponibili per rispondere alle chiamate) sia i periodi di vacanza (giorni in cui non ci sono agenti disponibili per rispondere alle chiamate).

Il cmdlet **Get-CsRgsWorkflow** consente di restituire informazioni sui flussi di lavoro configurati per l'utilizzo nell'organizzazione.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsRgsWorkflow** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsRgsWorkflow"}

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
<td><p>Rappresenta l'identità del servizio in cui è ospitato il flusso di lavoro di Response Group o l'identità piena dello stesso flusso di lavoro. Se si specifica l'identità di un servizio (ad esempio, service: ApplicationServer:atl-cs-001.litwareinc.com), verranno restituiti tutti i flussi di lavoro di Response Group ospitati nel servizio. Se si specifica l'identità di un flusso di lavoro, verrà restituito solo tale flusso di lavoro di Response Group. L'identità di un flusso di lavoro è costituita dall'identità del servizio seguita da un identificatore univoco globale (GUID), ad esempio service:ApplicationServer:atl-cs-001.litwareinc.com /1987d3c2-4544-489d-bbe3-59f79f530a83.</p>
<p>Un modo alternativo per restituire un singolo flusso di lavoro di Response Group consiste nello specificare l'identità del servizio e nell'includere il parametro Name e il nome del flusso di lavoro. Ciò consente di recuperare un flusso di lavoro specifico senza conoscere il GUID assegnato al flusso di lavoro stesso.</p>
<p>Se chiamato senza alcun parametro, <strong>Get-CsRgsWorkflow</strong> restituirà una raccolta di tutti i flussi di lavoro configurati per l'utilizzo nell'organizzazione.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome univoco assegnato al flusso di lavoro di Response Group nel momento stesso in cui il flusso di lavoro è stato creato.</p></td>
</tr>
<tr class="odd">
<td><p><em>Owner</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>Nome di dominio completo del pool &quot;proprietario&quot; del flusso di lavoro. L'ID del pool proprietario e l'ID del pool di un flusso di lavoro in genere coincidono. Se tuttavia è necessario spostare temporaneamente un flusso di lavoro, ad esempio in una procedura di ripristino di emergenza, l'ID del pool cambia. L'ID del proprietario invece continuerà a puntare al pool originale.</p></td>
</tr>
<tr class="even">
<td><p><em>ShowAll</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, mostra tutti i flussi di lavoro di Response Group, inclusi quelli in cui l'ID del pool proprietario e l'ID del pool sono diversi. Per impostazione predefinita, Get-CsRgsWorkflow restituisce solo le informazioni sui flussi di lavoro in cui i pool proprietario e padre sono identici.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. **Get-CsRgsWorkflow** non accetta l'input da pipeline.

## Tipi restituiti

**Get-CsRgsWorkflow** restituisce istanze dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.Workflow.

## Vedere anche

#### Ulteriori risorse

[New-CsRgsWorkflow](new-csrgsworkflow.md)  
[Remove-CsRgsWorkflow](remove-csrgsworkflow.md)  
[Set-CsRgsWorkflow](set-csrgsworkflow.md)

