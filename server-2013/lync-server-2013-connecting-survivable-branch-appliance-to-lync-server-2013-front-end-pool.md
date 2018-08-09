---
title: "Lync Server 2013: Collega Survivable Branch Appl. a pool Front End LS 2013"
TOCTitle: Connessione di Survivable Branch Appliance al pool Front End di Lync Server 2013
ms:assetid: 3c7ca33f-5295-4d82-9152-41d8bc6f35cf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688026(v=OCS.15)
ms:contentKeyID: 49887526
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Connessione di Survivable Branch Appliance al pool Front End di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-05_

Ogni Survivable Branch Appliance (SBA) è associato a un pool Front End, che funge da funzione di registrazione di backup per l'SBA. Quando il pool Front End viene aggiornato a Lync Server 2013, l'SBA deve essere dissociato dal pool Front End durante l'aggiornamento del pool Front End. Successivamente all'aggiornamento del pool Front End, l'SBA può essere riassociato al pool Front End. Ciò implica l'eliminazione e la successiva nuova aggiunta dell'SBA alla topologia nel Generatore di topologie. Prima di rimuovere l'SBA dalla topologia, gli utenti in esso presenti devono essere spostati in un altro pool Front End. Dopo la nuova aggiunta dell'SBA alla topologia, gli utenti possono essere ritrasferiti in esso.

La procedura è sintetizzata sotto.

1.  Spostare gli utenti dei siti di succursale presenti nell'SBA in un altro pool Front End.

2.  Rimuovere l'SBA dalla topologia per dissociare il pool Front End esistente come funzione di registrazione di backup.

3.  Aggiornare il pool Front End a Microsoft Lync Server 2013.

4.  Aggiungere nuovamente l'SBA alla topologia.

5.  Associare il nuovo pool Front End all'SBA come funzione di registrazione di backup.

6.  Trasferire nuovamente gli utenti dei siti di succursale nell'SBA.

## Argomenti della sezione

  - [Aggiungere un sito di succursale Survivable Branch Appliance di Lync Server 2013 alla topologia](lync-server-2013-add-lync-server-2013-survivable-branch-appliance-branch-site-to-your-topology.md)

  - [Aggiungere un sito di succursale Survivable Branch Appliance di Lync Server 2010 alla topologia](lync-server-2013-add-lync-server-2010-survivable-branch-appliance-branch-site-to-your-topology.md)

