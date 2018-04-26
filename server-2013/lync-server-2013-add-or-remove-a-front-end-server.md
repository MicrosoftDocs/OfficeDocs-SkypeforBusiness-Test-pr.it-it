---
title: Aggiungere o rimuovere un Front End Server in Lync Server 2013
TOCTitle: Aggiungere o rimuovere un Front End Server in Lync Server 2013
ms:assetid: ab748733-6bad-4c93-8dda-db8d5271653d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205153(v=OCS.15)
ms:contentKeyID: 49301626
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aggiungere o rimuovere un Front End Server in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-19_

Quando si aggiunge un Front End Server a un pool oppure si rimuove un Front End Server da un pool, è quindi necessario riavviare il pool. Per evitare un'interruzione del servizio per gli utenti, eseguire la procedura seguente quando si aggiunge o si rimuove un Front End Server.

## Per aggiungere o rimuovere i server front-end

1.  Se si desidera rimuovere uno o più Front End Server, innanzitutto interrompere le nuove connessioni a questi server. A tale scopo, è possibile utilizzare il cmdlet seguente:
    
        Stop -CsWindowsServices -Graceful

2.  Quando nei server da rimuovere non vi sono sessioni correnti, arrestare i servizi di Lync Server in esecuzione su di essi.

3.  Aprire Generatore di topologie e aggiungere o rimuovere i server necessari.

4.  Pubblicare la topologia.

5.  Se il pool è passato da due a più di due Front End Server oppure è passato da più di due server a esattamente due server, è necessario digitare il cmdlet seguente:
    
        Reset-CsPoolRegistrarState-ResetType FullReset -PoolFqdn <PoolFqdn>
    
    Se il pool dispone di tre o più server, almeno tre di questi server devono essere in esecuzione quando si digita questo cmdlet.

6.  Riavviare tutti i Front End Server del pool, uno alla volta.

