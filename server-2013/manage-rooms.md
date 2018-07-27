---
title: Gestire le chat room
TOCTitle: Gestire le chat room
ms:assetid: d4835cf4-cd09-4769-a08e-e92706861b64
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205292(v=OCS.15)
ms:contentKeyID: 49302079
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestire le chat room

 

_**Ultima modifica dell'argomento:** 2013-02-21_

Per creare una nuova chat room di server Chat persistente

    New-CsPersistentChatRoom -Name Foo1 -PersistentChatPoolFqdn client.contoso.com -Category client.contoso.com\Foo [other parameters]

> [!IMPORTANT]  
> -PersistentChatPoolFqdn non è necessario se si verifica una delle condizioni seguenti:<ul>
> <li><p>È presente un solo pool di server Chat persistente.</p></li>
> 
> <li><p>Si specifica l'FQDN di un pool per la categoria.</p></li>
> 
> 
> <li><p>Si specifica l'FQDN di un pool per l'aggiunta della chat room.</p></li></ul>


Per apportare modifiche a una chat room di server Chat persistente esistente

    Set-CsPersistentChatRoom -Identity testCat -Members @{Add="sip:user1@contoso.com", "CN=container,DC=contoso,DC=com"}
    Set-CsPersistentChatRoom -Identity testCat -Managers @{Add="sip:user2@contoso.com"}
    Set-CsPersistentChatRoom -Identity testCat -Presenters @{Add="sip:user1@contoso.com"}

Windows PowerShell: i membri (Members), i responsabili (Managers) e i relatori (Presenters) possono essere impostati simultaneamente. Dovrebbero corrispondere tutti al sottoinsieme di AllowedMembers meno DeniedMembers della categoria (Category) host. Una chat room definita come type=normal non può includere relatori (Presenters).

## Creare, ottenere, impostare, cancellare o rimuovere una chat room

Per creare una nuova chat room

    New-CsPersistentChatRoom -Name <String> [-PersistentChatPoolFqdn <String>]-Category <String> [-Description <String>] [-Disabled <Switch Parameter>] [-Type <Normal | Auditorium>] [-AddIn <String>] [-Privacy <ChatRoomPrivacy> {Open | Closed | Secret}] [-Invitations <Switch Parameter>]

Per impostare una chat room

    Set-CsPersistentChatRoom -Identity <String> [-Name <String>] [-Category <String>] [-Description <String>] [-Disabled <boolean>] [-Type <Normal | Auditorium>] [-AddIn <String>] [-Privacy <ChatRoomPrivacy> {Open | Closed | Secret}] [-Invitations <Enum>] [-Members <PSListModifier<String>>] [-Managers <PSListModifier<String>>] [-Presenters <PSListModifier<String>>] [-Force < Switch Parameter >] [-Confirm <Switch Parameter>][-WhatIf <Switch Parameter>]

Per ottenere una chat room

    Get-CsPersistentChatRoom -Identity <String>

oppure

    Get-CsPersistentChatRoom -filter <String> [-PersistentChatPoolFqdn <String>] [-SearchDescription] [-Member <String>] [-Manager <string>] [-Category <string>] [-Addin <string>] [-Disabled <bool>] [-Privacy <ChatRoomPrivacy> {Open | Closed | Secret}] [-Type <ChatRoomType> {Normal | Auditorium}] [-Invitations <ChatRoomInvitations> {False | Inherit}] [-ChatContentExceedsMB <int>] [-ResultSize <int>]

dove –filter supporta solo Name e Description e consente di trovare chat room in cui Name/Description corrisponde alla stringa della parola chiave. PoolFqdn esegue la ricerca in un pool di server Chat persistente specifico.

Per cancellare una chat room e per cancellare i messaggi di una chat room

    Clear-CsPersistentChatRoom [-Identity] <string> -EndDate <DateTime> [-WhatIf] [-Confirm]  [<CommonParameters>]

oppure

    Clear-CsPersistentChatRoom [-Instance] <ChatRoomObject> -EndDate <DateTime> [-WhatIf] [-Confirm] [<CommonParameters>]

Per rimuovere una chat room

    Remove-CsPersistentChatRoom [-Identity] <string> [-Force] [-WhatIf] [-Confirm]  [<CommonParameters>]

oppure

    Remove-CsPersistentChatRoom [-Instance] <ChatRoomObject> [-Force] [-WhatIf] [-Confirm]  [<CommonParameters>]

