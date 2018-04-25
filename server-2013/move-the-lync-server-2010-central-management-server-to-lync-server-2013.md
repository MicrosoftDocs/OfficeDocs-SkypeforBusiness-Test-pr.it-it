---
title: Spostare il server di gestione centrale di Lync Server 2010 in Lync Server 2013
TOCTitle: Spostare il server di gestione centrale di Lync Server 2010 in Lync Server 2013
ms:assetid: 30cc98f2-1916-4dbe-99d0-8df5368ed3ec
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688013(v=OCS.15)
ms:contentKeyID: 49887504
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Spostare il server di gestione centrale di Lync Server 2010 in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-25_

Dopo aver eseguito la migrazione da Lync Server 2010 a Lync Server 2013, è prima necessario spostare il server di gestione centrale di Lync Server 2010 nel Front End Server di Lync Server 2013 o nel pool per poter rimuovere il server Lync Server 2010 legacy.

Il server di gestione centrale è un sistema di replica multipla/a master singolo, in cui la copia di lettura/scrittura del database è gestita dal Front End Server che contiene il server di gestione centrale. Ogni computer nella topologia, incluso il Front End Server che contiene il server di gestione centrale, ha una copia di sola lettura dei dati dell' archivio di gestione centrale nel database SQL Server (denominato RTCLOCAL per impostazione predefinita) installato nel computer durante la configurazione e la distribuzione. Il database locale riceve aggiornamenti della replica tramite il servizio Agente di replica per la replica di Lync Server che viene eseguito su tutti i computer. Il nome del database effettivo nel server di gestione centrale e della replica locale è XDS, costituito dai file xds.mdf e xds.ldf. La posizione del database master viene referenziata da un punto di controllo del servizio (SCP) in Servizi di dominio Active Directory. Tutti gli strumenti che usano il server di gestione centrale per gestire e configurare Lync Server usano il punto di controllo del servizio per individuare l' archivio di gestione centrale.

Dopo aver spostato correttamente il server di gestione centrale, rimuovere i database del server di gestione centrale dal Front End Server. Per informazioni sulla rimozione dei database del server di gestione centrale, vedere [Rimuovere il database di SQL Server per un pool Front End](remove-the-sql-server-database-for-a-front-end-pool.md).

Viene usato il cmdlet Windows PowerShell di **Move-CsManagementServer** in Lync Server Management Shell per spostare il database dal database SQL Server di Lync Server 2010 nel database SQL Server di Lync Server 2013 e quindi aggiornare il punto di controllo del servizio in modo che punti alla posizione del server di gestione centrale di Lync Server 2013.

## Preparazione dei Front End Server di Lync Server 2013 prima dello spostamento al server di gestione centrale

Seguire le procedure descritte in questa sezione per preparare i Front End Server di Lync Server 2013 prima di spostare il server di gestione centrale di Lync Server 2010.

## Per preparare un pool Front End Enterprise Edition

1.  Nel pool Front End Enterprise Edition di Lync Server 2013 in cui si desidera riposizionare il server di gestione centrale: accedere al computer in cui è installato Lync Server Management Shell come membro del gruppo **RTCUniversalServerAdmins**. È anche necessario disporre dei diritti e delle autorizzazioni di utente sysadmin del database SQL Server sul database in cui si desidera installare il archivio di gestione centrale.

2.  Aprire Lync Server Management Shell.

3.  Per creare il nuovo archivio di gestione centrale nel database SQL Server di Lync Server 2013, in Lync Server Management Shell digitare:
    
        Install-CsDatabase -CentralManagementDatabase -SQLServerFQDN <FQDN of your SQL Server> -SQLInstanceName <name of instance>

4.  Verificare che lo stato del servizio **Lync Server Front-End** sia **Avviato** .

## Per preparare un Standard Edition Front End Server

1.  Nel Front End Server del Lync Server 2013 Standard Edition in cui si desidera riposizionare il server di gestione centrale: accedere al computer in cui è installato Lync Server Management Shell come membro del gruppo **RTCUniversalServerAdmins**.

2.  Aprire Distribuzione guidata di Lync Server.

3.  Nella Distribuzione guidata di Lync Server fare clic su **Prepara primo server Standard Edition** .

4.  Nella pagina **Esecuzione comandi in corso** SQL Server Express è installato come server di gestione centrale. Vengono create le regole firewall necessarie. Al termine dell'installazione del database e dei prerequisiti software, fare clic su **Fine** .
    

    > [!NOTE]
    > L'installazione iniziale può richiedere tempo senza che vengano visualizzati aggiornamenti visibili nella schermata riepilogativa di output dei comandi. Questo è dovuto all'installazione di SQL Server Express. Se si desidera monitorare l'installazione del database, usare Gestione attività.



