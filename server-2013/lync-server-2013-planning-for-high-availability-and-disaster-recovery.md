---
title: "Lync Server 2013: Pianifica disponibilità elevata e ripristino di emergenza"
TOCTitle: Pianificazione per la disponibilità elevata e il ripristino di emergenza
ms:assetid: 15a72073-0336-45dd-b2a0-35e7522c6000
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204703(v=OCS.15)
ms:contentKeyID: 49299781
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-10-31_

Come in Lync Server 2010, lo schema principale a disponibilità elevata per la maggior parte dei ruoli server di Lync Server 2013 si basa sulla ridondanza dei server tramite pooling. In caso di errore di un server che esegue un determinato ruolo, gli altri server del pool che eseguono lo stesso ruolo sopportano il carico del server in errore. Ciò vale per Front End Server, server perimetrali, Mediation Server e Director.

In Lync Server 2013 sono state introdotte nuove misure per il ripristino di emergenza dei pool Front End che prevedono la dispersione geografica dei server in due data center in modo da assicurare la continuazione del servizio in caso di inattività di un intero pool o sito.

Lync Server 2013 è stata inoltre migliorata la disponibilità elevata dei server back-end con il supporto del mirroring SQL sincrono dei database back-end.

In questa sezione vengono illustrate le principali funzionalità per disponibilità elevata e ripristino di emergenza e descritti i passaggi da effettuare per assicurare disponibilità elevata e ripristino di emergenza per gli altri ruoli server.

## Contenuto della sezione

  - [Ripristino di emergenza del pool Front End in Lync Server 2013](lync-server-2013-front-end-pool-disaster-recovery.md)

  - [Ripristino di emergenza dei server perimetrali in Lync Server 2013](lync-server-2013-edge-server-disaster-recovery.md)

  - [Pianificazione della resilienza di VoIP aziendale in Lync Server 2013](lync-server-2013-planning-for-enterprise-voice-resiliency.md)

  - [Funzionalità di gestione delle chiamate per il ripristino di emergenza in Lync Server 2013](lync-server-2013-call-management-features-for-disaster-recovery.md)

  - [Configurazione del server Chat persistente per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013](lync-server-2013-configuring-persistent-chat-server-for-high-availability-and-disaster-recovery.md)

  - [Resilienza di siti metropolitani di Lync Server 2010](lync-server-2013-compatibility-with-lync-server-2010-metropolitan-site-resiliency.md)

