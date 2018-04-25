---
title: Set-CsRgsWorkflow
TOCTitle: Set-CsRgsWorkflow
ms:assetid: 36cffa89-e5bb-48fd-bd6e-da67066fd273
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425845(v=OCS.15)
ms:contentKeyID: 49300168
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsRgsWorkflow

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un flusso di lavoro esistente di Response Group. I flussi di lavoro determinano le azioni da eseguire quando l'applicazione Response Group riceve una chiamata telefonica. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsRgsWorkflow -Instance <Workflow> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

I comandi mostrati nell'esempio 1 recuperano un insieme esistente di orari d'ufficio e assegnano tali orari a un flusso di lavoro denominato Help Desk. A tale scopo, nel primo comando dell'esempio viene utilizzato **Get-CsRgsHoursOfBusiness** per recuperare la raccolta di orari d'ufficio denominata US Business Hours dal servizio ApplicationServer:atl-cs-001.litwareinc.com. Gli orari d'ufficio vengono memorizzati in una variabile denominata $businessHours.

Dopo avere recuperato gli orari d'ufficio, viene utilizzato il cmdlet **Get-CsRgsWorkflow** per recuperare il flusso di lavoro Help Desk da ApplicationServer:atl-cs-001.litwareinc.com. L'oggetto viene archiviato in una variabile denominata $y.

Nel terzo comando dell'esempio la proprietà BusinessHoursId del flusso di lavoro Help Desk viene impostata sulla raccolta di orari d'ufficio recuperata. A tale scopo, il parametro BusinessHoursID viene impostato sull'identità della raccolta recuperata ($businessHours.Identity). Nel comando finale viene utilizzato **Set-CsRgsWorkflow** per scrivere i nuovi orari d'ufficio nel flusso di lavoro Help Desk effettivo in ApplicationServer:atl-cs-001.litwareinc.com. Questo ultimo passaggio è importante perché finora tutte le modifiche sono state apportate solo in memoria. Per salvare le modifiche nel flusso di lavoro Help Desk, è necessario chiamare **Set-CsRgsWorkflow**, passando al cmdlet il riferimento oggetto ($y) contenente la copia virtuale del flusso di lavoro.

    $businessHours = Get-CsRgsHoursOfBusiness service:ApplicationServer:atl-cs-001.litwareinc.com -Name "US Business Hours"
    $y = Get-CsRgsWorkflow Service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    $y.BusinessHoursId = $businessHours.Identity
    Set-CsRgsWorkflow -Instance $y

## ESEMPIO 2

Nell'esempio 2 viene assegnata una nuova descrizione al flusso di lavoro Help Desk trovato nel servizio ApplicationServer:atl-cs-001.litwareinc.com. A tale scopo, il primo comando dell'esempio recupera il flusso di lavoro specificato (-Name "Help Desk") e archivia l'oggetto recuperato in una variabile denominata $x. Nel secondo comando viene aggiunta una nuova descrizione ("Workflow for the Redmond Help Desk") alla copia virtuale del flusso di lavoro Help Desk. Una volta modificata la descrizione, nel terzo comando viene utilizzato **Set-CsRgsWorkflow** per scrivere le modifiche nel flusso di lavoro Help Desk effettivo in ApplicationServer:atl-cs-001.litwareinc.com.

    $x = Get-CsRgsWorkflow service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    $x.Description = "Workflow for the Redmond Help Desk" 
    Set-CsRgsWorkflow -Instance $x

## ESEMPIO 3

I comandi mostrati nell'esempio 3 importano un nuovo file audio di Response Group e lo assegnano a un flusso di lavoro esistente. Per effettuare questa operazione, il primo comando nell'esempio importa un nuovo file audio. A tale scopo, viene chiamato il cmdlet **Get-Content** per leggere byte per byte il file audio (C:\\MediaFiles\\Hold.wav). Per essere certi che il file audio venga letto correttamente, è necessario includere il parametro ReadContent (impostato su 0) e il parametro Encoding (impostato su Byte). Dopo che il file audio è stato letto, i dati vengono inviati tramite pipe a **New-CsRgsAudioFile**, che crea un nuovo file in ApplicationServer:atl-cs-001.litwareinc.com. Un riferimento oggetto a tale file, denominato HelpDeskHoldMusic.wav, viene archiviato in una variabile denominata $musicFile.

Dopo che il file audio è stato creato, il secondo comando recupera il flusso di lavoro Help Desk da ApplicationServer:atl-cs-001.litwareinc.com, archiviando l'oggetto restituito in una variabile denominata $y. Nel terzo comando alla proprietà CustomMusicOnHoldFile relativa a questo flusso di lavoro viene assegnato il valore $musicFile, che è la variabile contenente il file audio appena creato.

