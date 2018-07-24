---
title: 'Lync Server 2013: Definizione dei requisiti per Front End Server, messaggistica istantanea e presenza'
TOCTitle: Definizione dei requisiti per Front End Server, messaggistica istantanea e presenza
ms:assetid: c21198bc-520c-4d17-8b84-7ff1475b9b0a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412956(v=OCS.15)
ms:contentKeyID: 49301862
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definizione dei requisiti per Front End Server, messaggistica istantanea e presenza in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-10-07_

L'attività principale di pianificazione per la messaggistica istantanea e la presenza consiste nel verificare di disporre di Front End Server sufficienti per gli utenti.

## Abilitazione delle comunicazioni con utenti esterni

È possibile aumentare notevolmente i vantaggi dell'investimento in  Lync Server consentendo agli utenti di comunicare con utenti esterni. Gli utenti esterni possono essere:

  - **Utenti remoti**   Utenti dell'organizzazione che lavorano all'esterno dei firewall utilizzando computer portatili o altri dispositivi di Lync Server.

  - **Utenti federati**   Utenti di società con cui si collabora, che utilizzano anch'essi Lync Server. Per consentire agli utenti di mettersi facilmente in contatto con questi utenti, si creano relazioni federate con le relative società.

  - **Utenti pubblici**   Utenti di servizi di messaggistica istantanea pubblica, come i servizi offerti dalle reti di servizi Internet Windows Live, da Yahoo\! e AOL, nonché utenti di provider e server che utilizzano il protocollo XMPP (Extensible Messaging and Presence Protocol), come Google Talk.
    

    > [!NOTE]
    > Si noti che potrebbe essere necessaria una licenza separata per la connettività a servizi di messaggistica istantanea pubblica con Windows Live, AOL e Yahoo!

    
    > [!important]  
    > <ul>    
> <li><p>Dal 1 settembre 2012, la licenza di sottoscrizione utenti per la connettività di messaggistica istantanea pubblica di Microsoft Lync (“PIC USL”) non è più disponibile per l'acquisto per i nuovi contratti o quelli in fase di rinnovo. I clienti con licenze attive potranno continuare a eseguire la federazione con Yahoo! Messenger fino alla data di chiusura del servizio. Giugno 2014 è la data di fine servizio annunciata per Yahoo! e AOL. Per informazioni dettagliate, vedere <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Supporto della connettività per messaggistica istantanea pubblica in Lync Server 2013</a>.</p></li>    
> 
> <li><p>La licenza PIC USL è una licenza di sottoscrizione di tipo mensile per utente, richiesta per la federazione di Lync Server o Office Communications Server con Yahoo! Messenger. La capacità di Microsoft di fornire questo servizio dipende dal supporto offerto da Yahoo! e il contratto sottostante è in fase di chiusura.</p></li>    
> 
> 
> <li><p>Oggi più che mai, Lync è un potente strumento per la connessione tra diverse organizzazioni e con utenti di tutto il mondo. La federazione con Windows Live Messenger non richiede ulteriori licenze per utente/dispositivo in aggiunta alla licenza CAL Standard per Lync. La federazione con Skype verrà aggiunta a questo elenco, consentendo agli utenti di Lync di raggiungere centinaia di milioni di persone tramite messaggistica istantanea e comunicazioni vocali.</p></li>    </ul>


Per abilitare qualsiasi scenario tra questi oppure tutti, è necessario distribuire un server perimetrale per consentire comunicazioni sicure tra la distribuzione di Lync Server e gli utenti esterni. Gli utenti remoti dell'organizzazione e gli utenti di organizzazioni federate potranno vedere le reciproche informazioni sulla presenza e comunicare tramite messaggistica istantanea. Per informazioni dettagliate sull'abilitazione delle comunicazioni con utenti esterni, vedere [Pianificazione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-planning-for-external-user-access.md) nella documentazione relativa alla pianificazione.

## Archiviazione del contenuto della messaggistica istantanea

Lync Server offre funzionalità utili nel caso l'organizzazione sia tenuta a rispettare regolamentazioni di conformità. È possibile utilizzare l'archiviazione per archiviare il contenuto dei messaggi istantanei per tutti gli utenti nell'organizzazione o solo per particolari utenti specificati. Per informazioni dettagliate, vedere [Pianificazione dell'archiviazione in Lync Server 2013](lync-server-2013-planning-for-archiving.md) nella documentazione relativa alla pianificazione.

Se è stato distribuito anche Microsoft Exchange Server 2013, è possibile integrare l'archiviazione dei dati di Exchange con l'archiviazione dei dati di Lync Server e utilizzare un unico strumento per eseguire ricerche in entrambi i tipi di dati archiviati. Per ulteriori informazioni, vedere [Configurazione di Microsoft Lync Server 2013 per l'utilizzo dell'archiviazione di Microsoft Exchange Server 2013](configuring-lync-server-2013-to-use-microsoft-exchange-server-2013-archiving.md).

