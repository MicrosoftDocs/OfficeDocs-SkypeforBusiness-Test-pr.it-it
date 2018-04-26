---
title: 'Lync Server 2013: Eliminazione di una chat room o una categoria'
TOCTitle: Eliminazione di una chat room o una categoria
ms:assetid: adccb869-0015-4eba-ac73-718bac7843b5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ215881(v=OCS.15)
ms:contentKeyID: 49301658
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminazione di una chat room o una categoria in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Le chat room di Chat persistente possono essere eliminate. Se una chat room non viene più utilizzata, è possibile disabilitarla. Per informazioni dettagliate, vedere [Disabilitazione o abilitazione di una chat room in Lync Server 2013](lync-server-2013-disabling-or-enabling-a-chat-room.md).

Un amministratore di Chat persistente può richiedere tramite query le chat room disabilitate e cancellare periodicamente ed eliminare definitivamente le chat room mediante il cmdlet **Remove-CsPersistentChatRoom** di Windows PowerShell.

Le categorie possono essere eliminate. Tuttavia, per eliminare una categoria, è prima necessario eliminare tutte le chat room che appartengono a essa oppure spostare le chat room in una nuova categoria, lasciando una categoria vuota per l'eliminazione. Il server Chat persistente non consente di eliminare una categoria contenente chat room. Per informazioni dettagliate, vedere [Spostamento di una chat room da una categoria all'altra in Lync Server 2013](lync-server-2013-moving-a-chat-room-from-one-category-to-another.md).

Per informazioni dettagliate sull'eliminazione di categorie vuote mediante interfaccia della riga di comando Windows PowerShell, vedere la sezione relativa alla gestione delle chat room in [Configurazione del server Chat persistente tramite i cmdlet di Windows PowerShell](configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md).

Per informazioni dettagliate sulle chat room e sulle categorie, vedere [Configurare le chat room in Lync Server 2013](lync-server-2013-configure-rooms.md) and [Configurare le categorie in Lync Server 2013](lync-server-2013-configure-categories.md) nella documentazione relativa alla distribuzione.

