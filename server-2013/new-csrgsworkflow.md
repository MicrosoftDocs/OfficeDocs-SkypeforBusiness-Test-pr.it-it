---
title: New-CsRgsWorkflow
TOCTitle: New-CsRgsWorkflow
ms:assetid: 1a2ac5b7-cb1d-4a83-801f-f27671e71743
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398246(v=OCS.15)
ms:contentKeyID: 49299833
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRgsWorkflow

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo flusso di lavoro di Response Group. I flussi di lavoro determinano le azioni da eseguire quando l'applicazione Response Group riceve una chiamata telefonica. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsRgsWorkflow -Name <String> -Parent <RgsIdentity> -PrimaryUri <Uri> [-Active <$true | $false>] [-Anonymous <$true | $false>] [-BusinessHoursID <RgsIdentity>] [-Confirm [<SwitchParameter>]] [-CustomMusicOnHoldFile <AudioFile>] [-DefaultAction <CallAction>] [-Description <String>] [-DisplayNumber <String>] [-EnabledForFederation <$true | $false>] [-Force <SwitchParameter>] [-HolidayAction <CallAction>] [-HolidaySetIDList <Collection>] [-InMemory <SwitchParameter>] [-Language <String>] [-LineUri <Uri>] [-Managed <$true | $false>] [-ManagersByUri <Collection>] [-NonBusinessHoursAction <CallAction>] [-TimeZone <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene creato un nuovo flusso di lavoro nel servizio ApplicationServer:atl-cs-001.litwareinc.com. A questo flusso di lavoro vengono assegnati il nome Help Desk e l'URI primario sip:helpdesk@litwareinc.com.

    New-CsRgsWorkflow -Parent service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk" -PrimaryUri "sip:helpdesk@litwareinc.com" 

## ESEMPIO 2

Il comando mostrato nell'esempio 2 crea un nuovo prompt di flusso di lavoro e una nuova azione di chiamata, quindi assegna tali elementi a un nuovo flusso di lavoro di Response Group. Nel primo comando viene utilizzato il cmdlet **New-CsRgsPrompt** per creare un prompt di sintesi vocale "Welcome to the help desk". Il nuovo prompt viene archiviato in una variabile denominata $prompt.

Nel secondo comando viene utilizzato il cmdlet **Get-CsRgsQueue** per recuperare l'identità di una coda esistente di Response Group denominata Help Desk. L'identità restituita viene archiviata in una variabile denominata $queue.

