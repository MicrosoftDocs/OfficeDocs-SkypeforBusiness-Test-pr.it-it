---
title: Rimuovere database e istanze di SQL Server nel server back-end
TOCTitle: Rimuovere database e istanze di SQL Server nel server back-end
ms:assetid: 32457df9-7dd9-4fca-9362-ea4de26b0296
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688016(v=OCS.15)
ms:contentKeyID: 49887510
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rimuovere database e istanze di SQL Server nel server back-end

 

_**Ultima modifica dell'argomento:** 2012-10-19_

È possibile rimuovere i database e le istanze di Microsoft SQL Server dopo aver rimosso i relativi server dipendenti che eseguono Lync Server 2010 o dopo aver riconfigurato i server che eseguono Lync Server 2010 per l'uso di un altro database. È necessario eseguire la procedura descritta in questo argomento quando si disattiva il database SQL Server corrente o si riconfigura il server corrente che esegue Lync Server 2010 in modo da rendere i database obsoleti o non disponibili.

Per rimuovere i database o le istanze per il server di archiviazione o Monitoring Server, è innanzitutto necessario rimuovere il ruolo server. Analogamente, per rimuovere le istanze o i database per il pool Front End, è innanzitutto necessario rimuovere o riconfigurare il ruolo server dipendente. Per queste procedure non viene fatta distinzione tra database collocati o istanze separate dei server. La collocazione dei database non incide sulle procedure.

## Argomenti della sezione

  - [Rimuovere il database di SQL Server per un pool Front End](remove-the-sql-server-database-for-a-front-end-pool.md)

  - [Rimuovere il database di SQL Server per un server Monitoring Server](remove-the-sql-server-database-for-a-monitoring-server.md)

  - [Rimuovere il database di SQL Server per un server di archiviazione](remove-the-sql-server-database-for-an-archiving-server.md)

