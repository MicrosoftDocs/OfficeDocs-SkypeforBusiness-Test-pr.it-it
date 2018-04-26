---
title: 'Lync Server 2013: Requisiti di sistema per SQL Server'
TOCTitle: Requisiti di sistema per SQL Server
ms:assetid: 9c235085-cbfa-4e9e-9cec-3f5749039a6b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205112(v=OCS.15)
ms:contentKeyID: 49301472
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti di sistema per SQL Server in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-10-25_

Prima di distribuire il server Enterprise Edition, installare Microsoft SQL Server 2008 R2 o Microsoft SQL Server 2012 su un computer dedicato che soddisfi i requisiti hardware. Per informazioni dettagliate sui requisiti hardware, vedere [Piattaforme hardware server per Lync Server 2013](lync-server-2013-server-hardware-platforms.md) nella documentazione sulla supportabilità. Per informazioni dettagliate sui requisiti software, vedere [Supporto per il software di database in Lync Server 2013](lync-server-2013-database-software-support.md) nella documentazione sulla supportabilità. Per informazioni sulle autorizzazioni necessarie per la distribuzione, vedere [Autorizzazioni di distribuzione per SQL Server in Lync Server 2013](lync-server-2013-deployment-permissions-for-sql-server.md).

Per creare il pool Front End, è anche necessario configurare Windows Firewall per consentire a Lync Server 2013 di accedere a SQL Server su specifiche porte definendo queste ultime per il server mediante Gestione configurazione SQL Server e aprendole in Windows Firewall con sicurezza avanzata.

