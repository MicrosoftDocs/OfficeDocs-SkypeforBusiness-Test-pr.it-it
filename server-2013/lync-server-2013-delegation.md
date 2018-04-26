---
title: 'Lync Server 2013: Delega'
TOCTitle: Delega
ms:assetid: 89e76e5c-3cfb-4504-8d0d-7509c8ba9815
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994045(v=OCS.15)
ms:contentKeyID: 52062209
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Delega in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-03-09_

Il routing in base alla posizione influisce sulle funzionalità di delega in Lync nel modo seguente:

  - Quando un delegato abilitato per il routing in base alla posizione effettua una chiamata per conto di un responsabile, viene utilizzato il criterio vocale del delegato per autorizzare la chiamata e verrà utilizzato il criterio di routing vocale del sito del delegato per instradare la chiamata

  - Per le chiamate PSTN in arrivo a un responsabile verranno applicate le stesse regole valide per l'inoltro delle chiamate o lo squillo simultaneo descritte negli argomenti corrispondenti.

  - Quando un delegato imposta un endpoint PSTN come destinazione dello squillo simultaneo per una chiamata in arrivo al responsabile, verrà utilizzato il criterio di routing vocale del sito associato al trunk in arrivo per instradare la chiamata all'endpoint PSTN del delegato.

  - Per la delega è consigliabile che il responsabile e i delegati associati si trovino in genere nello stesso sito di rete.

## Vedere anche

#### Ulteriori risorse

[Scenari per il routing in base alla posizione in Lync Server 2013](lync-server-2013-scenarios-for-location-based-routing.md)

