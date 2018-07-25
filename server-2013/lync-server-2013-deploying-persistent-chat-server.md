---
title: 'Lync Server 2013: Distribuzione del server Chat persistente'
TOCTitle: Distribuzione del server Chat persistente
ms:assetid: e3b930fb-6855-47f0-b6b3-7dfae386540d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205357(v=OCS.15)
ms:contentKeyID: 49302278
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuzione del server Chat persistente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-03-31_

Il server Chat persistente di Lync Server 2013 fa parte dell'infrastruttura di Lync Server 2013.

Per la distribuzione del server Chat persistente è necessario:

  - Utilizzare Generatore di topologie per definire, importare e successivamente pubblicare la topologia e i componenti che si desidera distribuire.

  - Preparare l'ambiente per la distribuzione dei componenti del server Chat persistente.

  - Installare e configurare i componenti del server Chat persistente per la distribuzione.

Il server Chat persistente è disponibile con Lync Server 2013Enterprise Edition come pool separato (non collocato con Enterprise EditionFront End Server). Per il server Chat persistente è necessario un server back-end di SQL Server nel pool di Enterprise Edition per archiviare il contenuto delle chat room e altri metadati rilevanti. È consigliabile installare **PersistentChatStore** in un server back-end di SQL Server dedicato, sebbene sia supportata la collocazione del server back-endLync Server 2013 e **PersistentChatStore** nella stessa istanza di SQL Server.

È inoltre possibile distribuire il server Chat persistente con Lync Server 2013Standard Edition. In questo caso, **PersistentChatService**Front End Server è collocato nel computer Standard Edition e il server back-end**PersistentChatStore** può essere distribuito nell'istanza di SQL Server Express locale.

Per informazioni dettagliate sule configurazioni di collocazione supportate, vedere [Collocazione di server supportata in Lync Server 2013](lync-server-2013-supported-server-collocation.md).

> [!important]  
> La disponibilità elevata non è supportata per server Chat persistenteStandard Edition. Prestazioni e scalabilità saranno limitate, Sono inoltre supportati solo server Chat persistenteserver Standard Edition nuovi. Non è supportato l'aggiornamento da Lync Server 2010, Group Chat Server a un server Chat persistente di Lync Server 2013Standard Edition.

Se l'organizzazione richiede il supporto della conformità, è possibile installare il servizio di conformità del server Chat persistente nel server Chat persistenteFront End Server. Per la conformità è necessario un database separato.

Ogni topologia richiede almeno un server in cui sia installato Lync Server 2013 e un server in cui sia installato il software di database SQL Server.

Utilizzare Generatore di topologie per aggiungere un server Chat persistente alle distribuzioni di Lync Server 2013. È possibile scegliere di aggiungere uno o più pool di server Chat persistente tramite Generatore di topologie. Seguire le stesse istruzioni per la distribuzione di più pool di server Chat persistente valide per qualsiasi pool. Per informazioni dettagliate, vedere [Distribuzione di Lync Server 2013](lync-server-2013-deploying-lync-server.md) nella documentazione relativa alla distribuzione.

Per informazioni dettagliate sulle topologie disponibili e sui requisiti tecnici e software per l'installazione di server Chat persistente, vedere [Pianificazione del server Chat persistente in Lync Server 2013](lync-server-2013-planning-for-persistent-chat-server.md) nella documentazione relativa alla pianificazione, [Funzionamento del server chat persistente in Lync Server 2013](lync-server-2013-how-persistent-chat-server-works.md) nella documentazione relativa alla pianificazione, alla distribuzione o alle operazioni e [Hardware supportato per Lync Server 2013](lync-server-2013-supported-hardware.md) nella documentazione relativa alla supportabilità.

Per informazioni dettagliate sull'acquisizione dei certificati, la creazione del database di SQL Server e la creazione di archivi di file, vedere [Distribuzione di Lync Server 2013](lync-server-2013-deploying-lync-server.md) nella documentazione relativa alla distribuzione.

Un singolo server Chat persistenteFront End Server può supportare 20.000 utenti attivi. È possibile configurare un pool di server Chat persistente con fino a 4 Front End Server attivi per supportare un totale di 80.000 utenti contemporanei.

server Chat persistente è inoltre supportato in un server virtuale. Quest'ultimo può supportare fino a 20.000 utenti se ha le stesse specifiche del server fisico.

> [!important]  
> È necessario installare server Chat persistente in un file system NTFS per garantire un livello adeguato di sicurezza del file system. Il file system FAT32 non è supportato per server Chat persistente.

## Contenuto della sezione

  - [Funzionamento del server chat persistente in Lync Server 2013](lync-server-2013-how-persistent-chat-server-works.md)

  - [Elenco di controllo di distribuzione per il server Chat persistente in Lync Server 2013](lync-server-2013-deployment-checklist-for-persistent-chat-server.md)

  - [Requisiti tecnici per il server Chat persistente in Lync Server 2013](lync-server-2013-technical-requirements-for-persistent-chat-server.md)

  - [Configurazione dei sistemi e dell'infrastruttura per il server Chat persistente in Lync Server 2013](lync-server-2013-setting-up-systems-and-infrastructure-for-persistent-chat-server.md)

  - [Aggiunta del server Chat persistente alla distribuzione in Lync Server 2013](lync-server-2013-adding-persistent-chat-server-to-your-deployment.md)

  - [Installazione del server Chat persistente in Lync Server 2013](lync-server-2013-installing-persistent-chat-server.md)

  - [Aggiunta di un amministratore di Chat persistente in Lync Server 2013](lync-server-2013-adding-a-persistent-chat-administrator.md)

  - [Configurazione del server Chat persistente in Lync Server 2013](lync-server-2013-configuring-persistent-chat-server.md)

  - [Configurazione del server Chat persistente tramite i cmdlet di Windows PowerShell](configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md)

  - [Risoluzione dei problemi di configurazione del server Chat persistente tramite i cmdlet di Windows PowerShell in Lync Server 2013](lync-server-2013-troubleshooting-persistent-chat-server-configuration-using-windows-powershell-cmdlets.md)

  - [Configurazione del server Chat persistente per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013](lync-server-2013-configuring-persistent-chat-server-for-high-availability-and-disaster-recovery.md)

  - [Failover e failback del server Chat persistente in Lync Server 2013](lync-server-2013-failing-over-and-failing-back-persistent-chat-server.md)

