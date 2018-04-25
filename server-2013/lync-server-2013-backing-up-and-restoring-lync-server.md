---
title: Backup e ripristino di Lync Server 2013
TOCTitle: Backup e ripristino di Lync Server 2013
ms:assetid: 07dc1f5e-af66-4e18-bf39-881dceff8bc3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh202160(v=OCS.15)
ms:contentKeyID: 52062089
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Backup e ripristino di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

In questa sezione vengono illustrate le procedure consigliate per eseguire il backup dei dati di Lync Server 2013 e per ripristinarli in caso di problemi. Tali procedure consigliate si applicano alle situazioni seguenti:

  - Un intero pool di Lync Server di qualsiasi tipo (Front End Server, server perimetrale, Mediation Server, server Chat persistente o Server Director) o un singolo server in uno di questi pool.

  - Il server di gestione centrale

  - Un server Standard Edition

  - Un server back-endEnterprise Edition

  - Un Archivio file

  - Un database di archiviazione, database di monitoraggio o database chat persistente

In questa sezione non sono incluse informazioni sul ripristino di un intero sito o per lo sviluppo di un sito di standby. Per informazioni sullo sviluppo di una soluzione di ripristino di emergenza con pool Front End accoppiati, vedere [Pianificazione per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md). Questo è il metodo consigliato per la pianificazione di un ripristino di emergenza.

Se sono stati distribuiti pool Front End accoppiati, se si verificano errori irreversibili in uno dei due pool, è possibile ripristinarlo con un nuovo nome di dominio completo (FQDN) dal pool accoppiato. Per informazioni dettagliate sulle procedure per eseguire il ripristino, vedere [Failover di un pool in Lync Server 2013](lync-server-2013-failing-over-a-pool.md). Inoltre, se successivamente si desidera ricreare un pool con errori irreversibili che faceva parte di una coppia di pool Front End, è possibile utilizzare le procedure in [Esecuzione del failover del pool ABC front-end](lync-server-2013-performing-an-abc-front-end-pool-failover.md).

Per la metodologia illustrata in questo documento sono previste considerazioni speciali durante la fase di pianificazione. Per informazioni dettagliate, vedere [Definizione di un piano di backup e ripristino](lync-server-2013-establishing-a-backup-and-restoration-plan.md).

## Argomenti della sezione

  - [Preparazione per il backup e il ripristino di Lync Server](lync-server-2013-preparing-for-lync-server-backup-and-restoration.md)

  - [Backup di dati e impostazioni](lync-server-2013-backing-up-data-and-settings.md)

  - [Ripristino di dati e impostazioni](lync-server-2013-restoring-data-and-settings.md)

  - [Fogli di lavoro per il backup e il ripristino](lync-server-2013-backup-and-restoration-worksheets.md)

