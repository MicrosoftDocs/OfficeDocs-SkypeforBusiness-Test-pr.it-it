---
title: Configurazione del server di gestione principale
TOCTitle: Configurazione del server di gestione principale
ms:assetid: 44e2e9a8-c130-4c66-9871-80b1ff11b27c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204844(v=OCS.15)
ms:contentKeyID: 49300372
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione del server di gestione principale

 

_**Ultima modifica dell'argomento:** 2014-03-19_

Per sfruttare al massimo le nuove funzionalità di monitoraggio dell'integrità in Microsoft Lync Server 2013, gli amministratori devono prima scegliere un computer da utilizzare come server di gestione principale. In tale computer è necessario innanzitutto installare System Center Operations Manager 2007 R2 o System Center Operations Manager 2012. Occorre inoltre installare una versione supportata di SQL Server da utilizzare come database back-end di Operations Manager. Se è installato System Center Operations Manager 2012, è possibile utilizzare una delle versioni seguenti di SQL Server come database back-end:

  - SQL Server 2008 R2 Service Pack 1

  - SQL Server 2008 R2 Service Pack 2

Se si utilizza System Center Operations Manager 2007 R2, è consigliabile installare SQL Server 2005 Service Pack 4 o SQL Server 2008 Service Pack 3. È anche possibile utilizzare SQL Server 2008 R2 come database back-end per System Center Operations Manager 2007 R2. Vedere l'appendice 1 di questa documentazione per ulteriori informazioni su come configurare SQL Server 2008 R2 per funzionare con System Center Operations Manager 2007 R2.

Quando si installa System Center Operations Manager 2012 o System Center Operations Manager 2007 R2, è necessario installare tutti i componenti del prodotto, inclusi i seguenti:

  - Database operativo

  - Server

  - Console

  - Cmdlet di Windows PowerShell

  - Console Web

  - Report

  - Data warehouse

Questi componenti e la relativa installazione non verranno esaminati in dettaglio in questo documento. Per informazioni dettagliate su System Center Operations Manager 2007 R2, vedere la documentazione di Operations Manager 2007 R2 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=257526\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=257526%26clcid=0x410) e la documentazione di System Center Operations Manager 2012 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=257527\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=257527%26clcid=0x410). Seguire tali istruzioni se si intende utilizzare SQL Server 2005 o SQL Server 2008 Service Pack 1 come database back-end.

Se è installato System Center Operations Manager 2012, è possibile utilizzare SQL Server 2012 come database back-end. Per informazioni dettagliate su SQL Server 2012, vedere la documentazione online di SQL Server 2012 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=257528\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=257528%26clcid=0x410).

Tenere presente che per ogni distribuzione di Lync Server deve essere presente un solo server di gestione primario. Inoltre, anche se è possibile usare System Center Operations Manager 2012 o System Center Operations Manager 2007 R2, non è possibile eseguire le due applicazioni contemporaneamente: è necessario scegliere l'una o l'altra. Se ad esempio si esegue System Center Operations Manager 2012, anche tutti gli agenti di System Center devono eseguire System Center Operations Manager 2012. Non è consentito che alcuni agenti eseguano System Center Operations Manager 2012 mentre altri eseguono System Center Operations Manager 2007 R2.

