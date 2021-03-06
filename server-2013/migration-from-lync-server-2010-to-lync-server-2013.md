﻿---
title: Migrazione da Lync Server 2010 a Lync Server 2013
TOCTitle: Migrazione da Lync Server 2010 a Lync Server 2013
ms:assetid: ef99d4a9-a666-4a92-9994-4d7930f70d55
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205369(v=OCS.15)
ms:contentKeyID: 49302414
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Migrazione da Lync Server 2010 a Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-17_

Negli argomenti di questa sezione viene illustrato il processo di migrazione da Lync Server 2010 a Lync Server 2013.

> [!IMPORTANT]  
> Questo documento descrive i passaggi normalmente necessari per eseguire ogni fase della migrazione. Non sono descritti tutti gli scenari di migrazione o tutte le topologie di distribuzione legacy possibili. Per questo motivo, potrebbe non essere necessario eseguire tutti i passaggi descritti oppure potrebbero servirne altri, a seconda della distribuzione. Nel documento sono inoltre disponibili alcuni esempi dei passaggi di verifica, forniti allo scopo di illustrare quali aspetti ed elementi considerare per assicurarsi che ogni fase venga completata correttamente, man mano che si procede nella migrazione. Adattare tali passaggi di verifica allo specifico processo di migrazione.

Questa guida include informazioni specifiche per l'aggiornamento della distribuzione esistente e non spiega come modificare la topologia esistente. Non viene descritta l'implementazione delle nuove funzionalità. Se una procedura dettagliata è descritta altrove, in questa guida vengono forniti riferimenti al documento o alla sezione del documento appropriato.

Nel documento vengono utilizzati termini specifici, con le definizioni seguenti.

  - *migrazione*   
    Spostamento della distribuzione di produzione da una versione precedente di Lync Server 2010 a Lync Server 2013.

<!-- end list -->

  - *aggiornamento*   
    Installazione di una versione più recente del software in un computer server o client.

<!-- end list -->

  - *coesistenza*   
    Ambiente temporaneo esistente durante la migrazione, quando è stata completata la migrazione di alcune funzionalità a Lync Server 2013 e altre rimangono ancora in una versione precedente di Lync Server 2010.

<!-- end list -->

  - *interoperabilità*   
    Capacità della distribuzione di operare in modo corretto durante il periodo di coesistenza.

## Contenuto della sezione

  - [Operazioni preliminari alla migrazione](before-you-begin-the-migration.md)

  - [Fase 1: pianificare la migrazione da Lync Server 2010](phase-1-plan-your-migration-from-lync-server-2010.md)

  - [Fase 2: eseguire la preparazione per la migrazione](phase-2-prepare-for-migration.md)

  - [Fase 3: distribuire il pool pilota di Lync Server 2013](phase-3-deploy-lync-server-2013-pilot-pool.md)

  - [Fase 4: spostare gli utenti di prova nel pool pilota](phase-4-move-test-users-to-the-pilot-pool.md)

  - [Fase 5: aggiungere server perimetrali Lync Server 2013 al pool pilota](phase-5-add-lync-server-2013-edge-server-to-pilot-pool.md)

  - [Fase 6: passare dalla distribuzione pilota alla produzione](phase-6-move-from-pilot-deployment-into-production.md)

  - [Fase 7: completare le attività successive alla migrazione](phase-7-complete-post-migration-tasks.md)

  - [Fase 8: rimuovere le autorizzazioni dei pool legacy](phase-8-decommission-legacy-pools.md)

