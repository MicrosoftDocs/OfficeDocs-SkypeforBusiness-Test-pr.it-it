---
title: "Lync Server 2013: Aggiunge domini utenti e gruppi di utenti a chat room"
TOCTitle: Aggiunta dei domini di utenti e gruppi di utenti alla categoria della chat room
ms:assetid: ee03f2cf-1c84-41c4-b524-d0729be33b8c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ215884(v=OCS.15)
ms:contentKeyID: 49302399
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aggiunta dei domini di utenti e gruppi di utenti alla categoria della chat room in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-02-07_

Per aggiungere gruppi più ampi di utenti a una chat room, vedere [Configurare le categorie in Lync Server 2013](lync-server-2013-configure-categories.md) e [Gestire le categorie](manage-categories.md) nella documentazione relativa alla distribuzione. Ad esempio, questo comando consente di aggiungere tutti gli utenti dell'unità organizzativa NorthAmericaUsers di Active Directory alla chat room NorthAmerica:

    Set-CsPersistentChatRoom -PersistentChatPoolFqdn "atl-cs-001.litwareinc.com\NorthAmerica" -Members @{Add="OU=NorthAmericaUsers,DC=litwareinc,DC=com"}

Con questo comando tutti i membri del gruppo di distribuzione Finance verranno aggiunti alla stessa chat room:

    Set-CsPersistentChatRoom -PersistentChatPoolFqdn "atl-cs-001.litwareinc.com\NorthAmerica" -Members @{Add="CN=Finance,OU=ExternalUsers,DC=litwareinc,DC=com"}

