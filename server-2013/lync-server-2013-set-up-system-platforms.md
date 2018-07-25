---
title: 'Lync Server 2013: Configurare le piattaforme del sistema'
TOCTitle: Configurare le piattaforme del sistema
ms:assetid: 2e72e49d-2737-4b5b-8c0a-60f6ecb15bf1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204783(v=OCS.15)
ms:contentKeyID: 49300054
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare le piattaforme del sistema in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

Prima di iniziare la distribuzione del server Chat persistente, è necessario installare nell'hardware il sistema operativo richiesto per soddisfare i requisiti di sistema dei server:

Per informazioni dettagliate sull'hardware supportati per i server che eseguono Lync Server 2013, server di database e file server, vedere [Hardware supportato per Lync Server 2013](lync-server-2013-supported-hardware.md) nella documentazione relativa alla supportabilità. Per informazioni dettagliate sul software di database e sui sistemi operativi supportati, vedere [Supporto dell'infrastruttura e del software server in Lync Server 2013](lync-server-2013-server-software-and-infrastructure-support.md) nella documentazione relativa alla supportabilità. Per informazioni dettagliate sui requisiti di aggiornamento di Windows, vedere [Requisiti e supporto per i server aggiuntivi in Lync Server 2013](lync-server-2013-additional-server-support-and-requirements.md) nella documentazione relativa alla supportabilità.

Il Front End Server del server Chat persistente, **PersistentChatService**, può essere distribuito su uno o più computer autonomi in un pool di Lync Server 2013Enterprise Edition. Non può essere collocato sui Front End Server del Lync ServerEnterprise Edition. server Chat persistente può essere distribuito dal programma di avvio automatico, come altri ruoli di Lync Server. Il **Chat persistente Web Services for File Upload/Download** e il **Chat persistente Web Services for Chat Room Management** sono componenti Web distribuiti nei Front End Server di Lync Server 2013.

Un singolo Front End Server di server Chat persistente può supportare 20.000 utenti attivi. È possibile disporre di un pool di server Chat persistente con un massimo di 4 front end attivi che supportano un totale di 80.000 utenti concorrenti. Il server back-end di Chat persistente, **PersistentChatStore**, archivia le chat room e le categorie. È consigliabile installare il **PersistentChatStore** in un server back-end di SQL Server dedicato nel pool di Enterprise Edition, anche se la collocazione del server back-end di Lync Server 2013 e di **PersistentChatStore** nella stessa istanza di SQL Server è supportata.

Se l'organizzazione richiede il supporto per la conformità, è possibile installarlo usando Generatore di topologie. Il servizio di conformità di server Chat persistente viene installato nello stesso computer del Front End Server di server Chat persistente. Per motivi di conformità è richiesto un database separato. Per informazioni dettagliate sui requisiti di conformità per server Chat persistente, vedere [Pianificazione del server Chat persistente in Lync Server 2013](lync-server-2013-planning-for-persistent-chat-server.md) nella documentazione relativa alla pianificazione.

Ogni topologia richiede almeno un server con Lync Server 2013 installato e un server con il software di database SQL Server installato. Generatore di topologie supporta più pool di server Chat persistente. Per la distribuzione di più pool di server Chat persistente attenersi alle istruzioni valide per qualsiasi pool riportate nell'argomento [Distribuzione di Lync Server 2013](lync-server-2013-deploying-lync-server.md) della documentazione relativa alla distribuzione.

È anche possibile distribuire server Chat persistente con Lync Server 2013Standard Edition. In questo caso, il Front End Server**PersistentChatService** viene collocato sul Server Standard Edition ed è possibile distribuire il server back-end**PersistentChatStore** nell'istanza locale di SQL Server Express.

> [!important]  
> Non è disponibile il supporto di server Chat persistenteStandard Edition per la disponibilità elevata, in quanto le prestazioni e la scala risulterebbero limitati. Inoltre, sono supportate solo le nuove distribuzioni del Server Standard Edition di server Chat persistente e non è supportato l'aggiornamento di un Group Chat Server di Lync Server 2010 a un server Chat persistenteStandard Edition di Lync Server 2013.

## Vedere anche

#### Concetti

[Requisiti e supporto per i server aggiuntivi in Lync Server 2013](lync-server-2013-additional-server-support-and-requirements.md)  

#### Ulteriori risorse

[Hardware supportato per Lync Server 2013](lync-server-2013-supported-hardware.md)  
[Supporto dell'infrastruttura e del software server in Lync Server 2013](lync-server-2013-server-software-and-infrastructure-support.md)  
[Pianificazione del server Chat persistente in Lync Server 2013](lync-server-2013-planning-for-persistent-chat-server.md)  
[Distribuzione di Lync Server 2013](lync-server-2013-deploying-lync-server.md)

