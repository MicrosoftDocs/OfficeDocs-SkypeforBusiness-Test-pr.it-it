---
title: 'Lync Server 2013: Eseguire, concedere, ottenere, rimuovere o impostare criteri di Chat persistente'
TOCTitle: Eseguire, concedere, ottenere, rimuovere o impostare criteri di Chat persistente
ms:assetid: 39ccdbe8-fb3d-47bc-96e2-9486b6d317e0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204810(v=OCS.15)
ms:contentKeyID: 49300236
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eseguire, concedere, ottenere, rimuovere o impostare criteri di Chat persistente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-01_

Per creare nuovi criteri Chat persistente

    New-CsPersistentChatPolicy -Identity <XdsIdentity> [-Enable <Switch Parameter>] [-Confirm <Switch Parameter>] [-Force <Switch Parameter>] [-WhatIf <Switch Parameter>] [-InMemory <Switch Parameter>]

Per assegnare criteri Chat persistente

    Grant-CsPersistentChatPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm <Switch Parameter>] [-WhatIf <Switch Parameter>]

Per ottenere criteri Chat persistente

    Get-CsPersistentChatPolicy [-Identity <XdsIdentity>] [-Filter <String>] [-LocalStore <Switch Parameter>]

Per rimuovere criteri Chat persistente

    Remove-CsPersistentChatPolicy -Identity <XdsIdentity> [-Confirm <Switch Parameter>] [-Force <Switch Parameter>] [-WhatIf <Switch Parameter>]

Per impostare criteri Chat persistente

    Set-CsPersistentChatPolicy [-Identity <XdsIdentity>] [-Instance < PSObject>]

