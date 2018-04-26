---
title: New-CsRgsAnswer
TOCTitle: New-CsRgsAnswer
ms:assetid: aba521db-1741-4da3-aaf0-2d78fda4c4d2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412812(v=OCS.15)
ms:contentKeyID: 49301637
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRgsAnswer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova risposta di Response Group. Le risposte di Response Group sono utilizzate per associare una risposta del chiamante all'azione appropriata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsRgsAnswer -Action <CallAction> [-DtmfResponse <String>] [-Name <String>] [-VoiceResponseList <PSListModifier>]

## Descrizione dettagliata

Per elaborare le chiamate, spesso l'applicazione Response Group fornisce un'istruzione o pone una domanda e quindi esegue un'azione in base alla risposta del cliente. Ad esempio, il servizio può chiedere al chiamante di premere 1 per l'inglese e 2 per lo spagnolo. Dopo questo tipo di domanda, il sistema deve aspettare la risposta del chiamante, quindi eseguire l'azione appropriata. In questo caso, ciò significa che la chiamata viene trasferita alla coda della lingua inglese, se il chiamante preme 1 sulla tastiera del telefono, o a quella della lingua spagnola se il chiamante preme 2 sulla tastiera.

Le risposte di Response Group sono utilizzate per analizzare le risposte del chiamante ed eseguire l'azione appropriata. Ad esempio, se ai chiamanti viene fornita l'opzione di premere 1 o 2, le risposte di Response Group sono necessarie per affrontare la situazione: le due risposte servono infatti a specificare l'azione da eseguire nel caso in cui il chiamante prema 1 o 2. Queste due risposte vengono create utilizzando il cmdlet **New-CsRgsAnswer** e quindi devono essere aggiunte alla domanda appropriata di Response Group, ovvero alla domanda posta ai chiamanti affinché premano 1 o 2. Le risposte di Response Group devono includere un insieme di risposte vocali consentite (ad esempio, la parola "Inglese") o la risposta appropriata tramite la tastiera del telefono (ad esempio, da fornire premendo 1). In alternativa, è possibile fornire ai clienti l'opzione di utilizzare la risposta vocale o la risposta tramite tastiera: pronunciando la parola "Inglese" o premendo 1 sulla tastiera. In queste situazioni per il riconoscimento vocale viene utilizzata la lingua del flusso di lavoro padre.

Le risposte di Response Group non possono essere salvate e riutilizzate con altre domande. Si prenda ad esempio il caso di una risposta che trasferisce una chiamata alla segreteria telefonica ogni volta che un chiamante preme 9. Si decide quindi di associare tale risposta a una domanda di Response Group. In un secondo momento si provvede a creare una nuova domanda che fornisce a sua volta ai chiamanti l'opzione di trasferire la chiamata alla segreteria telefonica premendo 9. In questo caso, sarà necessario creare una nuova istanza della risposta di Response Group. Non vi è infatti alcun modo per salvare le risposte e utilizzare più volte le risposte salvate.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsRgsAnswer** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Poiché tuttavia questo cmdlet crea un oggetto in memoria e da solo non apporta modifiche al sistema, può essere essenzialmente eseguito da chiunque. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRgsAnswer"}

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
<td><p><em>Action</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.CallAction</p></td>
<td><p>Indica l'azione da eseguire ogni volta che un chiamante fornisce questa risposta. Il parametro Action deve essere specificato utilizzando un riferimento oggetto creato mediante il cmdlet <strong>New-CsRgsCallAction</strong>. Per informazioni dettagliate, vedere la sezione relativa agli esempi in questo argomento.</p></td>
</tr>
<tr class="even">
<td><p><em>DtmfResponse</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indica il tasto da premere sulla tastiera del telefono per trovare la risposta corrispondente. Ad esempio, se ai chiamanti viene detto di premere 1 per Hardware, DtmfResponse è configurato come segue: -DtmfResponse 1.</p>
<p>Una singola risposta può includere sia una risposta vocale che una risposta multifrequenza (DTMF, Dual Tone Multiple-Frequency). Ogni risposta deve avere almeno uno di questi due tipi di risposta.</p></td>
</tr>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome assegnato alla risposta di Response Group. I nomi non devono essere univoci.</p></td>
</tr>
<tr class="even">
<td><p><em>VoiceResponseList</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Array di parole chiave corrispondenti alla risposta che i chiamanti possono pronunciare. Ad esempio, se un'opzione disponibile per i chiamanti è &quot;Hardware&quot;, la proprietà VoiceResponseList può essere impostata come segue: -VoiceResponseList &quot;Hardware&quot;. Diverse parole chiave possono essere specificate utilizzando valori delimitati da virgole. Ad esempio, questo valore del parametro fa corrispondere alla risposta Hardware o Dispositivi: -VoiceResponseList Hardware, Devices. Le risposte vocali non devono contenere virgolette doppie perché tale carattere non viene riconosciuto dal motore di sintesi vocale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. **New-CsRgsAnswer** non accetta l'input da pipeline.

## Tipi restituiti

Crea nuove istanze dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.Answer.

## Esempi

## ESEMPIO 1

I comandi mostrati nell'esempio 1 illustrano come creare una nuova risposta di Response Group associata a una coda di Response Group e a un'azione di chiamata di Response Group. Nel primo comando dell'esempio viene utilizzato il cmdlet **New-CsRgsPrompt** per creare un oggetto TextToSpeechPrompt per la nuova risposta. Viene quindi chiamato il cmdlet **Get-CsRgsQueue** per restituire un riferimento oggetto ($x) alla coda di Response Group Help Desk. Il riferimento oggetto viene quindi utilizzato nel comando successivo, che chiama **New-CsRgsCallAction** per creare un'azione di chiamata che trasferisca il chiamante alla coda Help Desk. L'azione di chiamata viene archiviata in una variabile denominata $y.

Il comando finale dell'esempio crea una risposta di Response Group (archiviata nella variabile $a). Tale risposta accetta la risposta DTMF 1 (che viene fornita premendo 1 sulla tastiera del telefono) o la risposta vocale "Yes" ("Sì").

Dopo che la risposta è stata creata, può essere associata a una domanda di Response Group. Per informazioni dettagliate, vedere l'argomento [New-CsRgsQuestion](new-csrgsquestion.md) della Guida.

    $w = New-CsRgsPrompt -TextToSpeechPrompt "Please hold while we transfer your call."
    $x = Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    
    $y = New-CsRgsCallAction -Prompt $w -Action TransferToQueue -QueueID $x.Identity
    
    $a = New-CsRgsAnswer -Action $y -DtmfResponse 1 -VoiceResponseList Yes -Name "New Service Request"

## Vedere anche

#### Ulteriori risorse

[New-CsRgsQuestion](new-csrgsquestion.md)

