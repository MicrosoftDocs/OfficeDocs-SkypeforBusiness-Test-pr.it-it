---
title: 'Lync Server 2013: Pool di server Director con scalabilità implementata - bilanciamento del carico DNS e bilanciamento del carico hardware'
TOCTitle: Pool di server Director con scalabilità implementata - bilanciamento del carico DNS e bilanciamento del carico hardware
ms:assetid: a1f6ffc0-9e6e-4217-a923-025c9679e154
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205142(v=OCS.15)
ms:contentKeyID: 49301528
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pool di server Director con scalabilità implementata - bilanciamento del carico DNS e bilanciamento del carico hardware in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-22_

Un pool di server Director con scalabilità implementata, in cui è distribuito più di un Server Director per gestire la capacità aggiuntiva e garantire una disponibilità elevata, richiede il bilanciamento del carico per distribuire la comunicazione client e server a tutti i membri del pool. Un Server Director ospita i servizi Web in modo analogo a un pool Front End. Per garantire il bilanciamento del carico, è possibile utilizzare il bilanciamento del carico hardware oppure il bilanciamento del carico DNS (Domain Name System) insieme al bilanciamento del carico hardware. Quest'ultimo è necessario per i servizi Web e il bilanciamento del carico DNS da solo non offre le funzionalità richieste per tali servizi.

Negli argomenti seguenti vengono illustrate le considerazioni di pianificazione per la distribuzione di un pool di server Director con il bilanciamento del carico DNS insieme al bilanciamento del carico hardware. Se si intende utilizzare il bilanciamento del carico hardware ma non il bilanciamento del carico DNS per il pool di server Director, vedere l'argomento [Pool di server Director con scalabilità implementata, servizio di bilanciamento del carico hardware in Lync Server 2013](lync-server-2013-scaled-director-pool-hardware-load-balancer.md), in cui vengono descritti i requisiti di pianificazione per tale topologia.

![Pool di server Director con scalabilità implementata](images/JJ205142.35a78a7a-b781-4c8f-951e-168451ba6a65(OCS.15).jpg "Pool di server Director con scalabilità implementata")

## Argomenti della sezione

  - [Riepilogo dei certificati - bilanciamento del carico DNS e bilanciamento del carico hardware in Lync Server 2013](lync-server-2013-certificate-summary-dns-and-hlb-load-balanced.md)

  - [Riepilogo delle porte - bilanciamento del carico DNS e bilanciamento del carico hardware in Lync Server 2013](lync-server-2013-port-summary-dns-and-hlb-load-balanced.md)

  - [Riepilogo di DNS - bilanciamento del carico DNS e bilanciamento del carico hardware in Lync Server 2013](lync-server-2013-dns-summary-dns-and-hlb-load-balanced.md)

