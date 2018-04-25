---
title: 'Lync Server 2013: Eliminazione di un messaggio o dei messaggi obsoleti'
TOCTitle: Eliminazione di un messaggio o dei messaggi obsoleti
ms:assetid: 3f0c612d-6dfd-41a4-a5fe-5ff3448eb0ce
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ215874(v=OCS.15)
ms:contentKeyID: 49300306
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminazione di un messaggio o dei messaggi obsoleti in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-02-05_

Un amministratore di Chat persistente può eliminare un messaggio da una chat Chat persistente e facoltativamente sostituirlo con un altro. Gli amministratori possono inoltre eliminare i messaggi durante le operazioni di manutenzione in modo da ridurre l'aumento delle dimensioni del database. Ad esempio, questo comando Windows PowerShell consente di rimuovere dalla chat room ITChatRoom tutti i i messaggi pubblicati dall'utente kenmyer@litwareinc.com

    Remove-CsPersistentChatMessage -Identity "atl-persistentchat-001.litwareinc.com\ITChatRoom" -UserUri "sip:kenmyer@litwareinc.com"

Questo esempio consente invece di sostituire tutti i messaggi rimossi con la nota in cui si informa che il messaggio non è più disponibile:

    Remove-CsPersistentChatMessage -Identity "atl-persistentchat-001.litwareinc.com\ITChatRoom" -UserUri "sip:kenmyer@litwareinc.com" -ReplaceMessage "This message is no longer available."

Per ulteriori informazioni, vedere l'argomento della Guida per il cmdlet [Remove-CsPersistentChatMessage](remove-cspersistentchatmessage.md).

