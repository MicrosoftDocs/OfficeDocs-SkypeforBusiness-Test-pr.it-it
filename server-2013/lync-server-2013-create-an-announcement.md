---
title: 'Lync Server 2013: Creare un annuncio'
TOCTitle: Creare un annuncio
ms:assetid: a6fd5922-fe46-41ba-94e3-c76b1101a31b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412783(v=OCS.15)
ms:contentKeyID: 49301572
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare un annuncio in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Per creare un nuovo annuncio, è necessario eseguire la procedura seguente:

1.  Per i messaggi audio, registrare il file audio mediante l'applicazione di registrazione audio preferita.

2.  Per i messaggi audio, eseguire il cmdlet **Import-CsAnnouncementFile** per importare il contenuto del file audio nell'archivio file.

3.  Eseguire il cmdlet **New-CsAnnouncement** per creare l'annuncio e assegnargli un nome. Eseguire questo passaggio per creare annunci con un messaggio audio o un messaggio di sintesi vocale (TTS) oppure senza alcun messaggio.
    
    > [!TIP]  
    > È possibile creare un annuncio senza messaggio, ad esempio se si desidera trasferire le chiamate a una destinazione specifica senza riprodurre un messaggio.

4.  Assegnare il nuovo annuncio a un intervallo di numeri della tabella di numeri non assegnati.

In questo argomento viene descritto come importare e creare annunci. Per informazioni dettagliate sull'assegnazione di annunci nella tabella dei numeri non assegnati, vedere [Configurare la tabella dei numeri non assegnati in Lync Server 2013](lync-server-2013-configure-the-unassigned-number-table.md).

## Per creare un nuovo annuncio

1.  Per i messaggi audio, creare il file audio.

2.  Accedere al computer in cui è installata Lync Server Management Shell come membro del gruppo RTCUniversalServerAdmins oppure con i diritti utente necessari, come descritto in [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

3.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

4.  Per i messaggi audio eseguire:
    
        Import-CsAnnouncementFile -Parent <service of the Application Server running the Announcement application> -FileName <name for file in File Store> -Content Byte [<contents of file in byte array>]

5.  Eseguire:
    
        New-CsAnnouncement -Parent <service of Application Server running the Announcement application, in the form: service:ApplicationServer:<fqdn>> -Name <unique name to be used as destination in unassigned number table> [-AudioFilePrompt <FileName specified in Import-CsAnnouncementFile>] [-TextToSpeechPrompt <text string to be converted to speech>] [-Language <Language for playing the TTS prompt (required for PromptTts)>] [-TargetUri sip:SIPAddress for transferring caller after announcement]
    
    Per trasferire le chiamate alla segreteria telefonica, digitare SIPAddress nel formato sip:nomeutente@nomedominio;opaque=app:voicemail (ad esempio, sip:francesco@contoso.com;opaque=app:voicemail). Per trasferire le chiamate a un numero di telefono, digitare SIPAddress nel formato sip:numero@nomedominio;user=phone (ad esempio, sip:+ 14255550121@contoso.com;user=phone).
    
    Ad esempio, per specificare un messaggio audio:
    
        $a = Get-Content ".\PromptFile.wav" -ReadCount 0 -Encoding Byte
        Import-CsAnnouncementFile -Parent service:ApplicationServer:pool0@contoso.com -FileName "ChangedNumberMessage.wav" -Content $a
        New-CsAnnouncement -Parent service:ApplicationServer:pool0.contoso.com -Name "Number Changed Announcement" -AudioFilePrompt "ChangedNumberMessage.wav"
    
    Ad esempio, per specificare un messaggio di sintesi vocale:
    
        New-CsAnnouncement -Parent service:ApplicationServer:pool0.contoso.com -Name "Help Desk Announcement" -TextToSpeechPrompt "The Help Desk number has changed. Please dial 5550100." -Language "en-US"
    
    Per ulteriori informazioni su questi cmdlet e per visualizzare l'elenco dei codici di lingua da utilizzare nel parametro **TextToSpeechPrompt**, vedere [New-CsAnnouncement](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsAnnouncement).

## Vedere anche

#### Ulteriori risorse

[Import-CsAnnouncementFile](https://docs.microsoft.com/en-us/powershell/module/skype/Import-CsAnnouncementFile)  
[New-CsAnnouncement](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsAnnouncement)  
[Configurare la tabella dei numeri non assegnati in Lync Server 2013](lync-server-2013-configure-the-unassigned-number-table.md)

