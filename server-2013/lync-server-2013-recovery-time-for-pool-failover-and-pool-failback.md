---
title: 'Lync Server 2013: Tempo di ripristino per il failover e il failback dei pool'
TOCTitle: Tempo di ripristino per il failover e il failback dei pool
ms:assetid: 902c658f-8442-4d0d-b3ad-bf795ecd550d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205079(v=OCS.15)
ms:contentKeyID: 49301312
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tempo di ripristino per il failover e il failback dei pool in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-10_

Per il failover e il failback dei pool, l'obiettivo tecnico relativo al tempo di ripristino è di 30 minuti. Si tratta del tempo necessario per l'esecuzione del failover dopo che gli amministratori hanno determinano l'esistenza di un'emergenza e hanno avviato le procedure di failover. Non include il tempo necessario agli amministratori per valutare la situazione e prendere decisioni né quello impiegato dagli utenti per ripetere l'accesso dopo il completamento del failover.

Per il failover e il failback del pool, l'obiettivo tecnico relativo al punto di ripristino è pari a 30 minuti. Questo valore rappresenta la misura temporale dei dati che potrebbero essere persi a causa dell'emergenza, in virtù della latenza della replica del servizio di backup. Se ad esempio un pool diventa inattivo alle 10.00 e l'obiettivo relativo al punto di ripristino è di 30 minuti, i dati scritti nel pool tra le 9.30 e le 10.00 potrebbero non essere stati replicati nel pool di backup e pertanto essere perduti.

Tutti i numeri degli obiettivi relativi al tempo e al punto di ripristino riportati in questo documento presuppongono che i due data center si trovino nella medesima area geografica con trasporto ad alta velocità e bassa latenza tra i siti. I valori sono misurati per un pool con 40.000 utenti attivi simultaneamente e 200.000 utenti abilitati per Lync in relazione a un modello utente predefinito in cui non esiste backlog nella replica dei dati. Le cifre sono soggette a modifiche a seconda dei test e della convalida delle prestazioni.

