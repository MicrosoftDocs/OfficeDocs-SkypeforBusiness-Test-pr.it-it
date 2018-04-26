---
title: 'Lync Server 2013: Failover di un pool'
TOCTitle: Failover di un pool
ms:assetid: 10b13732-bc80-4cb2-a71c-56b1d6cb5bbb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204678(v=OCS.15)
ms:contentKeyID: 49299710
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Failover di un pool in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-10-10_

Se si verifica un errore in un singolo pool Front End ed è necessario eseguirne il failover, utilizzare la procedura indicata di seguito. In questa procedura, Datacenter1 contiene Pool1 e l'errore si è verificato in Pool1. Viene eseguito il failover su Pool2 situato in Datacenter2.

La maggior parte dell'attività di failover del pool implica il failover dell' archivio di gestione centrale, se è necessario. Questo è importante perché l' archivio di gestione centrale deve essere funzionante al momento del failover degli utenti del pool.

Inoltre, se si verifica un errore in un pool Front End ma il pool di server perimetrali presso il sito è ancora in esecuzione, è necessario sapere se quest'ultimo pool utilizza quello in cui si è verificato l'errore come pool hop successivo. In caso affermativo, è necessario impostare il pool di server perimetrali in modo da utilizzare un pool Front End diverso prima del failover del pool Front End in errore. La modifica dell'impostazione relativa all'hop successivo varia a seconda che sia utilizzato un pool che si trova nello stesso sito o in un sito diverso.

**Per impostare un pool di server perimetrali per l'utilizzo di un pool hop successivo nello stesso sito**

1.  Aprire Generatore di topologie, fare clic con il pulsante destro del mouse sul pool di server perimetrali da modificare e scegliere **Modifica proprietà** .

2.  Fare clic su **Hop successivo** . Nell'elenco **Pool hop successivo** selezionare il pool da utilizzare come pool hop successivo.

3.  Fare clic su **OK** , quindi pubblicare le modifiche.

**Per impostare un pool di server perimetrali per l'utilizzo di un pool hop successivo in un sito diverso**

1.  Aprire una finestra di Lync Server Management Shell e digitare il cmdlet seguente:
    
        Set-CsEdgeServer -Identity EdgeServer:<Edge Server pool FQDN> -Registrar Registrar:<NextHopPoolFQDN>

**Per eseguire il failover di un pool in caso di emergenza**

1.  Individuare il pool che ospita il server di gestione centrale digitando il cmdlet seguente su un server Front End in Pool2:
    
        Invoke-CsManagementServerFailover -Whatif
    
    I risultati di questo cmdlet mostrano quale pool ospita attualmente il server di gestione centrale. Nella parte restante di questa procedura, questo pool è denominato CMS\_Pool.

2.  Utilizzare il Generatore di topologie per individuare la versione di Lync Server in esecuzione su CMS\_Pool. Se esegue Lync Server 2013, utilizzare il cmdlet seguente per individuare il pool di backup di Pool 1.
    
        Get-CsPoolBackupRelationship -PoolFQDN <CMS_Pool FQDN>
    
    Backup\_Pool sarà il pool di backup.

3.  Verificare lo stato dell' archivio di gestione centrale con il seguente cmdlet:
    
        Get-CsManagementStoreReplicationStatus -CentralManagementStoreStatus 
    
    Questo cmdlet dovrebbe mostrare che ActiveMasterFQDN e ActiveFileTransferAgents puntano entrambi al nome di dominio completo di CMS\_Pool. Se sono vuoti, il server di gestione centrale non è disponibile ed è necessario eseguirne il failover.

4.  Se l' archivio di gestione centrale non è disponibile o se l' archivio di gestione centrale era in esecuzione su Pool1, ovvero il pool nel quale è si è verificato un errore, è necessario eseguirne il failover sul server di gestione centrale prima del failover del pool. Se è necessario eseguire il failover del server di gestione centrale che era ospitato in un pool che esegue Lync Server 2013, utilizzare il cmdlet indicato al passaggio 5 di questa procedura. Se è necessario eseguire il failover del server di gestione centrale che era ospitato in un pool che esegue Lync Server 2010, utilizzare il cmdlet indicato al passaggio 6 di questa procedura. Se non è necessario eseguire il failover del server di gestione centrale, passare al passaggio 7 di questa procedura.