Il comando 3 crea quindi una nuova azione di chiamata (archiviata in una variabile denominata $callAction) che fa riferimento sia al nuovo prompt ($prompt), sia alla coda recuperata ($queue). L'ultimo comando dell'esempio infine crea un nuovo flusso di lavoro denominato Help Desk. Tale comando imposta il parametro PrimaryUri su sip:helpdesk@litwareinc.com e il valore della proprietà DefaultAction sull'azione di chiamata creata nel passaggio precedente.

    $prompt = New-CsRgsPrompt -TextToSpeechPrompt "Welcome to the help desk."
    $queue = (Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk").Identity
    $callAction = New-CsRgsCallAction -Prompt $prompt -Action TransferToQueue -QueueId $queue
    New-CsRgsWorkflow -Parent service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk" -PrimaryUri "sip:helpdesk@litwareinc.com" -DefaultAction $callAction

## Descrizione dettagliata

I flussi di lavoro sono un elemento chiave dell'applicazione Response Group. Ciascun flusso di lavoro è associato in modo univoco a un numero di telefono. Quando una persona chiama questo numero, il flusso di lavoro determina il modo in cui la chiamata verrà gestita. La chiamata può ad esempio essere instradata a una serie di domande del sistema IVR (Interactive Voice Response), mediante cui si avvisa il chiamante che è necessario immettere ulteriori informazioni ("Premere 1 per supporto hardware. Premere 2 per supporto software.") In alternativa, la chiamata può essere messa in una coda e il chiamante può essere lasciato in attesa finché un agente non è disponibile per rispondere alla chiamata. La disponibilità di agenti che rispondano alle chiamate è determinata anche dal flusso di lavoro: i flussi di lavoro sono utilizzati per configurare sia l'orario di ufficio (i giorni della settimana e le ore del giorno in cui gli agenti sono disponibili per rispondere alle chiamate) sia le festività (giorni in cui non ci sono agenti disponibili per rispondere alle chiamate).

È possibile creare nuovi flussi di lavoro utilizzando il cmdlet **New-CsRgsWorkflow**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsRgsWorkflow** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRgsWorkflow"}

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
<td><p>Nome univoco da assegnare al flusso di lavoro. La combinazione della proprietà Parent e della proprietà Name consente di identificare in modo univoco i flussi di lavoro senza dover fare riferimento al relativo identificatore univoco globale (GUID).</p></td>
</tr>
<tr class="even">
<td><p><em>Parent</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>Servizio in cui sarà ospitato il nuovo flusso di lavoro. Ad esempio: -Parent &quot;service:ApplicationServer:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>PrimaryUri</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Uri</p></td>
<td><p>Indirizzo SIP per il flusso di lavoro. Ad esempio: -PrimaryUri &quot;sip:helpdesk@litwareinc.com&quot;. PrimaryUri deve iniziare con il prefisso &quot;sip:&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Active</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su TRUE, il flusso di lavoro è attivo e disponibile a ricevere chiamate telefoniche. Se la proprietà è impostata su False (valore predefinito), il flusso di lavoro non sarà disponibile per ricevere chiamate telefoniche.</p>
<p>Se la proprietà Active è impostata su True, il flusso di lavoro verrà convalidato prima di essere creato. Ad esempio, non verrà creato se non è stato specificato un parametro DefaultAction. Se la proprietà Active è impostata su False o non configurata, non verrà eseguita alcuna convalida e il flusso di lavoro verrà creato anche se non è stato specificato un parametro DefaultAction.</p></td>
</tr>
<tr class="odd">
<td><p><em>Anonymous</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostate su True, le identità dei singoli agenti di Response Group saranno mascherate ogni volta che questi agenti rispondono a una chiamata. Se questo parametro è impostato su False (valore predefinito), le identità degli agenti saranno disponibili per i chiamanti.</p></td>
</tr>
<tr class="even">
<td><p><em>BusinessHoursID</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>Giorni della settimana e ore del giorno in cui gli agenti del flusso di lavoro sono disponibili per rispondere alle chiamate. Le identità degli orari d'ufficio possono essere recuperate utilizzando il cmdlet <strong>Get-CsRgsHoursOfBusiness</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>CustomMusicOnHoldFile</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.AudioFile</p></td>
<td><p>Rappresenta la musica personalizzata da riprodurre quando i chiamanti restano in attesa. Se non definita, durante l'attesa i chiamanti sentiranno la musica predefinita. La musica personalizzata deve essere importata utilizzando il cmdlet <strong>Import-CsRgsAudioFile</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultAction</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.CallAction</p></td>
<td><p>Indica l'azione da eseguire quando un flusso di lavoro viene aperto durante l'orario d'ufficio. Il parametro DefaultAction deve essere definito utilizzando il cmdlet <strong>New-CsRgsCallAction</strong> e deve instradare la chiamata a una coda oppure a una domanda. Il parametro DefaultAction è obbligatorio se il flusso di lavoro è attivo, ma può essere omesso se il flusso di lavoro non è attivo.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di aggiungere informazioni supplementari su un flusso di lavoro di Response Group. Description può includere ad esempio informazioni di contatto per il proprietario del flusso di lavoro. Questa descrizione viene visualizzata nella scheda contatto di Lync per il flusso di lavoro.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Numero di telefono per il flusso di lavoro così com'è visualizzato in Lync. Il valore DisplayNumber può essere formattato come desiderato, ad esempio:</p>
<p>-DisplayNumber &quot;555-1219&quot;</p>
<p>-DisplayNumber &quot;1-(425)-555-1219&quot;</p>
<p>-DisplayNumber &quot;1.425.555.1219&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>EnabledForFederation</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se il flusso di lavoro è disponibile per utenti di un dominio federato. Se impostato su FALSE, solo gli utenti interni all'organizzazione potranno accedere al flusso di lavoro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>HolidayAction</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.CallAction</p></td>
<td><p>Azione da eseguire quando la chiamata viene ricevuta durante le festività. Il parametro HolidayAction deve essere definito utilizzando il cmdlet <strong>New-CsRgsCallAction</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>HolidaySetIDList</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Collections.ObjectModel.Collection</p></td>
<td><p>Rappresenta i giorni in cui gli agenti del flusso di lavoro non sono disponibili per rispondere alle chiamate. Le identità dei set di festività possono essere recuperate utilizzando il cmdlet <strong>Get-CsRgsHolidaySet</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>Language</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Lingua utilizzata per leggere i prompt di sintesi vocale del flusso di lavoro. Il parametro Language è facoltativo, purché nel sistema operativo venga utilizzata una delle lingue supportate elencate di seguito. Si noti infatti che le lingue per messaggi vocali supportate rappresentano un sottoinsieme delle lingue utilizzabili nel sistema operativo.</p>
<p>Se nel sistema operativo non viene utilizzata una lingua supportata, sarà obbligatorio includere il parametro Language, che dovrà specificare il codice di una lingua supportata. Se nel sistema operativo viene utilizzata una lingua non supportata e si esegue il cmdlet <strong>New-CsRgsWorkflow</strong> senza includere il parametro Language, il comando avrà esito negativo.</p>
<p>Si supponga ad esempio che nel sistema operativo sia in uso il faroese. Tale lingua è supportata dal sistema operativo Windows, ma non dall'applicazione Response Group. Al momento di creare un nuovo flusso di lavoro, sarà pertanto necessario includere il parametro Language e una lingua supportata.</p>
<p>Tale operazione è necessaria perché, se non viene specificata alcuna lingua, per il flusso di lavoro verrà utilizzata quella del sistema operativo. Tale lingua potrà tuttavia essere utilizzata in un flusso di lavoro solo se è supportata dall'applicazione Response Group.</p>
<p>Il linguaggio deve essere specificato utilizzando uno dei seguenti codici della lingua:</p>
<p>ca-ES – Catalano (Spagna)</p>
<p>da-DK – Danese (Danimarca)</p>
<p>de-DE – Tedesco (Germania)</p>
<p>en-AU – Inglese (Australia)</p>
<p>en-CA – Inglese (Canada)</p>
<p>en-GB – Inglese (Regno Unito)</p>
<p>en-IN – Inglese (India)</p>
<p>en-US – Inglese (Stati Uniti)</p>
<p>es-ES – Spagnolo (Spagna)</p>
<p>es-MX – Spagnolo (Messico)</p>
<p>fi-FI – Finlandese (Finlandia)</p>
<p>fr-CA – Francese (Canada)</p>
<p>fr-FR – Francese (Francia)</p>
<p>it-IT – Italiano (Italia)</p>
<p>ja-JP – Giapponese (Giappone)</p>
<p>ko-KR – Coreano (Corea)</p>
<p>nb-NO – Norvegese, Bokmal (Norvegia)</p>
<p>nl-NL – Olandese (Paesi Bassi)</p>
<p>pl-PL – Polacco (Polonia)</p>
<p>pt-BR – Portoghese (Brasile)</p>
<p>pt-PT – Portoghese (Portogallo)</p>
<p>ru-RU – Russo (Russia)</p>
<p>sv-SE – Svedese (Svezia)</p>
<p>zh-CN – Cinese (Repubblica popolare cinese)</p>
<p>zh-HK – Cinese (Hong Kong - R.A.S.)</p>
<p>zh-TW – Cinese (Taiwan)</p>
<p>Ad esempio: -Lingua &quot;nl-NL&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>LineUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Uri</p></td>
<td><p>Numero di telefono per il flusso di lavoro. L'URI (Uniform Resource Identifier) della linea deve essere specificato utilizzando il seguente formato: il prefisso TEL: seguito da un segno più, seguito dall'indicativo di chiamata del paese o dell'area geografica, dall'indicativo di località e dal numero di telefono (utilizzando solo cifre, senza spazi, punti o trattini). Ad esempio: -LineUri &quot;TEL:+14255551219&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Managed</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, indica che il flusso di lavoro verrà gestito da uno o più utenti. Tali utenti possono essere specificati utilizzando il parametro ManagedByUri.</p></td>
</tr>
<tr class="even">
<td><p><em>ManagersByUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Collections.ObjectModel.Collection</p></td>
<td><p>Indirizzi SIP dell'utente o degli utenti che gestiranno il flusso di lavoro, ad esempio:</p>
<p>-ManagedByUri &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>Per specificare più responsabili, separare i relativi indirizzi SIP con le virgole:</p>
<p>-ManagedByUri &quot;sip:kenmyer@litwareinc.com&quot;, &quot;sip:pilar@litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>NonBusinessHoursAction</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.CallAction</p></td>
<td><p>Azione da eseguire quando una chiamata viene ricevuta fuori dall'orario di ufficio del flusso di lavoro. Il parametro NonBusinessHoursAction deve essere definito utilizzando il cmdlet <strong>New-CsRgsCallAction</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>TimeZone</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Le informazioni sul fuso orario utilizzate quando si definiscono l'orario di ufficio e le festività. Ad esempio: -TimeZone &quot;Ora solare pacifico&quot;</p></td>
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

Nessuno. Il cmdlet **New-CsRgsWorkflow** non accetta l'input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsRgsWorkflow** crea nuove istanze dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.Workflow.

## Vedere anche

#### Ulteriori risorse

[Get-CsRgsWorkflow](get-csrgsworkflow.md)  
[Remove-CsRgsWorkflow](remove-csrgsworkflow.md)  
[Set-CsRgsWorkflow](set-csrgsworkflow.md)