5.  Per creare il nuovo archivio di gestione centrale nel Front End Server di Lync Server 2013 Standard Edition, in Lync Server Management Shell digitare:
    
        Install-CsDatabase -CentralManagementDatabase -SQLServerFQDN <FQDN of your Standard Edition Server> -SQLInstanceName <name of instance - RTC by default>

6.  Verificare che lo stato del servizio **Lync Server Front-End** sia **Avviato** .

## Per spostare il server di gestione centrale di Lync Server 2010 in Lync Server 2013

1.  Sul server Lync Server 2013 che rappresenterà il server di gestione centrale: accedere al computer in cui è installato Lync Server Management Shell come membro del gruppo **RTCUniversalServerAdmins**. È anche necessario disporre dei diritti e delle autorizzazioni di amministratore del database SQL Server.

2.  Aprire il Lync Server Management Shell.

3.  In Lync Server Management Shell digitare:
    
        Enable-CsTopology
    

    > [!WARNING]
    > Se <CODE>Enable-CsTopology</CODE> ha esito negativo, risolvere il problema impedendo il completamento del comando prima di continuare. Se <STRONG>Enable-CsTopology</STRONG> ha esito negativo, lo spostamento non riuscirà e potrebbe lasciare la topologia in uno stato senza archivio di gestione centrale.



4.  Sul Front End Server o sul pool Front End di Lync Server 2013 in Lync Server Management Shell digitare:
    
        Move-CsManagementServer

5.  Lync Server Management Shell visualizza i server, gli archivi file, gli archivi di database e i punti di connessione del servizio dello Stato corrente e dello Stato proposto. Leggere attentamente le informazioni e verificare che l'origine e la destinazione siano corrette. Digitare **S** per continuare o **N** per interrompere lo spostamento.

6.  Esaminare eventuali avvisi o errori generati dal comando **Move-CsManagementServer** e risolverli.

7.  Sul server Lync Server 2013 aprire la Distribuzione guidata di Lync Server.

8.  Nella Distribuzione guidata di Lync Server fare clic su **Installa o aggiorna il sistema Lync Server** , su **Passaggio 2: Installazione o rimozione componenti di Lync Server** e quindi su **Avanti** . Esaminare il riepilogo e quindi fare clic su **Fine** .

9.  Sul server Lync Server 2010 aprire la Distribuzione guidata di Lync Server.

10. Nella Distribuzione guidata di Lync Server fare clic su **Installa o aggiorna il sistema Lync Server** , su **Passaggio 2: Installazione o rimozione componenti di Lync Server** e quindi su **Avanti** . Esaminare il riepilogo e quindi fare clic su **Fine** .

11. Riavviare il server Lync Server 2013. Questa operazione è necessaria a causa di una modifica relativa all'appartenenza ai gruppi per l'accesso al database di server di gestione centrale.

12. Per verificare che venga eseguita la replica con il nuovo archivio di gestione centrale, in Lync Server Management Shell digitare:
    
        Get-CsManagementStoreReplicationStatus
    

    > [!NOTE]
    > Il processo di replica può richiedere tempo per aggiornare tutte le repliche correnti.



## Per rimuovere i file dell' archivio di gestione centrale di Lync Server 2010 dopo uno spostamento

1.  Sul server Lync Server 2010: accedere al computer sul quale è installato Lync Server Management Shell come membro del gruppo **RTCUniversalServerAdmins**. È anche necessario disporre dei diritti e delle autorizzazioni di amministratore del database SQL Server.

2.  Aprire Lync Server Management Shell
    

    > [!WARNING]
    > Non procedere con la rimozione dei file di database precedenti prima del completamento e della stabilizzazione della replica. Se si rimuovono i file prima del completamento della replica, verrà danneggiato il processo di replica e il server di gestione centrale appena spostato verrà lasciato in uno stato sconosciuto. Usare il cmdlet <STRONG>Get-CsManagementStoreReplicationStatus</STRONG> per verificare lo stato della replica.



3.  Per rimuovere i file di database dell' archivio di gestione centrale dal server di gestione centrale di Lync Server 2010, digitare:
    
        Uninstall-CsDatabase -CentralManagementDatabase -SqlServerFqdn <FQDN of SQL Server> -SqlInstanceName <Name of source server>
    
    Ad esempio:
    
        Uninstall-CsDatabase -CentralManagementDatabase -SqlServerFqdn sql.contoso.net -SqlInstanceName rtc
    
    Dove *\<FQDN del server SQL\>* è il server back-end di Lync Server 2010 in una distribuzione Enterprise Edition o l'FQDN del server Standard Edition.

