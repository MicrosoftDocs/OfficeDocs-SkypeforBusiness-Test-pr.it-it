---
title: 'Lync Server 2013: Caratteristiche e funzionalità di Front End Server, messaggistica istantanea e presenza'
TOCTitle: Caratteristiche e funzionalità di Front End Server, messaggistica istantanea e presenza
ms:assetid: 05b29536-dcd7-49b5-934a-2ebf20ddc45c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398109(v=OCS.15)
ms:contentKeyID: 49299556
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Caratteristiche e funzionalità di Front End Server, messaggistica istantanea e presenza in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-03-17_

I Front End Server forniscono la maggior parte delle funzionalità di Lync Server. Sono disponibili due edizioni, Lync Server Enterprise Edition, progettato principalmente per le organizzazioni di grandi dimensioni, e Lync Server Standard Edition, progettato principalmente per le piccole organizzazioni che desiderano un investimento in hardware più contenuto e non hanno bisogno della disponibilità elevata. Entrambe le edizioni supportano tutti i carichi di lavoro di Lync Server, compresi messaggistica istantanea, presenza, conferenze e VoIP aziendale.

La messaggistica istantanea consente agli utenti di comunicare tra loro in tempo reale mediante i loro computer con messaggi di testo. Sono supportate le sessioni di messaggistica istantanea sia tra due che tra più parti. Un partecipante a una conversazione di messaggistica istantanea tra due parti può aggiungere un terzo partecipante in qualsiasi momento. In tal caso, la finestra relativa alla conversazione cambia in modo da supportare le funzionalità di conferenza.

> [!IMPORTANT]  
> Una comunicazione uno-a-uno tra un client di Lync e un client di Communicator viene spesso denominata peer-to-peer. Tecnicamente i due client comunicano mediante una conversazione uno-a-uno con l'unità IMMCU (Instant Messaging Multipoint Control Unit) nel mezzo. IMMCU è un componente di Front End Server. Se si posiziona IMMCU nel flusso di lavoro necessario per la comunicazione, è possibile utilizzare la registrazione dettagli chiamata e altre caratteristiche abilitate da Front End Server. La comunicazione avviene da una porta di origine dinamica sul client alla porta TLS/TCP/5061 di Front End Server, purché venga utilizzata la crittografia TLS (Transport Layer Security) consigliata. Per impostazione predefinita, la comunicazione peer-to-peer, così come la messaggistica istantanea con più partecipanti, è possibile solo se Lync Server e IMMCU sono attivi e disponibili.

La *presenza* fornisce informazioni sullo stato di altri utenti presenti sulla rete. Lo stato di presenza di un utente fornisce informazioni che aiutano altri utenti a decidere se tentare di contattarlo e se utilizzare la messaggistica istantanea, il telefono o la posta elettronica. La presenza induce a scegliere la comunicazione istantanea ma, segnalando anche se un utente è in riunione o fuori ufficio, consente di capire quando la comunicazione istantanea non può essere utilizzata. Tale stato di presenza viene visualizzato con un'apposita icona in Lync e in altre applicazioni che supportano questa funzionalità, inclusi il client di messaggistica e collaborazione Microsoft Outlook, le tecnologie SharePoint, Microsoft Word e il software per fogli di calcolo Microsoft Excel. L'icona della presenza rappresenta la volontà di comunicare e la disponibilità corrente dell'utente.

