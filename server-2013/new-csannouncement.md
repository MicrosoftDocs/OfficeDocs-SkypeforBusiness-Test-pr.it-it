---
title: New-CsAnnouncement
TOCTitle: New-CsAnnouncement
ms:assetid: 6e3699c6-cd2b-4842-99bc-3cf2578fbd65
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398522(v=OCS.15)
ms:contentKeyID: 49300915
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsAnnouncement

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo annuncio di Lync Server. Gli annunci vengono riprodotti quando gli utenti compongono un numero di telefono valido ma non assegnato. Un annuncio può essere rappresentato da un messaggio, ad esempio "Questo numero è momentaneamente fuori servizio", oppure da un segnale di occupato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsAnnouncement -Parent <String> <COMMON PARAMETERS>

    New-CsAnnouncement -Identity <XdsIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -Name <String> [-AudioFilePrompt <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Language <String>] [-TargetUri <String>] [-TextToSpeechPrompt <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

L'Esempio 1 dimostra come creare un nuovo annuncio che riprodurrà un prompt TTS in English (U.S.). Il primo parametro specificato è l'identità. L'identità deve essere in ambito di servizio, seguita dal ID del servizio dell'Application Server (ApplicationServer:redmond.litwareinc.com). Successivamente viene assegnato all'annuncio un nome, in questo caso Help Desk Announcement. Per assegnare un prompt TTS a questo annuncio viene utilizzato il parametro TextToSpeechPrompt seguito da una stringa con il testo dell'annuncio. Quando viene utilizzato un prompt TTS per un annuncio, si deve specificare una lingua includendo il parametro Language seguito da una stringa che rappresenta U.S. English (en-US).

Si noti che l'identità dell'annuncio e composta da due parti: il servizio su cui l'annuncio viene memorizzato e un identificatore univoco globale (GUID) di 36 caratteri. L'identità completa di un nuovo annuncio sarà visibile solo dopo la sua creazione, il GUID viene generato ed applicato automaticamente. L'identità sarà simile a questa: service:ApplicationServer:redmond.litwareinc.com/1951f734-c80f-4fb2-965d-51807c792b90.

    New-CsAnnouncement -Identity ApplicationServer:redmond.litwareinc.com -Name "Help Desk Announcement" -TextToSpeechPrompt "Welcome to the Help Desk." -Language "en-US"

## ESEMPIO 2

L'Esempio 2 è simile all'Esempio 1 nel quale si iniziava immettendo i parametri obbligatori, Identity e Name. In questo esempio, tuttavia, al posto di un prompt TTS, come annuncio si vuole riprodurre un file audio. Per fare ciò si include il parametro AudioFilePrompt e gli si fornisce una stringa contenente il nome del file audio (WelcomeMessage.wav). Per essere riprodotto nell'annuncio, il file deve essere memorizzato in Archivio file. Per aggiungere file audio in Archivio file utilizzare il cmdlet **Import-CsAnnouncementFile**.

    New-CsAnnouncement -Identity ApplicationServer:redmond.litwareinc.com -Name "Welcome Announcement" -AudioFilePrompt "WelcomeMessage.wav"

## ESEMPIO 3

Come nell'Esempio 2, in questo esempio viene creato un annuncio che riproduce un file audio quando viene chiamato un numero. In questo esempio, tuttavia, in aggiunta ai parametri Identity, Name e AudioFilePrompt viene anche specificato il parametro TargetUri. A questo parametro viene fornito il SIP URI dell'utente o del telefono a cui il chiamante verrà inoltrato dopo la riproduzione dell'annuncio.

    New-CsAnnouncement -Identity ApplicationServer:redmond.litwareinc.com -Name "Forward Announcement" -AudioFilePrompt "WelcomeMessage.wav" -TargetUri sip:kmyer@litwareinc.com

## ESEMPIO 4

L'Esempio 4 è identico all'Esempio 3 con la differenza che invece di inoltrare la chiamata basandosi sull'indirizzo SIP di un utente, la chiamata viene inoltrata ad un numero di telefono.

    New-CsAnnouncement -Identity ApplicationServer:redmond.litwareinc.com -Name "Forward Announcement" -AudioFilePrompt "WelcomeMessage.wav" -TargetUri "sip:+14255551212@litwareinc.com;user=phone"

## ESEMPIO 5

In questo esempio non viene specificato né un prompt né un URI di destinazione, vengono inclusi solo Identity e Name. Ciò significa che il chiamante udrà un segnale di occupato quando chiamerà un numero non assegnato associato a questo annuncio.

    New-CsAnnouncement -Identity ApplicationServer:redmond.litwareinc.com -Name "Busy"

## Descrizione dettagliata

Una organizzazione può possedere numeri che non sono associati a utenti o telefoni ma sono numeri validi e che possono essere chiamati. Per impostazione predefinita quando qualcuno chiama uno di quei numeri riceverà il segnale di occupato e la chiamata può dare come risultato un errore che viene restituito al client SIP. Applicando le impostazioni di annuncio ai numeri non assegnati, gli amministratori hanno l'opportunità di riprodurre un annuncio, restituire un segnale di occupato o reindirizzare la chiamata. Questo cmdlet crea queste impostazioni di annuncio.

È possibile assegnare annunci ai numeri non assegnati utilizzando il cmdlet **New-CsUnassignedNumber** o **Set-CsUnassignedNumber**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsAnnouncement** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsAnnouncement"}

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
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Un identificatore univoco per l'annuncio. Per questo valore si deve immettere l'identità dell'Application Server sul quale è in esecuzione l'applicazione Response Group. Ad esempio, ApplicationServer:redmond.litwareinc.com.</p>
<p>Ad un singolo servizio si possono assegnare più di un annuncio. Perciò, per rendere l'identità un valore univoco verrà automaticamente generato un identificatore univoco globale (GUID) che verrà assegnato all'identità quando si crea l'annuncio. Il nuovo annuncio avrà l'identità nel formato service:&lt;service ID&gt;/&lt;GUID&gt;. Ad esempio: service: ApplicationServer:redmond.litwareinc.com/bef5fa3b-3c97-4af0-abe7-611deee7616c. Non è necessario fornire un GUID quando si utilizza questo cmdlet. Fornire invece l'identità di servizio e il GUID verrà automaticamente generato e aggiunto all'identità.</p>
<p>Non è necessario fornire un GUID ma è possibile farlo. Potrebbe essere necessario se era stato assegnato un annuncio ad un intervallo di numeri non assegnati, poi l'annuncio è stato eliminato. È possibile creare un nuovo annuncio con una identità corrispondente (incluso il GUID) ed in quel caso non è necessario aggiornare l'intervallo di numeri non assegnati.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Un nome descrittivo per l'annuncio. Questo nome deve essere univoco all'interno del servizio. Questo nome verrà utilizzato con il cmdlet <strong>New-CsUnassignedNumber</strong> o <strong>Set-CsUnassignedNumber</strong> per specificare l'annuncio associato a un intervallo di numeri non assegnati.</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Questo parametro è identico a Identity, eccetto che Identity accetterà l'identità del servizio e il GUID, laddove Parent accetterà solo l'identità del servizio e genererà automaticamente il GUID. Non è possibile specificare sia Identity sia Parent.</p></td>
</tr>
<tr class="even">
<td><p><em>AudioFilePrompt</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome del file audio da riprodurre per l'annuncio. I file audio vengono memorizzati in Archivio file. Per salvare i file audio in Archivio file, utilizzare il cmdlet <strong>Import-CsAnnouncementFile</strong>.</p>
<p>Tipi di file validi: WAV e WMA</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>Language</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>La lingua nella quale verrà riprodotto il prompt TTS. Questo parametro è necessario se viene immesso un valore in TextToSpeechPrompt.</p>
<p>I valori sono immessi come stringa e rappresentano la lingua e le impostazioni locali da utilizzare. Di seguito viene fornito un elenco dei valori validi, seguiti dalla lingua e dalle impostazioni locali tra parentesi: ca-ES (catalano, Spagna); da-DK (danese, Danimarca); de-DE (tedesco, Germania); en-AU (inglese, Australia); en-CA (inglese, Canada); en-GB (inglese, Regno Unito); en-IN (inglese, India); en-US (inglese, Stati Uniti); es-ES (spagnolo, Spagna); es-MX (spagnolo, Messico); fi-FI (finlandese, Finlandia); fr-CA (francese, Canada); fr-FR (francese, Francia); it-IT (italiano, Italia); ja-JP (giapponese, Giappone); ko-KR (coreano, Corea); nb-NO (norvegese, Bokmal, Norvegia); nl-NL (olandese, Paesi Bassi); pl-PL (polacco, Polonia); pt-BR (portoghese, Brasile); pt-PT (portoghese, Portogallo); ru-RU (russo, Russia); sv-SE (svedese, Svezia); zh-CN (cinese, Repubblica popolare cinese); zh-HK (cinese, Hong Kong - R.A.S.); zh-TW (cinese, Taiwan).</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>L'URI (Uniform Resource Identifier) a cui verrà trasferito il chiamante dopo la riproduzione dell'annuncio. Questo valore deve essere un indirizzo SIP immesso nel formato sip: seguito dall'indirizzo SIP. Ad esempio, sip:kmyer@litwareinc.com. Si noti che l'indirizzo SIP può anche essere un numero di telefono, ad esempio sip:+14255551212@litwareinc.com;user=phone per un numero di telefono o sip:kmyer@litwareinc.com;opaque=app:voicemail per una casella vocale.</p></td>
</tr>
<tr class="even">
<td><p><em>TextToSpeechPrompt</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Un prompt per sintesi vocale (TTS). Questa è una stringa che verrà convertita in audio e riprodotta come annuncio.</p>
<p>Se vengono specificati entrambi AudioFilePrompt e TextToSpeechPromp per un singolo annuncio, si verrà avvisati che il file audio avrà la precedenza e il file TTS verrà ignorato.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Consente di creare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.AnnouncementServiceSettings.Announcement.

## Vedere anche

#### Ulteriori risorse

[Remove-CsAnnouncement](remove-csannouncement.md)  
[Set-CsAnnouncement](set-csannouncement.md)  
[Get-CsAnnouncement](get-csannouncement.md)  
[Import-CsAnnouncementFile](import-csannouncementfile.md)  
[New-CsUnassignedNumber](new-csunassignednumber.md)  
[Set-CsUnassignedNumber](set-csunassignednumber.md)

