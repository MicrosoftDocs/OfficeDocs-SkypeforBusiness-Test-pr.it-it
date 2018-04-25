---
title: "Lync Server 2013: Preparazione dell'infrastruttura e dei sistemi"
TOCTitle: Preparazione dell'infrastruttura e dei sistemi
ms:assetid: 1254ee38-0679-4714-b293-1050f107c158
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398205(v=OCS.15)
ms:contentKeyID: 49299744
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Preparazione dell'infrastruttura e dei sistemi per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

La distribuzione di Lync Server 2013 richiede l'uso di Generatore di topologie per definire e pubblicare la struttura della topologia. Per identificare i componenti necessari per la topologia, è possibile utilizzare Generatore di topologie per creare e salvare una struttura. Prima di pubblicare la topologia nel Generatore di topologie, eseguire le operazioni seguenti:

  - Acquisire e installare l'hardware per ogni componente della struttura di topologia creata e salvata utilizzando il Generatore di topologie, compresi tutti i computer necessari (server che eseguono Lync Server 2013, server di database, server che eseguono Internet Information Services (IIS) e server proxy inversi), le schede di rete, i dispositivi di bilanciamento del carico hardware e i dispositivi di archiviazione (ad esempio file server). Per informazioni dettagliate su come definire una topologia che specifichi i componenti necessari per la distribuzione, vedere [Definizione e configurazione della topologia in Lync Server 2013](lync-server-2013-defining-and-configuring-the-topology.md). Per informazioni dettagliate sui requisiti hardware per i server, vedere [Hardware supportato per Lync Server 2013](lync-server-2013-supported-hardware.md) nella documentazione relativa alla supportabilità.

  - Assicurarsi che l'infrastruttura di rete soddisfi i requisiti. Per informazioni dettagliate, vedere [Requisiti dell'infrastruttura di rete per Lync Server 2013](lync-server-2013-network-infrastructure-requirements.md) nella documentazione relativa alla pianificazione.

  - Installare Servizi di dominio Active Directory. Per pubblicare e abilitare la topologia, è necessario che i server interni siano rappresentati da account computer in Servizi di dominio Active Directory. A tale scopo, i computer vengono aggiunti a Servizi di dominio Active Directory. Per informazioni dettagliate sulla preparazione di Servizi di dominio Active Directory, vedere [Preparazione di Servizi di dominio Active Directory per Lync Server 2013](lync-server-2013-preparing-active-directory-domain-services.md).

  - Creare una condivisione file. I server Standard Edition possono ospitare la condivisione file per il file richiesto, mentre in una distribuzione Enterprise la condivisione file non può essere ospitata sul server Front End. Le autorizzazioni e le appartenenze ai gruppi necessarie per la distribuzione e l'impostazione dell'elenco di controllo di accesso nella cartella e nella condivisione devono essere impostate in modo adeguato per l'esecuzione corretta del Generatore di topologie. È necessario assicurarsi che la persona che esegue il Generatore di topologie disponga delle autorizzazioni e delle appartenenze ai gruppi seguenti:
    
      - Membro del gruppo Administrators locale
    
      - Membro del gruppo Domain Users
    
      - Controllo completo sulla condivisione e sulla cartella dell'archivio file

  - Per Enterprise Edition, installare e configurare SQL Server. Per la corretta installazione di SQL Server è necessario che il server basato su SQL Server sia online e che la persona che pubblica la topologia sia un amministratore locale sul server SQL e membro del gruppo sysadmin di SQL Server sull'istanza di SQL Server.

Dopo aver completato tutte le attività di preparazione descritte in questo argomento, ma prima di pubblicare la topologia, è necessario eseguire anche le altre attività di preparazione, tra cui l'installazione dei sistemi operativi Windows e degli altri prerequisiti software, l'installazione di IIS e la configurazione di DNS. Per informazioni dettagliate su queste attività, vedere [Requisiti di sistema per i server Lync Server 2013](lync-server-2013-system-requirements-for-servers-running-lync-server-2013.md), [Configurare IIS per Lync Server 2013](lync-server-2013-configure-iis.md) e [Preparazione dell'infrastruttura e dei sistemi per Lync Server 2013](lync-server-2013-preparing-the-infrastructure-and-systems.md). È inoltre opportuno acquisire familiarità con i client e i relativi requisiti. Per informazioni dettagliate, vedere [Distribuzione di client e dispositivi in Lync Server 2013](lync-server-2013-deploying-clients-and-devices.md).

## Argomenti della sezione

  - [Configurazione hardware per Lync Server 2013](lync-server-2013-hardware-setup.md)

  - [Installazione del software per Lync Server 2013](lync-server-2013-software-setup.md)

  - [Preparazione di Servizi di dominio Active Directory per Lync Server 2013](lync-server-2013-preparing-active-directory-domain-services.md)

  - [Configurare SQL Server per Lync Server 2013](lync-server-2013-configure-sql-server-for-lync-server.md)

  - [Configurare record DNS in Lync Server 2013 per un pool Front End o un server Standard Edition](lync-server-2013-configure-dns-records-for-a-front-end-pool-or-standard-edition-server.md)

  - [Installare gli strumenti di amministrazione di Lync Server 2013](lync-server-2013-install-lync-server-administrative-tools.md)

