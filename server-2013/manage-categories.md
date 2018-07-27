---
title: Gestire le categorie
TOCTitle: Gestire le categorie
ms:assetid: 1b118d91-b4c4-4b2f-b842-b451417ec2c6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204719(v=OCS.15)
ms:contentKeyID: 49299835
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestire le categorie

 

_**Ultima modifica dell'argomento:** 2012-10-06_

Per creare una nuova categoria server Chat persistente

    New-CsPersistentChatCategory -Name Foo -PersistentChatPoolFqdn client.contoso1b118d91-b4c4-4b2f-b842-b451417ec2c6.com [other parameters]

> [!IMPORTANT]  
> PersistentChatPoolFqdn è necessario solo in presenza di più pool di server Chat persistente.

Per apportare modifiche a una categoria server Chat persistente esistente

    Set-CsPersistentChatCategory -Identity testCat -AllowedMembers @{Add="sip:user1@contoso.com", "CN=container,DC=contoso,DC=com"}  -DeniedMembers @{Add="sip:user2@contoso.com"}
    Set-CsPersistentChatCategory -Identity testCat -Creators @{Add="sip:user1@contoso.com"}

In Windows PowerShell è possibile impostare AllowedMembers, DeniedMembers e Creators contemporaneamente. Creators sarà il sottoinsieme di AllowedMembers meno DeniedMembers. È inoltre possibile impostare le proprietà di una categoria contemporaneamente ai membri e agli autori.

## Creare, ottenere, impostare o rimuovere una categoria

Per creare una nuova categoria

    New-CsPersistentChatCategory -Name <String> [-PersistentChatPoolFqdn <String>] [-Description <String>] [-EnableInvitations<Switch Parameter>] [-EnableFileUpload <Switch Parameter>] [-RemoveChatHistory <Switch Parameter>] [-MaxContentSize <Integer>]

Per ottenere una categoria

    Get-CsPersistentChatCategory -Identity <String>

oppure

    Get-CsPersistentChatCategory -PersistentChatPoolFqdn <String>

Per impostare una categoria

    Set-CsPersistentChatCategory -Instance <CategoryObject> [-WhatIf] [-Confirm] [<CommonParameters>]

oppure

    Set-CsPersistentChatCategory [-Identity] <string> [-Name <string>] [-Description <string>] [-Invitations <bool>] [-FileUpload <bool>] [-ChatHistory <bool>] [-AllowedMembers <PSListModifier[string]>] [-DeniedMembers <PSListModifier[string]>] [-Creators <PSListModifier[string]>] [-WhatIf] [-Confirm]  [<CommonParameters>]

Per rimuovere una categoria

    Remove-CsPersistentChatCategory -Instance <CategoryObject> [-Force <Switch Parameter>] [-Confirm <Switch Parameter>]

oppure

    Remove-CsPersistentChatCategory -Identity <String> [-Force <Switch Parameter>] [-Confirm <Switch Parameter>]