Dopo l'assegnazione di $musicFile a CustomMusicOnHoldFile, nel comando finale viene utilizzato il cmdlet **Set-CsRgsWorkflow** per scrivere tali modifiche nel flusso di lavoro Help Desk.

    $musicFile = Get-Content -ReadCount 0 -Encoding Byte C:\MediaFiles\Hold.wav | Import-CsRgsAudioFile -Identity Service:ApplicationServer:atl-cs-001.litwareinc.com -FileName "HelpDeskHoldMusic.wav"
    $y = Get-CsRgsWorkflow -Identity Service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    $y.CustomMusicOnHoldFile = $musicFile
    Set-CsRgsWorkflow -Instance $y

## Descrizione dettagliata

I flussi di lavoro sono forse l'elemento chiave dell'applicazione Response Group. Ciascun flusso di lavoro è associato univocamente a un numero di telefono; quando qualcuno chiama questo numero, il flusso di lavoro determina il modo in cui la chiamata verrà gestita. Ad esempio, la chiamata può essere instradata a una serie di domande del sistema IVR (Interactive Voice Response), mediante cui si avvisa il chiamante che è necessario immettere ulteriori informazioni (ad esempio, "Premere 1 per supporto hardware. Premere 2 per supporto software.") In alternativa, la chiamata può essere messa in una coda e il chiamante può essere lasciato in attesa finché un agente non sia disponibile per rispondere alla chiamata. La disponibilità di agenti che rispondano alle chiamate è determinata anche dal flusso di lavoro: i flussi di lavoro sono utilizzati per configurare sia l'orario di ufficio (i giorni della settimana e le ore del giorno in cui gli agenti sono disponibili per rispondere alle chiamate) sia i periodi di vacanza (giorni in cui non ci sono agenti disponibili per rispondere alle chiamate).

Il cmdlet **Set-CsRgsWorkflow** consente di modificare le proprietà di un flusso di lavoro esistente. Ad esempio, è possibile modificare il numero di telefono per un flusso di lavoro, i gruppi di agenti associati a un flusso di lavoro, o l'azione predefinita da eseguire ogni volta che il flusso di lavoro viene attivato, ovvero ogni volta che qualcuno chiama il numero di telefono associato al flusso di lavoro.

**Set-CsRgsWorkflow** non modifica direttamente un flusso di lavoro. Se si desidera apportare modifiche a un flusso di lavoro, è invece necessario innanzitutto utilizzare **Get-CsRgsWorkflow** per creare un riferimento oggetto al flusso di lavoro. Ciò significa semplicemente che si recupera il flusso di lavoro a cui si è interessati e quindi si archivia in una variabile l'oggetto restituito. Dopo avere creato il riferimento oggetto, è possibile modificare le proprietà dell'oggetto in memoria e quindi utilizzare **Set-CsRgsWorkflow** per scrivere tali modifiche nel flusso di lavoro effettivo dell'applicazione Response Group. Se **Set-CsRgsWorkflow** non viene chiamato, le modifiche esisteranno solo in memoria e scompariranno non appena si chiuderà Windows PowerShell o si eliminerà la variabile del riferimento oggetto.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsRgsWorkflow** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsRgsWorkflow"}

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
<td><p>Riferimento oggetto al flusso di lavoro dell'applicazione Response Group da modificare. Un riferimento oggetto in genere viene recuperato utilizzando il cmdlet <strong>Get-CsRgsWorkflow</strong> e assegnando il valore restituito a una variabile. Questo comando ad esempio restituisce un riferimento oggetto al flusso di lavoro Help Desk e archivia tale riferimento in una variabile denominata $x:</p>
<p>$x = Get-CsRgsWorkflow service:ApplicationServer:atl-cs-001.litwareinc.com -Name &quot;Help Desk&quot;</p>
<p>Il parametro Instance è un parametro posizionale e quindi può essere omesso se il riferimento oggetto al flusso di lavoro è il primo valore di parametro utilizzato nel comando. I due comandi seguenti sono pertanto identici da un punto di vista funzionale:</p>
<p>Set-CsRgsWorkflow –Instance $x</p>
<p>Set-CsRgsWorkflow $x</p></td>
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

Oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.Workflow. **Set-CsRgsWorkflow** accetta le istanze da pipeline dell'oggetto flusso di lavoro di Response Group.

## Tipi restituiti

**Set-CsRgsWorkflow** non restituisce alcun oggetto o valore. Il cmdlet modifica invece istanze esistenti dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.Workflow.

## Vedere anche

#### Ulteriori risorse

[Get-CsRgsWorkflow](get-csrgsworkflow.md)  
[New-CsRgsWorkflow](new-csrgsworkflow.md)  
[Remove-CsRgsWorkflow](remove-csrgsworkflow.md)

