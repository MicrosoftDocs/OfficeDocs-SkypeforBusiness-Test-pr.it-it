---
title: 'Lync Server 2013: Componenti richiesti per il server Director'
TOCTitle: Componenti richiesti per il server Director
ms:assetid: 15c7c8d4-b93f-4386-b2d1-d76dab8f801e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398228(v=OCS.15)
ms:contentKeyID: 49299788
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Componenti richiesti per il server Director in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-08_

Per poter creare e configurare un Server Director è necessario distribuire solo il ruolo del server Server Director. A tal fine, utilizzare Generatore di topologie e definire un pool computer singolo o un pool di più computer nel nodo pool di server Director. Dopo aver definito il Server Director o il pool di server Director, eseguire la Distribuzione guidata di Lync Server nel computer Server Director. Nel caso venga definito un pool di server Director, eseguire la Distribuzione guidata di Lync Server in ogni server membro del pool.

## Topologie

È possibile implementare un solo server Server Director oppure un pool di server Director. Il Server Director è sempre un server o un pool separato, non collocato con alcun altro ruolo del server in Lync Server 2013.


> [!NOTE]
> Se non vengono distribuiti Director, il Front End Server o il pool Front End assumerà il ruolo Server Director.



Un pool di Director deve avere il carico bilanciato. È possibile effettuare una delle operazioni seguenti:

  - Creare una topologia che usa un servizio di bilanciamento del carico hardware per i servizi Web e un bilanciamento del carico DNS (Domain Name System) per le altre tipologie di traffico.
    
    [Pool di server Director con scalabilità implementata - bilanciamento del carico DNS e bilanciamento del carico hardware in Lync Server 2013](lync-server-2013-scaled-director-pool-dns-load-balancing-and-hardware-load-balancer.md)

  - Creare una topologia che usa un bilanciamento del carico hardware per gestire il bilanciamento del carico necessario per il pool di server Director.
    
    [Pool di server Director con scalabilità implementata, servizio di bilanciamento del carico hardware in Lync Server 2013](lync-server-2013-scaled-director-pool-hardware-load-balancer.md)

