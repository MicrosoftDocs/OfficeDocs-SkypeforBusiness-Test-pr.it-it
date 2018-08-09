---
title: "Lync Server 2013: Usa Gener. di topol. per config. disp. Elev. e riprist. di emerg."
TOCTitle: Utilizzo di Generatore di topologie per configurare la disponibilità elevata e il ripristino di emergenza
ms:assetid: abc1a25d-1f5e-46ef-91d2-0144fc847206
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205172(v=OCS.15)
ms:contentKeyID: 49301628
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Utilizzo di Generatore di topologie per configurare la disponibilità elevata e il ripristino di emergenza in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-06_

Eseguire i passaggi seguenti in Generatore di topologie per configurare la disponibilità elevata e il ripristino di emergenza per il server Chat persistente.

1.  Aggiungere i database mirror e gli archivi SQL Server del database secondario di log shipping.

2.  Modificare le proprietà del servizio del server Chat persistente come segue:
    
    1.  Abilitare il mirroring per il database primario.
    
    2.  Aggiungere l'archivio SQL Server mirror primario.
    
    3.  Abilitare il database di log shipping SQL Server.
    
    4.  Aggiungere l'archivio SQL Server secondario di log shipping SQL Server.
    
    5.  Aggiungere il mirror dell'archivio SQL Server per il database secondario.
    
    6.  Pubblicare la topologia.

