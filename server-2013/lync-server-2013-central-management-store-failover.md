---
title: "Lync Server 2013: Failover dell'archivio di gestione centrale"
TOCTitle: Failover dell'archivio di gestione centrale
ms:assetid: f464d715-68a4-462c-9584-00f41ab10db0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205376(v=OCS.15)
ms:contentKeyID: 49302458
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Failover dell'archivio di gestione centrale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-18_

L' archivio di gestione centrale include dati di configurazione relativi ai server e ai servizi nella distribuzione di Lync 2013. Offre un meccanismo di archiviazione schematizzata più stabile per i dati necessari alla definizione, impostazione, manutenzione, amministrazione, descrizione e attività di una distribuzione di Lync 2013. Convalida inoltre i dati per garantire la coerenza della configurazione.

Ogni distribuzione di Lync include un archivio di gestione centrale ospitato dal server back-end di un pool Front End.

Quando si stabilisce un abbinamento di pool che include il pool che ospita l' archivio di gestione centrale, viene configurato un database archivio di gestione centrale di backup nel pool di backup e i servizi dell' archivio di gestione centrale vengono installati in entrambi i pool. In qualsiasi momento, uno dei due database dell' archivio di gestione centrale è il master attivo e l'altro è in standby. Il contenuto viene replicato dal servizio di backup dal master attivo in quello in standby.

Durante un failover del pool che coinvolge i pool che ospitano archivio di gestione centrale, l'amministratore deve eseguire il failover dell' archivio di gestione centrale prima di eseguire il failover del pool Front End.

Una volta superata la situazione di emergenza, non è necessario eseguire il failback dell' archivio di gestione centrale. Dopo il ripristino, l' archivio di gestione centrale nel pool di backup può rimanere attivo.

Gli obiettivi di progettazione per il failover dell' archivio di gestione centrale sono 5 minuti per l'obiettivo del tempo di ripristino (RTO) e 5 minuti per l'obiettivo del punto di ripristino (RPO).

