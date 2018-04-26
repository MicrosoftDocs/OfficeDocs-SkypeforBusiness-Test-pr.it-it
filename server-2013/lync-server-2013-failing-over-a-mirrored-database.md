---
title: 'Lync Server 2013: Failover di un database con mirroring'
TOCTitle: Failover di un database con mirroring
ms:assetid: 70185476-e3d4-440a-9316-fa24b226343e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204991(v=OCS.15)
ms:contentKeyID: 49300935
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Failover di un database con mirroring in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-03-14_

Se è stato configurato il database back-end per l'utilizzo del mirroring sincronizzato con un'istanza di controllo, il failover è automatico. Se il mirroring sincronizzato è stato configurato senza istanza di controllo, è possibile utilizzare le procedure seguenti per il failover e failback del database. Queste procedure sono valide inoltre per eseguire il failover e failback manuale dei database anche quando è stata configurata un'istanza di controllo.

## Per eseguire il failover del database back-end

1.  Prima di eseguire il failover, determinare quale database back-end è quello principale, e quale è il mirror, utilizzando il seguente cmdlet:
    
        Get-CsDatabaseMirrorState -PoolFqdn <poolFQDN> -DatabaseType User

2.  Se archivio di gestione centrale è ospitato in questo pool, digitare il cmdlet seguente per determinare il principale e il mirror per archivio di gestione centrale:
    
        Get-CsDatabaseMirrorState -PoolFqdn <poolFQDN> -DatabaseType CentralMgmt

3.  Eseguire il failover del database utente:
    
      - Se il database primario non ha avuto esito positivo e si esegue il failover del mirror, digitare:
        
            Invoke-CsDatabaseFailover -PoolFqdn <poolFQDN> -DatabaseType User -NewPrincipal mirror -Verbose
    
      - Se il mirror non ha avuto esito positivo e si esegue il failover del database primario, digitare:
        
            Invoke-CsDatabaseFailover -PoolFqdn <poolFQDN> -DatabaseType User -NewPrincipal primary -Verbose

4.  Se server di gestione centrale è ospitato nel pool, eseguire il failover di archivio di gestione centrale.
    
      - Se il database primario non ha avuto esito positivo e si esegue il failover del mirror, digitare:
        
            Invoke-CsDatabaseFailover -PoolFqdn <poolFQDN> -DatabaseType CentralMgmt -NewPrincipal mirror -Verbose
    
      - Se il mirror non ha avuto esito positivo e si esegue il failover del database primario, digitare:
        
            Invoke-CsDatabaseFailover -PoolFqdn <poolFQDN> -DatabaseType CentralMgmt -NewPrincipal primary -Verbose

