---
title: Import-CsRgsAudioFile
TOCTitle: Import-CsRgsAudioFile
ms:assetid: ae9dfd76-9b3e-4c51-9692-39d1fe8e430b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412830(v=OCS.15)
ms:contentKeyID: 49301657
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsRgsAudioFile

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Importa un nuovo file audio da utilizzare con l'applicazione Response Group. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Import-CsRgsAudioFile -Content <Byte[]> -FileName <String> -Identity <RgsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

I comandi mostrati nell'esempio 1 importano un file audio (C:\\Media\\WhileYouWait.wav) e assegnano quindi il file alla proprietà CustomMusicOnHold di un flusso di lavoro. Per eseguire questa attività, nel primo comando viene utilizzato **Import-CsRgsAudioFile** per importare il file audio nell'applicazione Response Group trovata in ApplicationServer:atl-cs-001.litwareinc.com. Oltre al parametro Identity che specifica la posizione del servizio, viene utilizzato il parametro FileName per specificare il nome del file da importare.

Viene contemporaneamente utilizzato il parametro Content per importare il file audio. L'importazione di file viene eseguita chiamando il cmdlet **Get-Content** seguito dal percorso del file da importare. **Get-Content** richiede inoltre di impostare il tipo di codifica su byte e ReadCount su 0. L'impostazione di ReadCount su 0 garantisce che l'intero file venga letto in una singola operazione. Il file importato viene quindi archiviato in una variabile denominata $x.

Nel secondo comando viene utilizzato **Get-CsRgsWorkflow** per creare un riferimento oggetto ($y) al flusso di lavoro Help Desk Workflow. Una volta creato questo riferimento oggetto, il terzo comando imposta il valore della proprietà CustomMusicOnHoldFile su $x, la variabile contenente il file audio importato. Nell'ultimo comando dell'esempio viene infine utilizzato **Set-CsRgsWorkflow** per scrivere queste modifiche nel flusso di lavoro effettivo Help Desk Workflow. Se **Set-CsRgsWorkflow** non viene chiamato, le modifiche esisteranno solo in memoria e scompariranno non appena si chiuderà Windows PowerShell o si eliminerà la variabile $x o $y.

    $x = Import-CsRgsAudioFile -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -FileName "WhileYouWait.wav" -Content (Get-Content C:\Media\WhileYouWait.wav -Encoding byte -ReadCount 0)
    
    $y = Get-CsRgsWorkflow -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "Help Desk Workflow"
    $y.CustomMusicOnHoldFile = $x
    
    Set-CsRgsWorkflow $y

## Descrizione dettagliata

L'applicazione Response Group può utilizzare file audio (soltanto nei formati WAV o WMA) in almeno due modi diversi. Nel primo caso, il servizio può riprodurre musica (o un annuncio) ogni volta che i chiamanti vengono lasciati in attesa. In alternativa, l'applicazione Response Group occasionalmente "parla" ai chiamanti. Ad esempio, tramite il sistema IVR (Interactive Voice Response), il servizio può porre ai chiamanti domande del tipo "Sta chiamando per un ordine esistente?". È possibile configurare il servizio in modo che legga tali domande utilizzando la tecnologia di sintesi vocale oppure riprodurre la registrazione audio di una persona reale che pone la domanda.

Indipendentemente dalla modalità con cui si sceglie di utilizzare i file audio, questi devono essere importati nell'applicazione Response Group mediante il cmdlet **Import-CsRgsAudioFile**. È necessario eseguire **Import-CsRgsAudioFile** ogni volta che si desidera utilizzare un file audio, anche se tale file è già in uso in un altro punto dell'applicazione Response Group. Si supponga ad esempio che nel flusso di lavoro A venga utilizzato un determinato file audio come file per la musica di attesa personalizzata e che ora si desideri utilizzare lo stesso file audio come musica di attesa personalizzata per il flusso di lavoro B. Anche se il file audio viene già utilizzato dall'applicazione Response Group, sarà comunque necessario importarlo per poterlo utilizzare nel flusso di lavoro B.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Import-CsRgsAudioFile** i membri dei seguenti gruppi: RTCUniversalServerAdmins. È inoltre necessario disporre dell'accesso in scrittura all'archivio file del computer di destinazione. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsRgsAudioFile"}

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
<td><p><em>Content</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Byte[]</p></td>
<td><p>Il contenuto attuale del file audio da importare. Nella proprietà Content vengono inseriti i dati chiamando il cmdlet <strong>Get-Content</strong>. Quando si chiama <strong>Get-Content</strong>, impostare il parametro Encoding su byte e il parametro ReadCount su 0. Per informazioni dettagliate, vedere la sezione relativa agli esempi in questo argomento.</p></td>
</tr>
<tr class="even">
<td><p><em>FileName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome del file audio da importare. Ad esempio, il nome del file per il file C:\Media\Welcome.wav è questo: Welcome.wav.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>Identità del servizio in cui importare il file audio. Deve essere lo stesso servizio in cui è ospitata l'applicazione Response Group. Ad esempio: -Identity &quot;service:ApplicationServer:atl-cs-001.litwareinc.com&quot;.</p></td>
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

Nessuno. **Import-CsRgsAudioFile** non accetta l'input da pipeline.

## Tipi restituiti

Crea nuove istanze dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.AudioFile.

## Vedere anche

#### Ulteriori risorse

[New-CsRgsWorkflow](new-csrgsworkflow.md)  
[Set-CsRgsWorkflow](set-csrgsworkflow.md)

