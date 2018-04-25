---
title: 'Lync Server 2013: Eseguire il backup delle relazioni di registrazione'
TOCTitle: Eseguire il backup delle relazioni di registrazione
ms:assetid: 7e078271-84b9-4666-989c-c4507a0cdf4a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205033(v=OCS.15)
ms:contentKeyID: 49301104
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eseguire il backup delle relazioni di registrazione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-06-28_

Oltre ad offrire funzioni di ripristino di emergenza, due pool accoppiati funzionano come registrar di backup l'uno per l'altro. In Lync Server 2013, le relazioni di registrar di backup tra pool Front End sono sempre di tipo 1:1 e reciproche. Pertanto, se il P1 è il backup del P2, il P2 sarà il backup del P1, e nessuno dei due potrà essere il backup di un altro pool Front End. Ciò rappresenta una modifica rispetto a Lync Server 2010, in cui le relazioni di backup del pool Front End potevano essere di tipo many-to-one.

Anche se le relazioni di backup tra due pool Front End devono essere di tipo 1:1 e simmetriche, ciascun pool Front End può rappresentare il registrar di backup di un numero qualunque di Survivable Branch Appliance, analogamente a quanto accade in Lync Server 2010.

Lync Server 2013 non estende il supporto al ripristino di emergenza agli utenti ospitati su un Survivable Branch Appliance. Se un pool Front End che funziona da backup per Survivable Branch Appliance diviene inattivo, gli utenti che hanno effettuato l'accesso a Survivable Branch Appliance passano alla modalità resilienza anche dopo che per gli utenti ospitati sul pool Front End viene eseguito il failover al pool Front End di backup.