5.  Per eseguire il failover dell' archivio di gestione centrale in un pool che esegue Lync Server 2013, eseguire le operazioni seguenti:
    
      - Verificare innanzitutto quale server back-end in Backup\_Pool esegue l'istanza principale dell' archivio di gestione centrale digitando quando segue:
        
            Get-CsDatabaseMirrorState -DatabaseType Centralmgmt -PoolFqdn <Backup_Pool Fqdn>
    
      - Se il server back-end principale in Backup\_Pool è il principale, digitare:
        
            Invoke-CSManagementServerFailover -BackupSQLServerFqdn <Backup_Pool Primary BackEnd Server FQDN> -BackupSQLInstanceName <Backup_Pool Primary SQL Instance Name>
        
        Se il server back-end di mirroring in Backup\_Pool è il principale, digitare:
        
            Invoke-CSManagementServerFailover -MirrorSQLServerFqdn <Backup_Pool Mirror BackEnd Server FQDN> -MirrorSQLInstanceName <Backup_Pool Mirror SQL Instance Name>
    
      - Verificare che il failover di server di gestione centrale sia stato completato. Digitare quanto segue:
        
            Get-CsManagementStoreReplicationStatus -CentralManagementStoreStatus 
        
        Verificare che ActiveMasterFQDN e ActiveFileTransferAgents puntino entrambi al nome di dominio completo di Backup\_Pool.
    
      - Infine, verificare lo stato di replica per tutti i Front End Server digitando:
        
            Get-CsManagementStoreReplicationStatus 
        
        Verificare che il valore di tutte le repliche sia True.
        
        Passare al passaggio 7 di questa procedura.

6.  Installare l' archivio di gestione centrale sul server back-end di Backup\_Pool.
    
      - Prima di tutto, eseguire il comando seguente:
        
        ``` 
        Install-CsDatabase -CentralManagementDatabase -Clean -SqlServerFqdn <Backup_Pool Back End Server FQDN> -SqlInstanceName rtc  
        ```
    
      - Eseguire il comando successivo su uno dei server back-end di Backup\_Pool per forzare lo spostamento dell' archivio di gestione centrale:
        
            Move-CsManagementServer -ConfigurationFileName c:\CsConfigurationFile.zip -LisConfigurationFileName c:\CsLisConfigurationFile.zip -Force 
    
      - Verificare che lo spostamento sia stato completato:
        
            Get-CsManagementStoreReplicationStatus -CentralManagementStoreStatus 
        
        Verificare che ActiveMasterFQDN e ActiveFileTransferAgents puntino entrambi al nome di dominio completo di Backup\_Pool.
    
      - Controllare lo stato della replica per tutti i Front End Server digitando quanto segue:
        
            Get-CsManagementStoreReplicationStatus 
        
        Verificare che il valore di tutte le repliche sia True.
    
      - Installare il servizio server di gestione centrale sui restanti Front End Server in Backup\_Pool. A questo scopo, eseguire il comando seguente su tutti i Front End Server, eccetto quello utilizzato quando è stato forzato lo spostamento dell' archivio di gestione centrale in un passaggio precedente di questa procedura:
        
            Bootstrapper /Setup 

7.  Eseguire il failover degli utenti da Pool1 a Pool2 eseguendo il cmdlet seguente in una finestra di Lync Server Management Shell:
    
        Invoke-CsPoolFailover -PoolFQDN <Pool1 FQDN> -DisasterMode -Verbose
    
    Dato che i passaggi eseguiti nelle parti precedenti di questa procedura per verificare lo stato del archivio di gestione centrale non sono universali, è comunque possibile che questo cmdlet abbia esito negativo poiché il failover del archivio di gestione centrale non è ancora stato effettuato completamente. In questo caso, è necessario correggere il archivio di gestione centrale in base ai messaggi di errore visualizzati, quindi ripetere l'esecuzione di questo cmdlet.
    
    Se viene visualizzato il seguente messaggio di errore, è necessario impostare il pool di server perimetrali di questo sito in modo che utilizzi un pool diverso come hop successivo prima di eseguire il failover del pool. Per informazioni dettagliate, vedere la procedura all'inizio di questo argomento.
    
        Invoke-CsPoolFailOver : This Front-end pool "pool1.contoso.com" is specified in
        topology as the next hop for the Edge server. Failing over this pool may cause External
        access/Federation/Split-domain/XMPP features to stop working. Please use Topology Builder to
        change the Edge internal next hop setting to point to a different Front-end pool,  before you
        proceed.

