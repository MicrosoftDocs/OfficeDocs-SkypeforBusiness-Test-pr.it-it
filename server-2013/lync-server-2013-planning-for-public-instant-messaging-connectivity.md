---
title: Pianificazione della connettività per messaggistica istantanea pubblica
TOCTitle: Pianificazione della connettività per messaggistica istantanea pubblica
ms:assetid: e75e8884-05c7-414a-8014-bc9aa8126fb7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205349(v=OCS.15)
ms:contentKeyID: 49302316
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione della connettività per messaggistica istantanea pubblica

 

_**Ultima modifica dell'argomento:** 2013-10-07_

La connettività per messaggistica istantanea pubblica è una classe di federazione, configurata per consentire agli utenti interni ed esterni di Lync Server 2013 di aggiungere contatti dalle origini seguenti:

  - Contatti di Messenger

  - Contatti di Yahoo\!

  - Contatti di AOL (America Online)

> [!IMPORTANT]  
> <ul>
> <li><p>Dal 1 settembre 2012, la licenza di sottoscrizione utenti per la connettività di messaggistica istantanea pubblica di Microsoft Lync (PIC USL) non è più disponibile per l'acquisto per i nuovi contratti o quelli in fase di rinnovo. I clienti con licenze attive potranno continuare a eseguire la federazione con Yahoo! Messenger fino alla data di chiusura del servizio. Giugno 2014 è la data di fine servizio annunciata per Yahoo! e AOL. Per informazioni dettagliate, vedere <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Supporto della connettività per messaggistica istantanea pubblica in Lync Server 2013</a>.</p></li>
> 
> <li><p>La licenza PIC USL è una licenza di sottoscrizione di tipo mensile per utente, richiesta per la federazione di Lync Server o Office Communications Server con Yahoo! Messenger. La capacità di Microsoft di fornire questo servizio dipende dal supporto offerto da Yahoo! e il contratto sottostante non verrà rinnovato.</p></li>
> 
> 
> <li><p>Oggi più che mai, Lync è un potente strumento per la connessione tra diverse organizzazioni e con utenti di tutto il mondo. La federazione con Windows Live Messenger non richiede ulteriori licenze per utente/dispositivo in aggiunta alla licenza CAL Standard per Lync. La federazione con Skype verrà aggiunta all'elenco, consentendo agli utenti di Lync di raggiungere centinaia di milioni di utenti tramite messaggistica istantanea e la trasmissione vocale.</p></li></ul>


Per questa classe di federazione è necessario tenere conto delle considerazioni seguenti per la pianificazione:

  - Gli utenti di Windows Live Messenger possono condurre comunicazioni audio/video peer-to-peer con gli utenti di Lync Server 2013 oltre a conversazioni istantanee. I server perimetrali devono soddisfare requisiti specifici per porte e protocolli. Per informazioni dettagliate, vedere [Determinare i requisiti di porte e firewall A/V esterni per Lync Server 2013](lync-server-2013-determine-external-a-v-firewall-and-port-requirements.md)

  - Per la messaggistica istantanea di Yahoo non sono previsti requisiti speciali, a parte quelli in genere utilizzati per la pianificazione e la distribuzione del server perimetrale tipico per la federazione.

  - Per AOL è richiesto che il certificato del server perimetrale assegnato al servizio Access Edge sia configurato per l'utilizzo chiavi avanzato (EKU) client.

## Argomenti della sezione

  - [Riepilogo dei certificati - connettività per messaggistica istantanea pubblica](lync-server-2013-certificate-summary-public-instant-messaging-connectivity.md)

  - [Riepilogo delle porte - connettività per messaggistica istantanea pubblica](lync-server-2013-port-summary-public-instant-messaging-connectivity.md)

  - [Riepilogo di DNS - connettività per messaggistica istantanea pubblica](this-topic-is-no-longer-available.md)

