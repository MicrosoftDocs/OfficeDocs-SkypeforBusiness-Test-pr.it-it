---
title: Rimuovere un Front End Server da un pool
TOCTitle: Rimuovere un Front End Server da un pool
ms:assetid: 767225c9-7c0b-4d54-a407-d77134ba2abe
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688095(v=OCS.15)
ms:contentKeyID: 49887610
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rimuovere un Front End Server da un pool

 

_**Ultima modifica dell'argomento:** 2012-10-04_

Il server Front End Server di Microsoft Lync Server 2010 Enterprise Edition non può esistere come computer autonomo, ma deve essere definito come pool Front End, anche se il pool include un solo computer.

In questo argomento vengono fornite informazioni dettagliate sul processo di rimozione di un singolo Front End Server da un pool Front End esistente. Se il server Front End Server è l'ultimo server nel pool o se si intende rimuovere completamente il pool, vedere [Rimuovere pool Front End o server Standard Edition](remove-front-end-pool-or-standard-edition-server.md). Non è necessario rimuovere singoli Front End Server prima di rimuovere il pool Front End. Quando si rimuove il pool, viene rimosso anche ogni Front End Server.

## Per rimuovere un Front End Server da un pool

1.  Aprire Lync Server 2013 Front End Server e quindi Generatore di topologie.

2.  Passare al nodo Lync Server 2010.

3.  Espandere **Pool Enterprise Edition Front End** , espandere il pool Front End che include il server Front End Server che si desidera rimuovere, fare clic con il pulsante destro del mouse sul server Front End Server da rimuovere e quindi scegliere **Elimina** .

