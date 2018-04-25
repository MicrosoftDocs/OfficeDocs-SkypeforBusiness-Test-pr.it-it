---
title: "Lync Server 2013: Supporto dell'archiviazione di file"
TOCTitle: Supporto dell'archiviazione di file
ms:assetid: ed66430d-3c19-4267-938c-956a51005073
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399073(v=OCS.15)
ms:contentKeyID: 49302375
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supporto dell'archiviazione di file in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-16_

Lync Server 2013 utilizza lo stesso archivio file per tutta l'archiviazione di file. Il supporto dell'archiviazione di file include:

  - Una condivisione file in DAS (Direct Attached Storage) o su una rete di archiviazione (SAN), incluso il file system distribuito (DFS), nonché su RAID (Redundant Array of Independent Disks) per gli archivi file. Per informazioni dettagliate sui requisiti di archiviazione, vedere [Requisiti tecnici per Front End Server, messaggistica istantanea e presenza in Lync Server 2013](lync-server-2013-technical-requirements-for-front-end-servers-instant-messaging-and-presence.md) e [Requisiti hardware e software per il server Director in Lync Server 2013](lync-server-2013-hardware-and-software-requirements-for-the-director.md) nella documentazione relativa alla pianificazione. Per informazioni dettagliate su DFS per sistema operativo Windows Server 2008, vedere la Guida dettagliata ai file system distribuiti in Windows Server 2008 all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=202835](http://go.microsoft.com/fwlink/p/?linkid=202835).

  - Un cluster condiviso per la condivisione file. Se si utilizza un cluster condiviso, è necessario utilizzare server cluster che eseguono Windows Server 2008 o Windows Server 2008 R2. L'utilizzo di server cluster che eseguono una versione precedente di Windows può generare problemi di autorizzazione che impediscono la disponibilità di alcune caratteristiche. Utilizzare Amministrazione cluster per creare le condivisioni file. Per informazioni dettagliate, vedere l'articolo numero 284838 della Microsoft Knowledge Base, "Creazione di una condivisione di file server cluster con cluster.exe" all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=140899](http://go.microsoft.com/fwlink/p/?linkid=140899).

