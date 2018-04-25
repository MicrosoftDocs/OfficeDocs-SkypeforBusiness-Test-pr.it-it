---
title: 'Lync Server 2013: Risorse necessarie per il server Chat persistente'
TOCTitle: Risorse necessarie
ms:assetid: bce50b95-f3c8-407e-963a-d8896ee77fbc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205211(v=OCS.15)
ms:contentKeyID: 49301804
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Risorse necessarie per il server Chat persistente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-01_

La disponibilità elevata e il ripristino di emergenza per il server Chat persistente richiedono ulteriori risorse rispetto a quelle normalmente necessarie per il completo funzionamento. Prima di configurare il server Chat persistente per la disponibilità elevata e il ripristino di emergenza, verificare di disporre delle risorse descritte di seguito, oltre a quelle necessarie per il funzionamento standard del server Chat persistente. Per ulteriori informazioni sulla configurazione, vedere [Configurazione del server Chat persistente in Lync Server 2013](lync-server-2013-configuring-persistent-chat-server.md).

  - Un'istanza di database dedicata nello stesso data center fisico in cui si trova il front-end principale del servizio server Chat persistente. Questo database fungerà da mirror di SQL Server per il database primario di Chat persistente. Facoltativamente, designare un ulteriore SQL Server da utilizzare come server di controllo del mirroring se si desidera un failover automatizzato al database mirror.

  - Un'istanza di database dedicata nell'altro data center fisico. Questo database fungerà da database secondario di log shipping di SQL Server per il database nel data center primario.

  - Un'istanza di database dedicata da utilizzare come mirror di SQL Server per il database secondario. Facoltativamente, designare un ulteriore SQL Server da utilizzare come server di controllo del mirroring. Entrambi devono trovarsi nello stesso data center fisico del database secondario.

  - Se è abilitata la conformità del server Chat persistente, saranno necessarie altre tre istanze di database dedicate. La relativa distribuzione è uguale a quella delle istanze descritte in precedenza per il database di Chat persistente. Benché sia possibile per il database di conformità condividere la stessa istanza di SQL Server utilizzata dal database di Chat persistente, è consigliabile utilizzare istanze autonome per la disponibilità elevata e il ripristino di emergenza.

  - È necessario creare e designare una condivisione file per i log delle transazioni di log shipping di SQL Server. Tutti gli SQL Server di entrambi i centri dati che eseguono i database di Chat persistente devono disporre dell'accesso in lettura/scrittura a questa condivisione file. Tale condivisione non è definita come parte di un ruolo FileStore.

  - Una condivisione file nel server di database secondario da utilizzare come cartella di destinazione per i log delle transazioni di SQL Server che vengono copiati dalla condivisione file del server primario.

Nelle figure riportate di seguito vengono presentati esempi di come può essere configurato l'intero pool di server Chat persistente nelle due diverse topologie di pool estese:

  - Il pool di server Chat persistente quando i data center sono georilevati con un'elevata larghezza di banda e una bassa latenza.

  - Il pool di server Chat persistente quando i data center sono georilevati con una bassa larghezza di banda e un'elevata latenza.

Nella figura seguente viene illustrata una topologia di pool di server Chat persistente estesa in cui i data center sono georilevati con un'elevata larghezza di banda e una bassa latenza.

**Pool di server di Chat persistente esteso quando i data center sono georilevati con un'elevata larghezza di banda e una bassa latenza.**

![Esame della configurazione HBW del pool di server Chat persistente](images/JJ205211.55d10910-c824-41e6-bed2-08d13a2abd65(OCS.15).jpg "Esame della configurazione HBW del pool di server Chat persistente")

Nella figura seguente viene illustrata una topologia di pool di server Chat persistente estesa in cui i data center sono georilevati con una bassa larghezza di banda e un'elevata latenza.

**Pool di server di Chat persistente esteso quando i data center sono georilevati con una bassa larghezza di banda e un'elevata latenza.**

![Esame della configurazione LBW del pool di server Chat persistente](images/JJ205211.586b0a3a-3767-4991-944f-ee54389512aa(OCS.15).jpg "Esame della configurazione LBW del pool di server Chat persistente")

