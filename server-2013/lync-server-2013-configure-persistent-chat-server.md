---
title: 'Lync Server 2013: Configurare il server Chat persistente'
TOCTitle: Configurare il server Chat persistente
ms:assetid: 85028aff-a38e-4748-958e-59e707a47532
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205054(v=OCS.15)
ms:contentKeyID: 49301197
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare il server Chat persistente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-06_

Per creare una nuova configurazione di Chat persistente

    New-CsPersistentChatConfiguration -Identity <XdsIdentity> [-DefaultChatHistory <Integer>] [-MaxChatContentSizeMB <Integer>] [-MaxFileSizeKB <Integer>] [-ParticipantUpdateLimit <Integer>] [-FileServiceUrl <UrlForFileUpload>] [-RoomManagementUrl <RoomManagementUrl>] [-Instance <PSObject>] [-Force <Switch Parameter>] [-Confirm <Switch Parameter>] [-WhatIf <Switch Parameter>]

Per ottenere la configurazione di Chat persistente

    Get-CsPersistentChatConfiguration [-LocalStore <Switch Parameter>] [-Identity <XdsIdentity>]

Per rimuovere la configurazione di Chat persistente

    Remove-CsPersistentChatConfiguration -Identity <XdsIdentity>

Per impostare la configurazione di Chat persistente

    Set-CsPersistentChatConfiguration [-DefaultChatHistory <Integer>] [-MaxChatContentSizeMB <Integer>] [-MaxFileSizeKB <Integer>] [-ParticipantUpdateLimit <Integer>] [-FileServiceUrl <UrlForFileUpload>] [-RoomManagementUrl <RoomManagementUrl>] [-Instance <PSObject >] [-Force <Switch Parameter>] [-Confirm <Switch Parameter>] [-WhatIf <Switch Parameter>]

In Lync Server 2013, tutto il traffico dei servizi Web è supportato da Lync Server 2013, Front End Server. Pertanto, l'indirizzo gcweb01 sul server Chat persistente non è necessario. L'accesso al servizio Web interno è ancora supportato poiché è offerto il servizio Web di Download e Upload file al sito Web *interno* (ma non al sito Web *esterno* per gli utenti remoti).

