---
title: Set-CsAnnouncement
TOCTitle: Set-CsAnnouncement
ms:assetid: 286cb990-844e-4b87-bdaf-4a75456d8c60
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425752(v=OCS.15)
ms:contentKeyID: 49299993
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAnnouncement

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica i valori delle proprietà di un annuncio Lync Server esistente. Gli annunci vengono riprodotti quando gli utenti compongono un numero di telefono valido, ma non assegnato. Un annuncio può corrispondere a un messaggio (ad esempio "Il numero è temporaneamente fuori servizio") o a un segnale di occupato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsAnnouncement [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsAnnouncement [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AudioFilePrompt <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Language <String>] [-Name <String>] [-TargetUri <String>] [-TextToSpeechPrompt <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 consente di assegnare un nuovo file audio all'annuncio Help Desk Announcement. Per eseguire questa operazione, il comando utilizza per prima cosa il cmdlet **Get-CsAnnouncement**, senza parametri, per restituire una raccolta di tutti gli annunci attualmente disponibili. Questa raccolta viene quindi inviata al cmdlet **Where-Object**, che seleziona l'unico annuncio in cui Name equivale a (-eq) "Help Desk Announcement". A sua volta, l'annuncio viene inviato al cmdlet **Set-CsAnnouncement**, che imposta il valore della proprietà AudioFilePrompt su helpdesk.wav.

Se a questo annuncio è già assegnato un valore TextToSpeechPrompt, il comando genera un avviso che segnala che il valore TextToSpeechPrompt sarà ignorato.

    Get-CsAnnouncement | Where-Object {$_.Name -eq "Help Desk Announcement"} | Set-CsAnnouncement -AudioFilePrompt "helpdesk.wav"

## ESEMPIO 2

Con l'esempio 2, la proprietà TextToSpeechPrompt per l'annuncio Help Desk Announcement viene impostata su un valore null; in questo modo viene cancellato il valore della proprietà. Per eseguire questa operazione, il comando utilizza per prima cosa il cmdlet **Get-CsAnnouncement** per restituire una raccolta di tutti gli annunci attualmente disponibili. Questa raccolta viene quindi inviata al cmdlet **Where-Object**, che seleziona l'annuncio in cui Name equivale a (-eq) "Help Desk Announcement". L'annuncio viene quindi inviato al cmdlet **Set-CsAnnouncement**, che imposta il valore della proprietà TextToSpeechPrompt su un valore null ($Null).

    Get-CsAnnouncement | Where-Object {$_.Name -eq "Help Desk Announcement"} | Set-CsAnnouncement -TextToSpeechPrompt $Null

## ESEMPIO 3

Con questo esempio viene aggiornato TargetUri per l'annuncio denominato Help Desk Announcement. Il comando utilizza per prima cosa il cmdlet **Get-CsAnnouncement** per restituire una raccolta di tutti gli annunci attualmente disponibili. Questa raccolta viene quindi inviata al cmdlet **Where-Object**, che seleziona l'annuncio in cui Name equivale a (-eq) "Help Desk Announcement". L'annuncio viene quindi inviato al cmdlet **Set-CsAnnouncement**, che imposta il valore della proprietà TargetUri su un percorso di segreteria telefonica (sip:kmyer@litwareinc.com;opaque=app:voicemail).

    Get-CsAnnouncement | Where-Object {$_.Name -eq "Help Desk Announcement"} | Set-CsAnnouncement -TargetUri "sip:kmyer@litwareinc.com;opaque=app:voicemail"

## Descrizione dettagliata

Un'organizzazione può disporre di numeri telefonici non assegnati a utenti o telefoni, ma che sono tuttora numeri validi per le chiamate. Per impostazione predefinita, quando un utente compone uno di questi numeri riceve un segnale di occupato e la chiamata può generare un errore restituito al client SIP. Applicando le impostazioni di annuncio ai numeri non assegnati, gli amministratori possono decidere di riprodurre un messaggio, restituire un segnale di occupato o reindirizzare la chiamata. Questo cmdlet consente di modificare queste impostazioni di annuncio.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsAnnouncement** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsAnnouncement"}

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
<td><p>String</p></td>
<td><p>Il nome del file audio da riprodurre per l'annuncio. I file audio vengono memorizzati in Archivio file. Per salvare i file audio in Archivio file, utilizzare il cmdlet <strong>Import-CsAnnouncementFile</strong>.</p>
<p>Tipi di file validi: WAV e WMA</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Un identificatore univoco per l'annuncio. Questo valore sarà sempre nel formato &lt;serviceID&gt;/&lt;GUID&gt;, dove serviceID è l'identità del server applicazioni che esegue il servizio Annuncio e GUID è un identificatore univoco globale associato a queste impostazioni di annuncio. Ad esempio: ApplicationServer:redmond.litwareinc.com/bef5fa3b-3c97-4af0-abe7-611deee7616c.</p>
<p>Dal momento che può essere difficile immettere correttamente i GUID nella riga di comando, è più comodo recuperare gli annunci utilizzando il cmdlet <strong>Get-CsAnnouncement</strong> e inviarli tramite pipe al cmdlet <strong>Set-CsAnnouncement</strong> per la modifica. Per informazioni dettagliate, vedere la sezione Esempi.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Announcement</p></td>
<td><p>Un riferimento all'oggetto annuncio da modificare. Questo oggetto deve essere di tipo Microsoft.Rtc.Management.WritableConfig.Settings.AnnouncementServiceSettings.Announcement e può essere recuperato chiamando il cmdlet <strong>Get-CsAnnouncement</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Language</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>La lingua in cui sarà riprodotto il prompt di sintesi vocale. Se viene immesso un valore per TextToSpeechPrompt, questo parametro è obbligatorio.</p>
<p>I valori sono immessi come stringa e rappresentano la lingua e le impostazioni locali da utilizzare. Di seguito viene fornito un elenco dei valori validi, seguiti dalla lingua e dalle impostazioni locali tra parentesi: ca-ES (catalano, Spagna); da-DK (danese, Danimarca); de-DE (tedesco, Germania); en-AU (inglese, Australia); en-CA (inglese, Canada); en-GB (inglese, Regno Unito); en-IN (inglese, India); en-US (inglese, Stati Uniti); es-ES (spagnolo, Spagna); es-MX (spagnolo, Messico); fi-FI (finlandese, Finlandia); fr-CA (francese, Canada); fr-FR (francese, Francia); it-IT (italiano, Italia); ja-JP (giapponese, Giappone); ko-KR (coreano, Corea); nb-NO (norvegese, Bokmal, Norvegia); nl-NL (olandese, Paesi Bassi); pl-PL (polacco, Polonia); pt-BR (portoghese, Brasile); pt-PT (portoghese, Portogallo); ru-RU (russo, Russia); sv-SE (svedese, Svezia); zh-CN (cinese, Repubblica popolare cinese); zh-HK (cinese, Hong Kong - R.A.S.); zh-TW (cinese, Taiwan).</p></td>
</tr>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Immettere un valore per questo parametro per modificare il nome dell'annuncio. I nomi devono essere univoci all'interno di un servizio.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'URI a cui sarà trasferito il chiamante dopo la riproduzione dell'annuncio. Questo valore deve essere un indirizzo SIP immesso nel formato sip: seguito dall'indirizzo SIP. Ad esempio, sip:kmyer@litwareinc.com. Si noti che l'indirizzo SIP può anche essere un numero di telefono o di segreteria telefonica, ad esempio sip:+14255551212@litwareinc.com;user=phone per un numero di telefono o sip:kmyer@litwareinc.com;opaque=app:voicemail per una segreteria telefonica.</p></td>
</tr>
<tr class="odd">
<td><p><em>TextToSpeechPrompt</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Un prompt per sintesi vocale (TTS). Questa è una stringa che verrà convertita in audio e riprodotta come annuncio.</p>
<p>Se vengono specificati entrambi AudioFilePrompt e TextToSpeechPromp per un singolo annuncio, si verrà avvisati che il file audio avrà la precedenza e il file TTS verrà ignorato.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.AnnouncementServiceSettings.Announcement. Consente di accettare l'input da pipeline di oggetti annuncio.

## Tipi restituiti

Il cmdlet **Set-CsAnnouncement** non restituisce oggetti o valori. Il cmdlet modifica invece le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.AnnouncementServiceSettings.Announcement.

## Vedere anche

#### Ulteriori risorse

[New-CsAnnouncement](new-csannouncement.md)  
[Remove-CsAnnouncement](remove-csannouncement.md)  
[Get-CsAnnouncement](get-csannouncement.md)  
[Import-CsAnnouncementFile](import-csannouncementfile.md)

