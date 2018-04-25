---
title: 'Lync Server 2013: Disponibilità elevata della condivisione di file'
TOCTitle: Disponibilità elevata della condivisione di file
ms:assetid: b8c8d5ec-9397-4128-8d1e-8ec6c30fade7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205203(v=OCS.15)
ms:contentKeyID: 49301766
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disponibilità elevata della condivisione di file in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-03-30_

Per garantire una disponibilità elevata per la condivisione file di Lync Server in un singolo data center, è possibile utilizzare il file system distribuito (DFS, Distributed File System). DFS supporta il failover da un file server a un altro all'interno dello stesso data center. Per una distribuzione su larga scala, è consigliabile utilizzare file server dedicati accoppiati mediante DFS.

A seconda delle dimensioni della rete e del grado di resilienza desiderato, è possibile utilizzare una coppia di server per ospitare tutte le condivisioni file in un sito oppure utilizzare una coppia per ogni pool Front End.

DFS è un meccanismo che esegue la replica nel miglior modo possibile in base alle condizioni esistenti, senza alcun impegno pubblicato relativamente al raggiungimento degli obiettivi in termini di tempo di ripristino (RTO, Recovery Time Objective) o di punto di ripristino (RPO, Recovery Point Objective). Il failover tra i server DFS dovrebbe avvenire rapidamente, ma il ritardo della replica dei dati può impedire agli utenti di proseguire con il lavoro che stavano svolgendo quando si verifica il failover.

Se si utilizza DFS e l'archivio dati nella condivisione file è importante, è consigliabile eseguire frequentemente il backup delle condivisioni file, ad esempio ogni 4-8 ore. Quando una condivisione file non è più attiva e la replica non è aggiornata, è possibile utilizzare il backup per ripristinare il contenuto del server con problemi nell'altro server accoppiato al server attualmente non disponibile.

