---
title: 'Lync Server 2013: Abilitazione della connettività Lync-Skype'
TOCTitle: Abilitazione della connettività Lync-Skype
ms:assetid: 34c4db3e-582f-41fb-85c4-3438ae02f09f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn440170(v=OCS.15)
ms:contentKeyID: 59602748
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitazione della connettività Lync-Skype in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-12-16_

Dopo aver inviato la richiesta di provisioning, è possibile concentrarsi sull'ambiente di Lync Server e le attività amministrative necessarie per configurare la connettività Lync-Skype. Le informazioni in questa sezione partono dal presupposto che l'amministratore di Lync Server abbia distribuito Lync Server e configurato l'accesso esterno. Per ulteriori informazioni sulla configurazione dell'accesso esterno per Lync Server, vedere [Pianificazione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-planning-for-external-user-access.md) e [Distribuzione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-deploying-external-user-access.md).

Per preparare l'ambiente di Lync Server per la connettività Lync-Skype, l'amministratore di Lync Server deve eseguire le tre attività seguenti:

## 1\. Configurare federazione e PIC

La federazione è obbligatoria per consentire agli utenti di Skype di comunicare con quelli di Lync all'interno dell'organizzazione. Il servizio PIC (Public Instant Messaging Connectivity) è una classe di federazione e deve essere configurato per consentire agli utenti di Lync di comunicare con quelli di Skype. I servizi di federazione e PIC possono essere configurati tramite il Pannello di controllo di Lync Server, illustrato di seguito.

![Visualizzazione di PIC](images/Dn440170.451b94e3-0b38-488c-835f-1f25690e8074(OCS.15).jpg "Visualizzazione di PIC")

> [!important]  
> La federazione PIC non è più supportata da Live Communication Server 2005 SP1 o da Office Communications Server 2007. Le piattaforme supportate per la federazione PIC includono Lync Server 2013, Lync Server 2010 e Office Communications Server 2007 R2.

## 2\. Configurare almeno un criterio per il supporto dell'accesso utente federato

Un amministratore deve usare il Pannello di controllo di Lync Server per configurare uno o più criteri di accesso per gli utenti esterni per stabilire se gli utenti di Skype possono collaborare con utenti interni di Lync Server.

![Criteri](images/Dn440170.8fd46ad1-9749-422c-8c47-c16ac9032cdb(OCS.15).jpg "Criteri")

## 3\. Configurare l'impostazione per Lync del provider PIC di Skype

Un amministratore deve usare Lync Server Management Shell per configurare i criteri client di Lync per la visualizzazione di Skype come provider PIC aggiuntivo.


> [!NOTE]
> Gli utenti dei provider di servizi PIC (Public Instant Messaging Connectivity) non possono partecipare alle conferenze audio o video o alla messaggistica istantanea nell'organizzazione finché non si procede anche alla configurazione di almeno un criterio per il supporto della connettività di messaggistica istantanea pubblica (passaggio 2 di questa procedura).



1.  Per configurare i servizi di federazione e PIC, vedere "Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica" all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=306063](http://go.microsoft.com/fwlink/p/?linkid=306063).

2.  Per configurare almeno un criterio per il supporto dell'accesso utente federato, vedere "Configurare criteri per controllare l'accesso degli utenti pubblici" all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=306064](http://go.microsoft.com/fwlink/p/?linkid=306064).

**Per modificare un provider PIC di Messenger PIC e configurarlo per Skype**

1.  Aprire Lync Server Management Shell da un Lync Server Front End Server.

2.  Eseguire i due comandi seguenti:
    
    `Remove-CsPublicProvider -Identity Messenger`
    
    `New-CsPublicProvider -Identity Skype -ProxyFqdn federation.messenger.msn.com -IconUrl "https://images.edge.messenger.live.com/Messenger_16x16.png" -VerificationLevel 2 -Enabled 1`

3.  Da un client Lync client adesso è possibile selezionare Skype come provider PIC e aggiungere un client Skype specificando il relativo account Microsoft. Inoltre, un utente Skype che ha eseguito l'unione e l'accesso con l'account Microsoft può inviare richieste di contatto agli utenti Lync. Per altre informazioni sugli account Microsoft, vedere [Cos'è un account Microsoft?](https://support.skype.com/it/faq/fa12059/what-is-a-microsoft-account). Per informazioni aggiuntive sull'aggiunta dei client a Lync, vedere [Uso della connettività Lync-Skype in Lync Server 2013 come utente finale](lync-server-2013-using-lync-skype-connectivity-as-an-end-user.md).
    
    ![Aggiungere un contatto Skype](images/Dn440170.df0e6ed9-2374-4dfa-a815-87281989487c(OCS.15).jpg "Aggiungere un contatto Skype")

4.  Per informazioni dettagliate sulla modifica dei provider ospitati, vedere "Creare o modificare provider federati SIP ospitati" all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=306065](http://go.microsoft.com/fwlink/p/?linkid=306065).

Sono così completate le attività amministrative da eseguire nel server per impostare la configurazione necessaria per la connettività Lync-Skype.

