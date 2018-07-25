---
title: Configurare il clustering di SQL Server per Lync Server 2013
TOCTitle: Configurare il clustering di SQL Server per Lync Server 2013
ms:assetid: d7b52ef1-573c-48ed-bb94-34e37b49645c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn383982(v=OCS.15)
ms:contentKeyID: 56558964
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare il clustering di SQL Server per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-01-10_

Microsoft Lync Server 2013 supporta il clustering per SQL Server 2012 e SQL Server 2008 R2. Per informazioni dettagliate sugli elementi supportati, vedere [Supporto per il software di database in Lync Server 2013](lync-server-2013-database-software-support.md).

Prima di installare e distribuire Enterprise Edition Front End Server e il database back-end, è necessario installare e configurare il cluster di SQL Server. Per le procedure consigliate e le istruzioni di configurazione del clustering di failover in SQL Server 2012, vedere <http://technet.microsoft.com/it-it/library/hh231721.aspx>. Per informazioni sul clustering di failover in SQL Server 2008, vedere <http://technet.microsoft.com/it-it/library/ms189134(v=sql.105).aspx>.

Insieme a SQL Server è necessario installare SQL Server Management Studio per gestire le posizioni del database e dei file di log. SQL Server Management Studio viene installato come componente facoltativo quando si installa SQL Server.

> [!important]  
> Per installare e distribuire i database nel server basato su SQL Server, è necessario essere membri del gruppo sysadmin di SQL Server per il server basato su SQL Server in cui verranno installati i file di database. Se non si è membri di questo gruppo, è necessario richiedere di essere aggiunti al gruppo finché i file di database non saranno stati distribuiti. Se non è possibile diventare membri del gruppo sysadmin, è necessario fornire all'amministratore di database di SQL Server lo script per configurare e distribuire i database. Per informazioni dettagliate sulle autorizzazioni e sui diritti utente necessari per eseguire le procedure, vedere <a href="lync-server-2013-deployment-permissions-for-sql-server.md">Autorizzazioni di distribuzione per SQL Server in Lync Server 2013</a>.

## Per configurare il clustering di SQL Server

1.  Dopo aver completato l'installazione e la configurazione del clustering di SQL Server, occorre definire l'archivio SQL Server in Generatore di topologie usando il nome del cluster virtuale dell'istanza di SQL Server (configurato nell'installazione del clustering di SQL Server) e il nome dell'istanza del database SQL Server. A differenza di un singolo server basato su SQL Server, per un server basato su SQL Server in cluster è necessario usare il nome di dominio completo (FQDN) del nodo virtuale.
    

    > [!NOTE]
    > Non è necessario configurare i singoli nodi di cluster di Windows Server per Generatore di topologie, poiché si userà solo il nome del cluster di SQL Server virtuale.



2.  Se si usa Generatore di topologie per distribuire i database, è necessario essere membri del gruppo sysadmin di SQL Server. Se si è membri di questo gruppo ma non si dispone di privilegi nel dominio (ad esempio un ruolo di amministratore di database di SQL Server), si è autorizzati a creare i database ma non a leggere le informazioni necessarie in Lync Server. Per informazioni dettagliate sulle autorizzazioni e sui diritti utente necessari per distribuire Lync Server, vedere [Autorizzazioni di distribuzione per SQL Server in Lync Server 2013](lync-server-2013-deployment-permissions-for-sql-server.md).

3.  Verificare che la cartella dei database e la cartella dei file di log predefinite siano mappate correttamente ai dischi condivisi del cluster di SQL Server mediante SQL Server Management Studio. Questa procedura è obbligatoria se si creano database con Generatore di topologie.
    

    > [!NOTE]
    > Se SQL Server Management Studio non è stato installato, è possibile farlo eseguendo di nuovo l'installazione di SQL Server e selezionando lo strumento di gestione come funzionalità aggiunta per la configurazione di SQL Server esistente.



4.  Installare i database per il server basato su SQL Server mediante Generatore di topologie o i cmdlet di Windows PowerShell. Se si usa Generatore di topologie, eseguire la procedura seguente. Se si usano i cmdlet di Windows PowerShell, vedere [Installazione di database mediante Lync Server Management Shell in Lync Server 2013](lync-server-2013-database-installation-using-lync-server-management-shell.md).

## Per creare database mediante Generatore di topologie

1.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.
    

    > [!WARNING]
    > La procedura seguente si basa sul presupposto che sia stata definita e configurata una topologia in Generatore di topologie. Per informazioni dettagliate sulla definizione della topologia, vedere<A href="lync-server-2013-defining-and-configuring-the-topology.md">Definizione e configurazione della topologia in Lync Server 2013</A>. Per usare Generatore di topologie per pubblicare la topologia e configurare il database, è necessario effettuare l'accesso con i diritti utente e le appartenenze ai gruppi corretti. Per informazioni dettagliate sui diritti utente e le appartenenze ai gruppi necessari, vedere <A href="lync-server-2013-deployment-permissions-for-sql-server.md">Autorizzazioni di distribuzione per SQL Server in Lync Server 2013</A>.



2.  Per pubblicare la topologia, nella pagina **Crea database** di Generatore di topologie fare clic su **Avanzate**.

3.  La pagina **Seleziona percorso file di database** contiene due opzioni che determinano la modalità di distribuzione dei file di database nel cluster di SQL Server. Selezionare una delle opzioni seguenti:
    
      - **Determina automaticamente il percorso dei file di database**. Questa opzione usa un algoritmo per determinare i percorsi dei file di dati e di log dei database in base alla configurazione dell'unità nel server basato su SQL Server. I file verranno distribuiti in modo tale da ottenere prestazioni ottimali.
    
      - **Utilizza i valori predefiniti dell'istanza di SQL Server**. Questa opzione installa i file di log e di dati in base alle impostazioni dell'istanza di SQL Server. Dopo la distribuzione dei file di database in SQL Server, l'amministratore di database di SQL Server può decidere di riposizionare i file per ottimizzare le prestazioni in base a determinati requisiti di configurazione di SQL Server.

4.  Completare la pubblicazione della topologia e verificare che non siano stati generati errori durante l'operazione.

