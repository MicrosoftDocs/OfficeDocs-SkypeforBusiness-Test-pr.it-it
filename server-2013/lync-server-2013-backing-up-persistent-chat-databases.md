---
title: Backup dei database di Chat persistente
TOCTitle: Backup dei database di Chat persistente
ms:assetid: b99ebdc0-a025-44d7-9d74-37a7365f330d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945646(v=OCS.15)
ms:contentKeyID: 52062252
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Backup dei database di Chat persistente

 

_**Ultima modifica dell'argomento:** 2013-02-17_

Il contenuto della Chat persistente viene archiviato nel database Chat persistente (Mgc.mdf). Si tratta di dati critici per l'azienda di cui deve essere eseguito un backup periodico. Oltre al contenuto della chat room, nel database Chat persistente vengono archiviate anche le informazioni sulle entità (ad esempio, utenti e gruppi di utenti), i ruoli e l'accesso che hanno alle chat room e al contenuto delle chat room.

Esistono due modi per eseguire il backup dei dati della Chat persistente.

  - Backup di SQL Server

  - Cmdlet `Export-CsPersistentChatData`, che esporta i dati della Chat persistente come file

Per i dati creati utilizzando il backup di SQL Server è necessario molto più spazio su disco, anche 20 volte di più, che per quelli creati da `Export-CsPersistentChatData`. Il backup di SQL Server è tuttavia una procedura con cui gli amministratori hanno probabilmente più familiarità.

