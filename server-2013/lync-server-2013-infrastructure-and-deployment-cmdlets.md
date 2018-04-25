---
title: Cmdlet per l'infrastruttura e la distribuzione
TOCTitle: Cmdlet per l'infrastruttura e la distribuzione
ms:assetid: 0a6e872a-9f70-4f23-a4a5-8820dbf55370
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398153(v=OCS.15)
ms:contentKeyID: 49299626
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlet per l'infrastruttura e la distribuzione

 

_**Ultima modifica dell'argomento:** 2012-10-09_

I cmdlet per l'infrastruttura e la distribuzione inclusi in Microsoft Lync Server 2013 possono essere utili nell'installazione iniziale e nella distribuzione del prodotto. Dopo che Lync Server è stato distribuito, questi cmdlet possono essere utilizzati per eseguire operazioni tra cui la verifica del corretto funzionamento dei componenti, la gestione delle impostazioni di replica e il backup e ripristino della topologia, dei criteri e delle impostazioni di configurazione di Lync Server.

## Cmdlet per l'infrastruttura e la distribuzione

Gli amministratori avranno raramente necessità di chiamare direttamente molti dei cmdlet per l'infrastruttura e la distribuzione. Questo è dovuto al fatto che tali cmdlet vengono richiamati automaticamente durante l'esecuzione del programma di installazione o di Generatore di topologie. Un'eccezione importante è rappresentata dal cmdlet **Export-CsConfiguration**, che consente di effettuare una copia di backup della topologia, dei criteri e delle impostazioni di configurazione di Lync Server. Quando necessario, i cmdlet per l'infrastruttura e la distribuzione possono tuttavia essere eseguiti anche da Lync Server Management Shell o mediante uno script. L'utilizzo di uno script consente di automatizzare alcune attività. Di seguito è riportato un elenco dei cmdlet correlati direttamente all'infrastruttura e alla distribuzione:

**[Cmdlet per Active Directory](lync-server-2013-active-directory-cmdlets.md)**

  -   
    [Disable-CsAdDomain](disable-csaddomain.md)

  -   
    [Enable-CsAdDomain](enable-csaddomain.md)

  -   
    [Get-CsAdDomain](get-csaddomain.md)

  -   
    [Disable-CsAdForest](disable-csadforest.md)

  -   
    [Enable-CsAdForest](enable-csadforest.md)

  -   
    [Get-CsAdForest](get-csadforest.md)

  -   
    [Get-CsAdServerSchema](get-csadserverschema.md)

  -   
    [Install-CsAdServerSchema](install-csadserverschema.md)

**[Cmdlet per la replica](lync-server-2013-replication-cmdlets.md)**

  -   
    [Debug-CsInterPoolReplication](debug-csinterpoolreplication.md)

  -   
    [Invoke-CsManagementStoreReplication](invoke-csmanagementstorereplication.md)

  -   
    [Get-CsManagementStoreReplicationStatus](get-csmanagementstorereplicationstatus.md)

  -   
    [Enable-CsReplica](enable-csreplica.md)

  -   
    [Test-CsReplica](test-csreplica.md)

  -   
    [Get-CsUserReplicatorConfiguration](get-csuserreplicatorconfiguration.md)

  -   
    [New-CsUserReplicatorConfiguration](new-csuserreplicatorconfiguration.md)

  -   
    [Remove-CsUserReplicatorConfiguration](remove-csuserreplicatorconfiguration.md)

  -   
    [Set-CsUserReplicatorConfiguration](set-csuserreplicatorconfiguration.md)

**[Cmdlet per la topologia](lync-server-2013-topology-cmdlets.md)**

  -   
    [Get-CsPool](get-cspool.md)

  -   
    [Get-CsSite](get-cssite.md)

  -   
    [Set-CsSite](set-cssite.md)

  -   
    [Enable-CsTopology](enable-cstopology.md)

  -   
    [Get-CsTopology](get-cstopology.md)

  -   
    [Publish-CsTopology](publish-cstopology.md)

  -   
    [Test-CsTopology](test-cstopology.md)

  -   
    [Export-CsConfiguration](export-csconfiguration.md)

  -   
    [Import-CsConfiguration](import-csconfiguration.md)

  -   
    [Get-CsServerVersion](get-csserverversion.md)

  -   
    [Disable-CsComputer](disable-cscomputer.md)

  -   
    [Enable-CsComputer](enable-cscomputer.md)

  -   
    [Get-CsComputer](get-cscomputer.md)

  -   
    [Test-CsComputer](test-cscomputer.md)

  -   
    [Get-CsNetworkInterface](get-csnetworkinterface.md)

**[Cmdlet di backup e disponibilità elevata](lync-server-2013-backup-and-high-availability-cmdlets.md)**

  - [Get-CsBackupServiceConfiguration](get-csbackupserviceconfiguration.md)

  - [Remove-CsBackupServiceConfiguration](remove-csbackupserviceconfiguration.md)

  - [Set-CsBackupServiceConfiguration](set-csbackupserviceconfiguration.md)

  - [Get-CsBackupServiceStatus](get-csbackupservicestatus.md)

  - [Invoke-CsBackupServiceSync](invoke-csbackupservicesync.md)

  - [Debug-CsIntraPoolReplication](debug-csintrapoolreplication.md)

  - [Backup-CsPool](backup-cspool.md)

  - [Get-CsPoolBackupRelationship](get-cspoolbackuprelationship.md)

  - [Get-CsPoolFabricState](get-cspoolfabricstate.md)

  - [Invoke-CsPoolFailBack](invoke-cspoolfailback.md)

  - [Invoke-CsPoolFailOver](invoke-cspoolfailover.md)

  - [Get-CsPoolUpgradeReadinessState](get-cspoolupgradereadinessstate.md)

  - [Invoke-CsStorageServiceFlush](invoke-csstorageserviceflush.md)

  - [Sync-CsUserData](sync-csuserdata.md)

  - [Remove-CsUserStoreBackupData](remove-csuserstorebackupdata.md)

## Vedere anche

#### Ulteriori risorse

[Blog di Lync Server PowerShell](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x410)

