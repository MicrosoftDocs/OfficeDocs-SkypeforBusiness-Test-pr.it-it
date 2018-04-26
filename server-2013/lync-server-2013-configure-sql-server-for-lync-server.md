---
title: 'Lync Server 2013: Configurare SQL Server per Lync Server'
TOCTitle: Configurare SQL Server per Lync Server 2013
ms:assetid: 375e5cc4-e436-46dc-9b02-5063f35cdcc1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425848(v=OCS.15)
ms:contentKeyID: 49300172
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare SQL Server per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-08-12_

Gli argomenti di questa sezione riguardano la distribuzione e la configurazione di SQL Server per consentirne l'uso in una distribuzione Enterprise di Lync Server. I server Standard Edition usano una versione SQL Server Express collocata di SQL Server le cui dimensioni sono appropriate per i carichi di lavoro di un server Standard Edition.

L' archivio di gestione centrale di Lync Server 2013 include in un pool tutti i dati utente di tutti i server Enterprise Edition ed è stato progettato per essere collocato in un server back-end basato su SQL Server. In quanto archivio centralizzato, l' archivio di gestione centrale non può essere installato nello stesso computer di altri ruoli di Lync Server 2013. L' archivio di gestione centrale non può risiedere in un server Enterprise Edition nel pool. L' archivio di gestione centrale viene creato automaticamente quando si pubblica la topologia per la prima volta e si sceglie di creare i database. Per consentire la corretta installazione, nel computer che si designa come server back-end deve già essere già in esecuzione il software di database SQL Server.

## Argomenti della sezione

  - [Posizionamento dei file di log e dei file di dati di SQL Server per Lync Server 2013](lync-server-2013-sql-server-data-and-log-file-placement.md)

  - [Configurare SQL Server in Lync Server 2013](lync-server-2013-configure-sql-server.md)

  - [Autorizzazioni di distribuzione per SQL Server in Lync Server 2013](lync-server-2013-deployment-permissions-for-sql-server.md)

  - [Installazione di database mediante Lync Server Management Shell in Lync Server 2013](lync-server-2013-database-installation-using-lync-server-management-shell.md)

  - [Informazioni sui requisiti del firewall per SQL Server con Lync Server 2013](lync-server-2013-understanding-firewall-requirements-for-sql-server.md)

  - [Configurare il clustering di SQL Server per Lync Server 2013](lync-server-2013-configure-sql-server-clustering.md)

