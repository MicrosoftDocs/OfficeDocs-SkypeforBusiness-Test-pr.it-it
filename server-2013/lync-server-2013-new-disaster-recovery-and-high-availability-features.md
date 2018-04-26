---
title: 'Lync Server 2013: Nuove funzionalità per la disponibilità elevata e il ripristino di emergenza'
TOCTitle: Nuove funzionalità per la disponibilità elevata e il ripristino di emergenza
ms:assetid: 4fa7cd0f-784b-4d3f-b839-432c2ecaf7c1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204892(v=OCS.15)
ms:contentKeyID: 49300507
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Nuove funzionalità per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-20_

Come in Lync Server 2010, lo schema principale di disponibilità elevata (HA, High Availability) per Lync Server 2013 si basa sulla ridondanza dei server tramite pool. Se in un server che esegue un ruolo specifico si verifica un errore, gli altri server del pool con lo stesso ruolo ricevono il carico del server con l'errore. Questo avviene per i Front End Server, i server perimetrali, i Mediation Server e i Director.

Lync Server 2013 aggiunge nuove misure per il ripristino di emergenza, consentendo di abbinare pool Front End situati in due data center diversi. Se uno dei pool abbinati non è più disponibile, per consentire la continuazione del servizio un amministratore può eseguire il failover degli utenti di questo pool all'altro pool della coppia. Questa funzionalità non richiede soluzioni di rete o hardware costose, ad esempio reti di archiviazione o dischi condivisi.

Lync Server 2013 offre inoltre funzionalità di disponibilità elevata dei server back-end. Si tratta di una topologia facoltativa in cui vengono distribuiti due server back-end per un pool Front End e viene configurato il mirroring SQL sincrono per tutti i database Lync in esecuzione sui server back-end. È possibile scegliere se distribuire o meno un server di controllo per il mirror.

## Vedere anche

#### Concetti

[Pianificazione per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md)

