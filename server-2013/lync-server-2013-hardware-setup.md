---
title: 'Lync Server 2013: Configurazione hardware'
TOCTitle: Configurazione hardware
ms:assetid: 37a9f295-cde3-4beb-9a6a-2580082798ab
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425852(v=OCS.15)
ms:contentKeyID: 49300215
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione hardware per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

Per impostare l'hardware e altri componenti richiesti nell'infrastruttura necessaria per implementare la topologia, prima di pubblicare quest'ultima in Generatore di topologie, eseguire le operazioni seguenti:

  - Installare l'hardware per ogni componente della struttura di topologia creata e salvata tramite Generatore di topologie, inclusi tutti i computer necessari (a seconda delle esigenze, server che eseguono Lync Server 2013, server di database, server che eseguono Internet Information Services (IIS) e server proxy inversi), le schede di rete, i dispositivi di bilanciamento del carico hardware e i dispositivi di archiviazione (ad esempio file server). Assicurarsi di aver rispettato i consigli relativi al numero e alla velocità delle schede di rete. Se si utilizzeranno servizi di bilanciamento del carico hardware, assicurarsi di aver ricevuto le informazioni appropriate dal fornitore per configurarli per l'uso con Lync Server 2013. Se si utilizzerà un file server o un altro tipo di server per ospitare la condivisione file richiesta da Lync Server, assicurarsi che il server sia disponibile e pronto per la configurazione della condivisione file. Per informazioni dettagliate sulla definizione di una topologia che specifichi i componenti necessari per la distribuzione, vedere [Definizione e configurazione della topologia in Lync Server 2013](lync-server-2013-defining-and-configuring-the-topology.md). Per informazioni dettagliate sui requisiti hardware per i server, vedere [Hardware supportato per Lync Server 2013](lync-server-2013-supported-hardware.md) nella documentazione relativa alla supportabilità.

  - Assicurarsi che l'infrastruttura di rete soddisfi i requisiti. Per informazioni dettagliate, vedere [Requisiti dell'infrastruttura di rete per Lync Server 2013](lync-server-2013-network-infrastructure-requirements.md) nella documentazione relativa alla pianificazione.

  - Configurare Servizi di dominio Active Directory. Tra le attività di configurazione sono incluse la preparazione di Servizi di dominio Active Directory e la definizione di tutti i componenti che si desidera distribuire in questo servizio. Per informazioni dettagliate sulla preparazione di Servizi di dominio Active Directory, vedere [Preparazione di Servizi di dominio Active Directory per Lync Server 2013](lync-server-2013-preparing-active-directory-domain-services.md) nella documentazione relativa alla distribuzione.

  - Configurare le autorizzazioni necessarie per creare la condivisione file. Le autorizzazioni per l'utilizzo di condivisioni file da parte di Lync Server 2013 vengono configurate automaticamente da Generatore di topologie quando si pubblica la topologia. L'account utente utilizzato per pubblicare la topologia, tuttavia, deve disporre del controllo completo (lettura/scrittura/modifica) per la condivisione file in modo che Generatore di topologie possa configurare le autorizzazioni necessarie. Per una gestione corretta della condivisione file durante il processo di pubblicazione da parte del Generatore di topologie, è necessario che l'utente o il gruppo di dominio di cui è membro l'utente sia membro del gruppo Administrators locale nel computer in cui si trova la condivisione file. In uno scenario multidominio l'utente o il gruppo del Dominio A deve essere membro del gruppo Administrators locale nel computer nel Dominio B in cui verrà posizionata la condivisione file.
    
    Per informazioni dettagliate sull'aggiornamento mediante le condivisioni file in un sistema DFS (Distributed File System), vedere [Configurare l'archiviazione dei file per Lync Server 2013](lync-server-2013-configure-dfs-file-storage.md).
    

    > [!WARNING]
    > La condivisione file per Lync Server 2013 Enterprise Edition non può essere posizionata nel Front End Server.



  - Installare e configurare il dispositivo di bilanciamento del carico hardware per i servizi Web. Con il bilanciamento del carico DNS (Domain Name System) distribuito, è comunque necessario utilizzare dispositivi di bilanciamento del carico hardware per questi pool, ma solo per il traffico HTTP/HTTPS. Il dispositivo di bilanciamento del carico hardware viene utilizzato per il traffico HTTPS proveniente da client sulle porte 443 e 80. Sebbene sia comunque necessario disporre di dispositivi di bilanciamento del carico hardware per questi pool, le impostazioni e l'amministrazione di tale bilanciamento saranno destinate principalmente al traffico HTTP/HTTPS, a cui gli amministratori del bilanciamento del carico hardware sono abituati.

Dopo aver eseguito tutte le attività di preparazione descritte in questo argomento, ma prima di pubblicare la topologia, è inoltre necessario eseguire le operazioni seguenti:

  - [Installare i sistemi operativi e il software prerequisito nei server per Lync Server 2013](lync-server-2013-install-operating-systems-and-prerequisite-software-on-servers.md)

  - [Configurare IIS per Lync Server 2013](lync-server-2013-configure-iis.md)

  - [Configurare SQL Server per Lync Server 2013](lync-server-2013-configure-sql-server-for-lync-server.md)

  - [Configurare record DNS in Lync Server 2013 per un pool Front End o un server Standard Edition](lync-server-2013-configure-dns-records-for-a-front-end-pool-or-standard-edition-server.md)

