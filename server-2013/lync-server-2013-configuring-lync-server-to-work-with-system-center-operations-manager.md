---
title: Configurazione di Lync Server per l'utilizzo con System Center Operations Manager
TOCTitle: Configurazione di Lync Server per l'utilizzo con System Center Operations Manager
ms:assetid: b55a24ab-648b-4142-b3cd-3792860ba872
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205188(v=OCS.15)
ms:contentKeyID: 49301731
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di Lync Server per l'utilizzo con System Center Operations Manager

 

_**Ultima modifica dell'argomento:** 2012-10-22_

Per configurare l'infrastruttura di Microsoft Lync Server 2013 in modo che funzioni con System Center Operations Manager, è necessario eseguire tre attività:

  - Identificare e configurare il server di gestione primario di System Center Operations Manager. Tale configurazione include l'installazione di System Center Operations Manager 2012 o System Center Operations Manager 2007 R2 e l'impostazione di un database back-end con SQL Server. L'effettiva versione di SQL Server da utilizzare dipende dalla versione di System Center Operations Manager in uso. Per ulteriori informazioni, vedere [Configurazione del server di gestione principale](lync-server-2013-configuring-the-primary-management-server.md).

  - Identificare e configurare i computer Lync Server che si desidera monitorare. Per monitorare un computer Lync Server utilizzando System Center Operations Manager, è necessario installare i file dell'agente System Center Operations Manager e configurare ogni server in modo che operi come proxy.

  - Identificare e configurare i computer che devono fungere da *nodi Watcher* di Lync Server. Tali nodi sono computer che eseguono periodicamente le transazioni sintetiche di Lync Server, le quali sono cmdlet di Windows PowerShell che verificano che i componenti chiave di Lync Server, come la possibilità di eseguire l'accesso al sistema o di scambiare messaggi istantanei, stiano funzionando come previsto.

Negli argomenti di questa sezione sono contenute le istruzioni per eseguire ognuna di queste attività.

## Contenuto della sezione

  - [Configurazione del server di gestione principale](lync-server-2013-configuring-the-primary-management-server.md)

  - [Installazione dei Management Pack di Lync Server 2013](lync-server-2013-installing-the-lync-server-2013-management-packs.md)

  - [Configurazione del computer Lync Server da monitorare](lync-server-2013-configuring-the-lync-server-computers-that-will-be-monitored.md)

  - [Installazione e configurazione dei nodi Watcher](lync-server-2013-installing-and-configuring-watcher-nodes.md)

