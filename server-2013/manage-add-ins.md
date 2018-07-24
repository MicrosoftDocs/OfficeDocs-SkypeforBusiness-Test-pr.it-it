---
title: Gestire i componenti aggiuntivi
TOCTitle: Gestire i componenti aggiuntivi
ms:assetid: b84f868e-b36e-4ab4-b284-7db212d401c3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205193(v=OCS.15)
ms:contentKeyID: 49301759
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestire i componenti aggiuntivi

 

_**Ultima modifica dell'argomento:** 2012-10-06_

Per creare un nuovo componente aggiuntivo del server Chat persistente

    New-CsPersistentChatAddin -Name Contoso -PersistentChatPoolFqdn client.contoso.com -Url http://contoso.com 

## Creare, ottenere, impostare o rimuovere un componente aggiuntivo

Per creare un nuovo componente aggiuntivo

    New-CsPersistentChatAddin -PersistentChatPoolFqdn <String> -Name <String> -Url<String>

> [!important]  
> PersistentChatPoolFqdn &lt;String&gt; è necessario solo vi è più di un pool di server Chat persistente.

Per ottenere un componente aggiuntivo

    Get-CsPersistentChatAddin -Identity <String>]

oppure

    Get-CsPersistentChatAddin -PersistentChatPoolFqdn <String>

Per impostare un componente aggiuntivo

    Set-CsPersistentChatAddIn -Instance <AddinObject> [-Force <Switch Parameter>] [-Confirm <Switch Parameter>]

oppure

    Set-CsPersistentChatAddIn -Identity <String> [-Name <String>] [-Url<String>] [-Force <Switch Parameter>] [-Confirm <Switch Parameter>]

Per rimuovere un componente aggiuntivo

    Remove-CsPersistentChatAddIn -Instance <AddinObject> [-Force <Switch Parameter>] [-Confirm <Switch Parameter>]

oppure

    Remove-CsPersistentChatAddIn -Identity <String> [-Force <Switch Parameter>] [-Confirm <Switch Parameter>]

