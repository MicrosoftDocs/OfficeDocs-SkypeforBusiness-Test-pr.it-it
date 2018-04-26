---
title: "Lync Server 2013: Opzioni e procedure consigliate per l'abbinamento dei pool"
TOCTitle: Opzioni e procedure consigliate per l'abbinamento dei pool
ms:assetid: 142caf34-0f20-47f3-9d32-ce25ab622fad
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204697(v=OCS.15)
ms:contentKeyID: 49299766
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Opzioni e procedure consigliate per l'abbinamento dei pool per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-19_

La distanza tra due data center che devono contenere pool Front End abbinati tra loro può essere illimitata. Si consiglia di utilizzare due data center situati nella stessa area internazionale con collegamenti ad alta velocità. La situazione ottimale prevede che i due data center siano sufficientemente distanti per evitare che un'emergenza interessi entrambi contemporaneamente.

L'implementazione di due data center in aree internazionali diverse è possibile, ma può causare una perdita di dati più elevata a causa della latenza nella replica dei dati.

Quando si pianifica l'abbinamento dei pool, è necessario tenere presente che sono supportati solo gli abbinamenti seguenti:

  - I pool Enterprise Edition possono essere abbinati solo ad altri pool Enterprise Edition. Analogamente, i pool Standard Edition sono abbinabili solo ad altri pool Standard Edition.

  - I pool fisici possono essere abbinati solo ad altri pool fisici. Analogamente, i pool virtuali sono abbinabili solo ad altri pool virtuali.

È possibile abbinare due pool in un modo diverso da quanto consigliato nel Generatore di topologie e durante la convalida della topologia. Il Generatore di topologie, ad esempio, consente di abbinare un pool Enterprise Edition a un pool Standard Edition. Questi tipi di abbinamento tuttavia non sono supportati.

Ogni pool di una coppia deve essere in grado di servire tutti gli utenti di entrambi i pool in caso di emergenza.

Se si abbinano pool Enterprise Edition, è anche possibile implementare la disponibilità elevata nei server Back End, ma per coppie di pool Standard Edition sono disponibili solo le misure per il ripristino di emergenza.

