---
title: Fasi della migrazione
TOCTitle: Fasi della migrazione
ms:assetid: cb7747ba-b872-42ca-ab41-76e3c4e77d06
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205336(v=OCS.15)
ms:contentKeyID: 49302000
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Fasi della migrazione

 

_**Ultima modifica dell'argomento:** 2012-09-17_

In Lync Server 2013 vengono definiti siti di rete contenenti componenti di Lync Server 2013. Un sito è un insieme di computer connessi tramite una rete ad alta velocità e a bassa latenza, ad esempio una singola rete locale (LAN) o due reti connesse tramite una rete in fibra ottica ad alta velocità.

Un *pool Front End* è un gruppo di Front End Server configurati in modo identico che collaborano per offrire servizi a un gruppo comune di utenti. Un pool garantisce scalabilità e funzionalità di failover per gli utenti. Ogni server in un pool deve eseguire uno o più ruoli del server identici. Anche un server Standard Edition, progettato per le organizzazioni di piccole dimensioni, definisce un pool e viene eseguito in un singolo server. In questo modo è possibile disporre delle funzionalità di Lync Server 2013 con costi minori, ma non di usufruire di una vera e propria soluzione a disponibilità elevata.

Nelle fasi seguenti viene descritto il processo della migrazione di un pool da Lync Server 2010 a Lync Server 2013. Nel caso di più siti che includono più pool, per ogni singolo pool sarà necessario adottare questo approccio in più fasi.

1.  [Fase 1: pianificare la migrazione da Lync Server 2010](phase-1-plan-your-migration-from-lync-server-2010.md)

2.  [Fase 2: eseguire la preparazione per la migrazione](phase-2-prepare-for-migration.md)

3.  [Fase 3: distribuire il pool pilota di Lync Server 2013](phase-3-deploy-lync-server-2013-pilot-pool.md)

4.  [Fase 4: spostare gli utenti di prova nel pool pilota](phase-4-move-test-users-to-the-pilot-pool.md)

5.  [Fase 5: aggiungere server perimetrali Lync Server 2013 al pool pilota](phase-5-add-lync-server-2013-edge-server-to-pilot-pool.md)

6.  [Fase 6: passare dalla distribuzione pilota alla produzione](phase-6-move-from-pilot-deployment-into-production.md)

7.  [Fase 7: completare le attività successive alla migrazione](phase-7-complete-post-migration-tasks.md)

8.  [Fase 8: rimuovere le autorizzazioni dei pool legacy](phase-8-decommission-legacy-pools.md)

