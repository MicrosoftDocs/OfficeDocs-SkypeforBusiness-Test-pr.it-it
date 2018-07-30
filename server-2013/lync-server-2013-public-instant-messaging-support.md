---
title: 'Lync Server 2013: Supporto per la messaggistica istantanea pubblica'
TOCTitle: Supporto per la messaggistica istantanea pubblica
ms:assetid: 1f45163b-52c6-4a78-b9c8-dfe3abe4e5eb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204732(v=OCS.15)
ms:contentKeyID: 49299889
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supporto per la messaggistica istantanea pubblica in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-10-07_

Lync Server 2013 supporta l'uso di provider di connettività di messaggistica istantanea pubblici con licenza, nonché l'uso del protocollo XMPP (eXtensible Messaging and Presence Protocol) per implementare un tipo speciale di federazione che consente a Lync Server di accedere ai partner di dominio XMPP configurati utilizzando il client Lync 2013.

## Supporto del provider di connettività di messaggistica istantanea pubblica

I partner di connettività di messaggistica istantanea pubblici attualmente supportati sono:

  - America Online

  - Windows Live

  - Yahoo\!

Per le comunicazioni con gli utenti di Windows Live, Lync Server 2013 supporta la messaggistica istantanea peer-to-peer e chiamate audio e video. Per le comunicazioni con AOL e Yahoo\!, Lync Server 2013 supporta la messaggistica istantanea peer-to-peer. Potrebbe essere necessaria una licenza separata.

> [!IMPORTANT]  
> <ul>
> <li><p>Dal 1 settembre 2012, la licenza di sottoscrizione utenti per la connettività di messaggistica istantanea pubblica di Microsoft Lync (&quot;PIC USL&quot;) non è più disponibile per l'acquisto per i nuovi contratti o quelli in fase di rinnovo. I clienti con licenze attive potranno continuare a eseguire la federazione con Yahoo! Messenger fino alla data di chiusura del servizio. Giugno 2014 è la data di fine servizio annunciata per Yahoo! e AOL. Per informazioni dettagliate, vedere <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Supporto della connettività per messaggistica istantanea pubblica in Lync Server 2013</a>.</p></li>
> 
> <li><p>La licenza PIC USL è una licenza di sottoscrizione di tipo mensile per utente, richiesta per la federazione di Lync Server o Office Communications Server con Yahoo! Messenger. La capacità di Microsoft di fornire questo servizio dipende dal supporto offerto da Yahoo! e il contratto sottostante è in fase di chiusura.</p></li>
> 
> 
> <li><p>Oggi più che mai, Lync è un potente strumento per la connessione tra diverse organizzazioni e con utenti di tutto il mondo. La federazione con Windows Live Messenger non richiede ulteriori licenze per utente/dispositivo in aggiunta alla licenza CAL Standard per Lync. La federazione con Skype verrà aggiunta a questo elenco, consentendo agli utenti di Lync di raggiungere centinaia di milioni di persone tramite messaggistica istantanea e comunicazioni vocali.</p></li></ul>


## Supporto della federazione XMPP

La federazione XMPP supporta la comunicazione degli utenti di Lync con gli utenti di dominio XMPP configurati che usano un provider pubblico, ad esempio GTalk. Le comunicazioni con questi utenti può includere:

  - Messaggistica istantanea peer-to-peer e presenza

  - Creazione di contatti federati XMPP nel client Lync

