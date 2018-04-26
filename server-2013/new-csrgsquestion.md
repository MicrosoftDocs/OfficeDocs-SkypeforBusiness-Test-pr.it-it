---
title: New-CsRgsQuestion
TOCTitle: New-CsRgsQuestion
ms:assetid: 0ed9f3b4-cbc5-41ca-8547-2300b579b119
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398186(v=OCS.15)
ms:contentKeyID: 49299687
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRgsQuestion

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova domanda di Response Group. L'applicazione Response Group utilizza domande per fornire scelte ai chiamanti e quindi esegue un'azione in base alle scelte effettuate dai chiamanti stessi. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsRgsQuestion -Prompt <Prompt> [-AnswerList <PSListModifier>] [-InvalidAnswerPrompt <Prompt>] [-Name <String>] [-NoAnswerPrompt <Prompt>]

## Esempi

## ESEMPIO 1

I comandi mostrati nell'esempio 1 creano una coppia di risposte di Response Group e le associano a una nuova domanda di Response Group. Per creare le due risposte, è innanzitutto necessario specificare le azioni di chiamata da eseguire a seconda della risposta fornita dal chiamante. Di conseguenza, i primi due comandi nell'esempio creano riferimenti oggetto alla coppia di code di Response Group: New Service Request ed Existing Service Request. Dopo che questi riferimenti oggetto sono stati creati, nel comando successivo viene utilizzato **New-CsRgsPrompt** per creare un prompt di sintesi vocale che viene archiviato in una variabile denominata $w.

Al termine di tale operazione, i due comandi successivi creano una coppia di azioni di chiamata corrispondenti, una per trasferire i chiamanti alla coda New Service Request e l'altra per trasferire i chiamanti alla coda Existing Service Request. Dopo che le azioni di chiamata sono state create, viene utilizzato il cmdlet **New-CsRgsAnswer** per creare due risposte di Response Group, una archiviata nella variabile $newRequest e l'altra nella variabile $existingRequest.

Con le due risposte archiviate, è quindi possibile utilizzare **New-CsRgsPrompt** per creare un prompt per la nuova domanda. In questo esempio il prompt è di sintesi vocale e richiede al chiamante di premere 1 o dire "New" (Nuova) per una nuova richiesta di assistenza oppure di premere 2 o dire "Existing" (Esistente) per una richiesta di assistenza esistente. Il prompt viene archiviato in una variabile denominata $u.

Una volta creato il prompt, è quindi possibile chiamare **New-CsRgsQuestion** per creare la nuova domanda. Oltre al parametro Prompt, viene utilizzato il parametro AnswerList per indicare le due risposte associate alla domanda, ovvero le variabili $newRequest ed $existingRequest.

    $new = Get-CsRgsQueue -Identity service:ApplicationServer:pool0.litwareinc.com -Name "New Service Request"
    $existing = Get-CsRgsQueue -Identity service:ApplicationServer:pool0.litwareinc.com -Name "Existing Service Request"
    
    $w = New-CsRgsPrompt -TextToSpeechPrompt "Please hold while we transfer your call."
    
    $y = New-CsRgsCallAction -Prompt $w -Action TransferToQueue -QueueID $new.Identity
    $z = New-CsRgsCallAction -Prompt $w -Action TransferToQueue -QueueID $existing.Identity
    
    $newRequest = New-CsRgsAnswer -Action $y -DtmfResponse 1 -VoiceResponseList "New" -Name "New Request"
    $existingRequest = New-CsRgsAnswer -Action $z -DtmfResponse 2 -VoiceResponseList "Existing" -Name "Existing Request"
    
    $u = New-CsRgsPrompt -TextToSpeechPrompt "Press 1 or say New for a new service request. Press 2 or say Existing for an existing service request."
    
    $question = New-CsRgsQuestion -Prompt $u -AnswerList $newRequest $newRequest, $existingRequest 

## Descrizione dettagliata

Per elaborare le chiamate, spesso l'applicazione Response Group fornisce un'istruzione o pone una domanda e quindi esegue un'azione in base alla risposta del chiamante. Ad esempio, il servizio può chiedere al chiamante di premere 1 per l'inglese e 2 per lo spagnolo. Dopo questo tipo di domanda, il sistema deve aspettare la risposta del chiamante, quindi eseguire l'azione appropriata. In questo caso, ciò significa che la chiamata viene trasferita alla coda della lingua inglese se il chiamante preme 1 sulla tastiera del telefono oppure a quella della lingua spagnola se il chiamante preme 2 sulla tastiera.

Per poter creare una domanda, è necessario utilizzare il cmdlet **New-CsRgsQuestion**. Quando si crea una domanda di Response Group, è necessario fornire almeno un prompt (ovvero la domanda effettiva) e un gruppo di risposte supportate. Se, ad esempio si offre ai chiamanti la possibilità di premere 1 o 2, sarà necessario disporre di due risposte: una per specificare l'azione da eseguire se il chiamante preme 1 e l'altra per specificare l'azione da eseguire se il chiamante preme 2. Se si offre ai chiamanti la possibilità di premere 1, 2, 3 o 4, saranno necessarie quattro risposte e così via.

**New-CsRgsQuestion** inoltre offre la possibilità di specificare un prompt da utilizzare nel caso in cui un chiamante non risponda o fornisca una risposta non valida. Se ad esempio il chiamante nello scenario originale preme 3, il prompt potrebbe essere simile al seguente: "Risposta non valida". A quel punto, verrà di nuovo visualizzato il prompt originale.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsRgsQuestion** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Poiché tuttavia questo cmdlet crea un oggetto in memoria e da solo non apporta modifiche al sistema, può essere essenzialmente eseguito da chiunque. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRgsQuestion"}

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
<td><p><em>Prompt</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.Prompt</p></td>
<td><p>Domanda del chiamante. È necessario creare i prompt utilizzando il cmdlet <strong>New-CsRgsPrompt</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>AnswerList</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Array di risposte valide alla domanda. Ad esempio, una domanda relativa al supporto tecnico può comportare risposte come Supporto hardware, Installazione software e Connessioni di rete. È necessario creare le risposte utilizzando il cmdlet <strong>New-CsRgsAnswer</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>InvalidAnswerPrompt</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.Prompt</p></td>
<td><p>Risposta da fornire nel caso in cui il chiamante scelga una risposta non valida. È necessario creare l'oggetto InvalidAnswerPrompt utilizzando il cmdlet <strong>New-CsRgsPrompt</strong>. Dopo la riproduzione dell'oggetto InvalidAnswerPrompt, verrà ripetuto il prompt originale.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Identificatore della domanda. I nomi delle domande, che non devono essere univoci, possono essere costituiti al massimo da 128 caratteri.</p></td>
</tr>
<tr class="odd">
<td><p><em>NoAnswerPrompt</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.Prompt</p></td>
<td><p>Risposta da fornire nel caso in cui il chiamante non risponda al prompt iniziale. È necessario creare l'oggetto NoAnswerPrompt utilizzando il cmdlet <strong>New-CsRgsPrompt</strong>.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. **New-CsRgsQuestion** non accetta l'input da pipeline.

## Tipi restituiti

**New-CsRgsQuestion** crea istanze dell'oggetto Microsoft.Rtc.Management.WriteableSettings.Question.

## Vedere anche

#### Ulteriori risorse

[New-CsRgsAnswer](new-csrgsanswer.md)

