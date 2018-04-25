---
title: 'Lync Server 2013: Componenti e topologie per il monitoraggio'
TOCTitle: Componenti e topologie per il monitoraggio
ms:assetid: c1bb36b0-1fb8-4d8e-9cc9-9bef740fe3c6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412952(v=OCS.15)
ms:contentKeyID: 49887736
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Componenti e topologie per il monitoraggio in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-05_

Poiché gli agenti di raccolta dati unificata vengono installati e attivati automaticamente in ogni Front End Server, non è necessario configurare un server in modo che operi come Monitoring Server. Ogni Front End Server infatti già funziona come Monitoring Server. È tuttavia necessario installare e configurare un database che operi come archivio dati back-end per i dati di monitoraggio. Microsoft Lync Server 2013 può utilizzare uno qualsiasi dei database seguenti come archivio back-end per il monitoraggio:

  - Microsoft SQL Server 2008 R2 Enterprise Edition

  - Microsoft SQL Server 2008 R2 Standard Edition

  - Microsoft SQL Server 2012 Enterprise Edition

  - Microsoft SQL Server 2012 Standard Edition

Si noti che è necessario utilizzare le versioni a 64 bit di questi database. Le versioni a 32 bit di SQL Server non possono essere utilizzate come archivio back-end per il monitoraggio. Allo stesso modo, Lync Server 2013 non supporta Server 2008 Express Edition o SQL Server 2012 Express Edition. Per ulteriori informazioni sui requisiti di database per Lync Server 2013, vedere l'argomento [Supporto per il software di database in Lync Server 2013](lync-server-2013-database-software-support.md) nella documentazione relativa al supporto di Lync Server 2013.

Tenere presente che SQL Server deve essere installato e configurato prima di distribuire e configurare il monitoraggio. È tuttavia necessario distribuire solo SQL Server, senza dover installare i database di monitoraggio in anticipo. Tali database verranno invece creati automaticamente durante la pubblicazione della topologia di Lync Server.

I dati di monitoraggio possono condividere un'istanza di SQL Server con altri tipi di dati. Il database di registrazione dettagli chiamata (LcsCdr) e il database della qualità percepita dagli utenti (QoEMetrics) in genere condividono la stessa istanza SQL. È inoltre comune che due database di monitoraggio si trovino nella stessa istanza SQL utilizzata dal database di archiviazione (LcsLog). L'unico reale requisito per le istanze di SQL Server è il fatto che ogni istanza di SQL Server sia limitata a quanto segue:

  - Un'istanza del database back-end di Lync Server 2013. Come regola generale, non è consigliabile che il database di monitoraggio sia collocato nella stessa istanza SQL, o persino nello stesso computer, del database back-end. Benché questo sia tecnicamente possibile, si rischia che il database di monitoraggio utilizzi lo spazio su disco necessario al database back-end.

  - Un'istanza del database di registrazione dettagli chiamata.

  - Un'istanza del database della qualità percepita dagli utenti.

  - Un'istanza del database di archiviazione.

In altri termini, non è possibile avere due istanze del database LcsCdr nella stessa istanza di SQL Server. Se sono necessarie più istanze del database LcsCdr, configurare più istanze di SQL Server.

## Vedere anche

#### Ulteriori risorse

[Distribuzione del monitoraggio in Lync Server 2013](lync-server-2013-deploying-monitoring.md)

