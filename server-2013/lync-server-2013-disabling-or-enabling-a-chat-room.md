---
title: 'Lync Server 2013: Disabilitazione o abilitazione di una chat room'
TOCTitle: Disabilitazione o abilitazione di una chat room
ms:assetid: db0908fc-aae3-46e8-bc0b-245e9adfa1e2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ215883(v=OCS.15)
ms:contentKeyID: 49302175
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disabilitazione o abilitazione di una chat room in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-02-05_

Se l'argomento di una chat room di Chat persistente non è più rilevante, è possibile rendere la chat room non disponibile agli utenti disabilitandola. Quando si disabilita una chat room, tutti i membri vengono disconnessi immediatamente. Dopo la disabilitazione di una chat room, gli utenti non possono più parteciparvi né trovarla eseguendo ricerche di chat room.

Una chat room disabilitata può essere successivamente abilitata da un amministratore di Chat persistente. Se una chat è disabilitata, il relativo elenco dei membri e le altre impostazioni vengono mantenuti. In questo modo, se si decide di riabilitarla, non sarà necessario ricreare manualmente le impostazioni.

Se è configurata la persistenza della cronologia della chat room, il contenuto verrà mantenuto in caso di disabilitazione della chat room. La persistenza della cronologia della chat room è un'impostazione facoltativa di una categoria e viene applicata a tutte le chat room della categoria. Per impostazione predefinita, la persistenza è abilitata, ma è possibile disabilitarla impostando la proprietà **Abilita cronologia chat** della categoria su false. Se si disabilita una chat room, il contenuto tuttavia non verrà visualizzato nelle ricerche per tutto il tempo in cui la chat room resterà disabilitata. Se successivamente si abilita la chat room, gli utenti potranno ricercare messaggi inseriti prima che la chat room venisse disabilitata.

Per informazioni dettagliate sulla disabilitazione e l'abilitazione delle chat room tramite interfaccia della riga di comando Windows PowerShell, vedere l'argomento relativo alla gestione delle chat room in [Configurazione del server Chat persistente tramite i cmdlet di Windows PowerShell](configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md). Per disabilitare una chat room, utilizzare un comando simile al seguente:

    Set-CsPersistentChatRoom -Identity "atl-cs-001.litwareinc.com\ITChatRoom" -Disabled $True

Per abilitare una chat room, impostare la proprietà Disabled su False:

    Set-CsPersistentChatRoom -Identity "atl-cs-001.litwareinc.com\ITChatRoom" -Disabled $False

Si noti che non è possibile abilitare o disabilitare le chat room mediante il Pannello di controllo di Lync Server.

Per informazioni dettagliate sulla configurazione delle chat room, vedere [Configurare le chat room in Lync Server 2013](lync-server-2013-configure-rooms.md) nella documentazione relativa alla distribuzione.

