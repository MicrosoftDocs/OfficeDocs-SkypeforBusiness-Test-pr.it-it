---
title: Backup di archivi file
TOCTitle: Backup di archivi file
ms:assetid: 1a7f4e93-aa3d-461e-878e-2c572baa1293
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh202167(v=OCS.15)
ms:contentKeyID: 52062105
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Backup di archivi file

 

_**Ultima modifica dell'argomento:** 2013-02-17_

Il backup degli archivi file di Lync Server include tutti i file e le cartelle utilizzati dai componenti di Lync Server.

## Per eseguire il backup degli archivi file

1.  Per trovare i percorsi specifici degli archivi file di Lync Server, aprire Generatore di topologie e cercare nel nodo **Archivi file**.

2.  Utilizzare Robocopy o un altro strumento di gestione del file system per copiare ogni Archivio file in $Backup\\filestore.

