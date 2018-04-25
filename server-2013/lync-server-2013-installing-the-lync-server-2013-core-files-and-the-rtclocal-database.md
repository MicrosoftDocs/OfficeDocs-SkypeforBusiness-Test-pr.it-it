---
title: Installazione dei file principali di Lync Server 2013 e del database RTCLocal
TOCTitle: Installazione dei file principali di Lync Server 2013 e del database RTCLocal
ms:assetid: 206f0c1d-40f7-45b6-aa62-88aaef6cf7f6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204734(v=OCS.15)
ms:contentKeyID: 49299903
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Installazione dei file principali di Lync Server 2013 e del database RTCLocal

 

_**Ultima modifica dell'argomento:** 2012-10-20_

Per installare i file principali di Lync Server 2013 in un computer, completare la procedura seguente. Il database RTCLocal viene installato automaticamente con i file principali. Ricordare che non è necessario installare SQL Server nei nodi Watcher. Verrà invece installato automaticamente SQL Server Express.

Per installare i file principali di Lync Server 2013 e il database RTCLocal:

1.  Nel computer del nodo Watcher fare clic su **Start**, scegliere **Tutti i programmi**, **Accessori**, quindi fare clic con il pulsante destro del mouse su **Prompt dei comandi** e scegliere **Esegui come amministratore**.

2.  Nella finestra della console digitare il comando seguente e premere INVIO, usando il percorso appropriato dei file di installazione di Lync Server:
    
        D:\Setup.exe /BootstrapLocalMgmt

Per verificare che i componenti principali di Lync Server siano stati installati correttamente, fare clic su **Start**, scegliere **Tutti i programmi**, **Lync Server 2013**, e quindi fare clic su **Lync Server Management Shell**. In Lync Server 2013 Management Shell digitare il comando di Windows PowerShell seguente, quindi premere INVIO:

    Get-CsWatcherNodeConfiguration

Quando si esegue questo comando per la prima volta, non viene restituito alcun dato perché non è ancora stato configurato alcun computer del nodo Wwatcher. Se il comando viene eseguito senza errori, si può ritenere che l'installazione di Lync Server sia andata a buon fine.

Se il computer del nodo Watcher si trova all'interno della rete perimetrale, è possibile eseguire il comando seguente per verificare l'installazione di Lync Server 2013:

    Get-CsPinPolicy

Verranno restituite informazioni, a seconda del numero di criteri PIN configurati per l'uso nell'organizzazione:

    Identity             : Global
    Description          :
    MinPasswordLength    : 5
    PINHistoryCount      : 0
    AllowCommonPatterns  : False
    PINLifetime          : 0
    MaximumLogonAttempts :

Se vengono restituite informazioni sui criteri PIN, i componenti principali sono stati correttamente installati.

