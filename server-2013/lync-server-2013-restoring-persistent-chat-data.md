---
title: Ripristino di dati di Chat persistente
TOCTitle: Ripristino di dati di Chat persistente
ms:assetid: c251a7fa-50da-434b-b39a-17f5978ce736
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945649(v=OCS.15)
ms:contentKeyID: 52062259
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ripristino di dati di Chat persistente

 

_**Ultima modifica dell'argomento:** 2013-02-18_

Il contenuto della Chat persistente viene archiviato nel database Chat persistente (mgc.mdf). Si tratta di dati critici per l'azienda di cui deve essere eseguito un backup periodico. Oltre al contenuto della chat room, nel database Chat persistente vengono archiviati anche le entità (ad esempio, utenti e gruppi) e i ruoli e l'accesso che hanno alle chat room e il contenuto delle chat room.

La modalità di ripristino dei dati della Chat persistente dipende dal metodo utilizzato per eseguirne il backup.

  - Se sono state utilizzate le procedure di backup di SQL Server, è necessario utilizzare le procedure di ripristino di SQL Server.

  - Se è stato utilizzato il cmdlet **Export-CsPersistentChatData** per eseguire il backup dei dati della Chat persistente, è necessario utilizzare il cmdlet **Import-CsPersistentChatData** per ripristinare i dati.

