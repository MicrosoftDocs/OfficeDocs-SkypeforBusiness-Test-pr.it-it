---
title: New-CsRgsPrompt
TOCTitle: New-CsRgsPrompt
ms:assetid: 6812acbf-ae56-43a6-a2d7-e28a930f81c7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398486(v=OCS.15)
ms:contentKeyID: 49300842
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRgsPrompt

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo prompt del flusso di lavoro per l'applicazione Response Group. Un prompt del flusso di lavoro è un file audio riprodotto o un testo letto ad alta voce in grado di fornire informazioni supplementari ai chiamanti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsRgsPrompt [-AudioFilePrompt <AudioFile>] [-TextToSpeechPrompt <String>]

## Esempi

## ESEMPIO 1

I comandi mostrati nell'Esempio 1 illustrano come includere un prompt del flusso di lavoro (e una coda di Response Group) in una nuova azione di chiamata. Nel primo comando viene utilizzato il cmdlet **Get-CsRgsQueue** per ottenere un riferimento oggetto ($queue) alla coda di Response Group denominata Help Desk. Nel secondo comando viene utilizzato il cmdlet **New-CsRgsPrompt** per creare il nuovo prompt di sintesi vocale "Welcome to the help desk. Please hold." Il nuovo prompt viene archiviato in una variabile denominata $prompt.

Nel comando finale dell'esempio viene utilizzato il cmdlet **New-CsRgsCallAction** per creare una nuova azione di chiamata di Response Group ($z). Quando si crea un'azione di chiamata, il riferimento oggetto $prompt (che contiene il prompt del flusso di lavoro appena creato) viene utilizzato come valore del parametro Prompt; analogamente, il riferimento oggetto $queue viene utilizzato insieme al parametro QueueID. Dopo aver eseguito questo comando, la nuova azione di chiamata e il corrispondente nuovo prompt del flusso di lavoro sono pronti per essere aggiunti a un flusso di lavoro di Response Group.

    $queue = Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    
    $prompt = New-CsRgsPrompt -TextToSpeechPrompt "Welcome to the help desk. Please hold."
    
    $z = New-CsRgsCallAction -Prompt $prompt -Action TransferToQueue -QueueID $queue.Identity

## ESEMPIO 2

I comandi mostrati nell'esempio 2 sono una variante dei comandi mostrati nell'esempio 1. In questo caso, tuttavia, il nuovo prompt del flusso di lavoro include un prompt di file audio oltre a un prompt di sintesi vocale. Per includere un file audio nel prompt del flusso di lavoro, nel il secondo comando nell'esempio viene utilizzato il cmdlet **Import-CsRgsAudioFile** per importare il file audio C:\\Media\\Welcome.wav. Il file importato viene quindi archiviato in una variabile denominata $audioFile.

Dopo essere stato importato, il file audio e il prompt di sintesi vocale vengono aggiunti a un nuovo prompt del flusso di lavoro ($prompt). Per ottenere questo risultato, il parametro AudioFilePrompt viene impostato su $audioFile e il parametro TextToSpeechPrompt viene impostato sul valore di testo "Welcome to the help desk. Please hold."

    $queue = Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk Queue"
    
    $audioFile = Import-CsRgsAudioFile -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -FileName "welcome.wav" -Content (Get-Content C:\Media\Welcome.wav -Encoding byte -ReadCount 0)
    
    $prompt = New-CsRgsPrompt -AudioFilePrompt $audioFile -TextToSpeechPrompt "Welcome to the help desk. Please hold."
    
    $z = New-CsRgsCallAction -Prompt $prompt -Action TransferToQueue -QueueID $queue.Identity

## Descrizione dettagliata

Mantenere i chiamanti informati su ciò che sta succedendo e sul perché sta succedendo è una parte importante del flusso di lavoro di Response Group. Ad esempio, è possibile configurare il flusso di lavoro in modo che risponda a una telefonata e immediatamente dopo la metta in attesa finché un agente non sia disponibile. Tutto ciò è fattibile, ma è necessario informare il chiamante che: 1) la telefonata è arrivata; 2) la chiamata verrà lasciata in attesa finché l'agente non sarà disponibile. Fornire informazioni come questa è il compito del prompt del flusso di lavoro.

applicazione Response Group supporta due diversi tipi di prompt dell flusso di lavoro. Innanzitutto, è possibile pre-registrare e quindi riprodurre un file audio. Per fare ciò, è necessario registrare il prompt ("Rimanete in attesa. Risponderemo nel più breve tempo possibile.") in formato WAV o WMA; importare il file utilizzando il cmdlet **Import-CsRgsAudioFile** e quindi assegnare il file al prompt del flusso di lavoro. In alternativa, si può semplicemente fornire il testo da leggere e, quando è necessario il prompt, applicazione Response Group utilizzerà le funzionalità di sintesi vocale per "leggere" il testo ad alta voce. I prompt di sintesi vocale sono più semplici da configurare: non ci sono file audio da registrare e importare. D'altra parte, generalmente i prompt dei file audio sono di alta qualità e ad alta fedeltà.

Si noti che la lingua utilizzata in un prompt di sintesi vocale è la stessa utilizzata nel flusso di lavoro principale.

Il cmdlet **New-CsRgsPrompt** consente di creare i prompt del flusso di lavoro. Ogni volta che è necessario utilizzare un prompt, occorre crearlo da zero; non è possibile salvare e riutilizzare i prompt. Ciò significa che sarà necessario reimportare anche i file audio. Quando si crea un nuovo prompt del flusso di lavoro, è necessario fornire un prompt di sintesi vocale; se si desidera, è possibile fornire anche un file audio. Se si forniscono un prompt di sintesi vocale e un prompt di file audio, applicazione Response Group utilizzerà il file audio per impostazione predefinita e si rivolgerà al prompt di sintesi vocale soltanto se il file audio non è disponibile. Dopo che in memoria sono stati creati nuovi prompt, generalmente il riferimento oggetto corrispondente viene aggiunto a un'azione di chiamata di Response Group.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsRgsPrompt** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Tuttavia, dal momento che questo cmdlet consente di creare un oggetto in memoria senza apportare modifiche al sistema, può essere utilizzato da chiunque. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRgsPrompt"}

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
<td><p><em>AudioFilePrompt</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.AudioFile</p></td>
<td><p>File audio da riprodurre quando il flusso di lavoro è attivato. Il file audio deve essere importato utilizzando il cmdlet <strong>Import-CsRgsAudioFile</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>TextToSpeechPrompt</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Prompt di sintesi vocale (TTS) da leggere quando il flusso di lavoro è attivato. Il prompt di sintesi vocale, utilizzato soltanto se non è specificato alcun file audio, può contenere un massimo di 4096 caratteri.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. **New-CsRgsPrompt** non accetta input tramite pipeline.

## Tipi restituiti

**New-CsRgsPrompt** consente di creare istanze dell'oggetto Microsoft.Rtc.Management.WritableSettings.Prompt.

## Vedere anche

#### Ulteriori risorse

[Import-CsRgsAudioFile](import-csrgsaudiofile.md)  
[New-CsRgsCallAction](new-csrgscallaction.md)

