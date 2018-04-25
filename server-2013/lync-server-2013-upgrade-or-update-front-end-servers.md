---
title: Eseguire l'aggiornamento dei Front End Server in Lync Server 2013
TOCTitle: Eseguire l'aggiornamento dei Front End Server in Lync Server 2013
ms:assetid: 20fa39ae-ecfb-4c72-9cc4-8e183d3c752f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204736(v=OCS.15)
ms:contentKeyID: 49299909
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eseguire l'aggiornamento dei Front End Server in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-06-28_

I Front End Server di un pool Enterprise Edition sono organizzati in *domini di aggiornamento*. Si tratta di subset di Front End Server nel pool. I domini di aggiornamento vengono creati automaticamente da Generatore di topologie.

L'aggiornamento dei server deve essere eseguito per un dominio di aggiornamento alla volta. Arrestare ogni server in un dominio di aggiornamento, aggiornarlo e quindi riavviarlo prima di passare a un altro dominio di aggiornamento.

![Diagramma di flusso per l'aggiornamento del server](images/JJ204736.42ed59a4-1c26-49f7-ade4-a5a788457ab9(OCS.15).jpg "Diagramma di flusso per l'aggiornamento del server")

## Per applicare un aggiornamento ai Front End Server in un pool

1.  In un Front End Server del pool eseguire il cmdlet seguente:
    
    **Get-CsPoolUpgradeReadinessState**
    
    Se il valore di *PoolUpgradeState* è **Occupato**, attendere 10 minuti, quindi riprovare **Get-CsPoolUpgradeReadiness**. Se il valore **Occupato** compare almeno tre volte consecutive, dopo avere atteso 10 minuti tra ogni tentativo o se viene visualizzato qualsiasi risultato di **InsufficientActiveFrontEnds** per **PoolUpgradeState,** si è verificato un problema con il pool. Se questo pool è associato a un altro pool Front End in una topologia per il ripristino di emergenza, eseguire il failover del pool nel pool di backup e aggiornare i server di questo pool. Per informazioni dettagliate, vedere [Failover di un pool in Lync Server 2013](lync-server-2013-failing-over-a-pool.md).
    
    Se il valore di *PoolUpgradeState* è **Pronto**, andare al passaggio 2.

2.  Il cmdlet **Get-CsPoolUpgradeReadiness** restituisce informazioni su ogni dominio di aggiornamento nel pool e sui Front End Server appartenenti a ciascun dominio. Se il valore **ReadyforUpgrade** è **True** per il dominio di aggiornamento che contiene il server o i server che si desidera aggiornare, è possibile procedere ora all'aggiornamento di tali server. A tale scopo, effettuare quando segue:
    
    1.  Arrestare le nuove connessioni al Front End Server che si sta per aggiornare utilizzando il cmdlet `Stop-CsWindowsService -Graceful -Verbose`.
        

        > [!NOTE]
        > Se questi aggiornamenti del server vengono eseguiti durante un tempo di inattività del server pianificato, è possibile eseguire questo cmdlet senza il parametro '-<STRONG>Graceful</STRONG>', come illustrato di seguito: <STRONG>Stop-CsWindowsService</STRONG>. I servizi verranno immediatamente arrestati, senza attendere che tutte le richieste esistenti dei servizi siano completate.

    
    2.  Aggiornare i server associati a questo dominio di aggiornamento
    
    3.  Riavviare i server e assicurarsi che accettino nuove connessioni.

3.  Ripetere i passaggi 1 e 2 per tutti gli altri domini di aggiornamento nel pool, fino a quando tutti i Front End Server non saranno stati aggiornati.

