---
title: Migrazione da Office Communications Server 2007 R2 a Lync Server 2013
TOCTitle: Migrazione da Office Communications Server 2007 R2 a Lync Server 2013
ms:assetid: f3fa4f5f-e9a2-4fb7-a12d-20f04173e697
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205375(v=OCS.15)
ms:contentKeyID: 49302453
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Migrazione da Office Communications Server 2007 R2 a Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-19_

Negli argomenti di questa sezione viene illustrato il processo di migrazione da Office Communications Server 2007 R2 a Lync Server 2013.

> [!IMPORTANT]  
> Questo documento descrive i passaggi normalmente necessari per eseguire ogni fase della migrazione. Non sono descritti tutti gli scenari di migrazione o tutte le topologie di distribuzione legacy possibili. Per questo motivo, potrebbe non essere necessario eseguire tutti i passaggi descritti oppure potrebbero servirne altri, a seconda della distribuzione. Nel documento sono inoltre disponibili alcuni esempi dei passaggi di verifica, forniti allo scopo di illustrare quali aspetti ed elementi considerare per assicurarsi che ogni fase venga completata correttamente, man mano che si procede nella migrazione. Adattare tali passaggi di verifica allo specifico processo di migrazione.

Questa guida include informazioni specifiche per l'aggiornamento della distribuzione esistente e non spiega come modificare la topologia esistente. Non viene descritta l'implementazione delle nuove funzionalità. Se una procedura dettagliata è descritta altrove, in questa guida vengono forniti riferimenti al documento o alla sezione del documento appropriato.

Nel documento vengono utilizzati termini specifici, con le definizioni seguenti.

  - *migrazione*   
    Spostamento della distribuzione di produzione da una versione precedente di Office Communications Server 2007 R2 a Lync Server 2013.

<!-- end list -->

  - *aggiornamento*   
    Installazione di una versione più recente del software in un computer server o client.

<!-- end list -->

  - *coesistenza*   
    Ambiente temporaneo esistente durante la migrazione, quando è stata completata la migrazione di alcune funzionalità a Lync Server 2013 e altre rimangono ancora in una versione precedente di Office Communications Server 2007 R2.

<!-- end list -->

  - *interoperabilità*   
    Capacità della distribuzione di operare in modo corretto durante il periodo di coesistenza.

## Contenuto della sezione

  - [Operazioni preliminari alla migrazione](before-you-begin-the-migration_1.md)

  - [Fasi della migrazione](migration-phases_1.md)

  - [Fase 1: pianificare la migrazione da Office Communications Server 2007 R2](phase-1-plan-your-migration-from-office-communications-server-2007-r2.md)

  - [Fase 2: eseguire la preparazione per la migrazione](phase-2-prepare-for-migration_1.md)

  - [Fase 3: distribuire il pool pilota di Lync Server 2013](phase-3-deploy-lync-server-2013-pilot-pool_1.md)

  - [Fase 4: unire le topologie](phase-4-merge-topologies.md)

  - [Fase 5: configurare il pool pilota](phase-5-configure-the-pilot-pool.md)

  - [Fase 6: spostare gli utenti nel pool pilota](phase-6-move-users-to-the-pilot-pool.md)

  - [Fase 7: aggiungere server perimetrali Lync Server 2013 al pool pilota](phase-7-add-lync-server-2013-edge-server-to-pilot-pool.md)

  - [Fase 8: passare dalla distribuzione pilota alla produzione](phase-8-move-from-pilot-deployment-into-production.md)

  - [Fase 9: completare le attività successive alla migrazione](phase-9-complete-post-migration-tasks.md)

  - [Fase 10: rimuovere le autorizzazioni del sito legacy](phase-10-decommission-legacy-site.md)

