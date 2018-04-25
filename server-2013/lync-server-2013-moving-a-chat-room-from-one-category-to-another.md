---
title: "Lync Server 2013: Spostamento di una chat room da una categoria all'altra"
TOCTitle: Spostamento di una chat room da una categoria all'altra
ms:assetid: 7e93b8f6-5a18-4476-a432-3918e01bcfa6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ215877(v=OCS.15)
ms:contentKeyID: 49301109
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Spostamento di una chat room da una categoria all'altra in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

È consigliabile non modificare la categoria di una Chat persistente room dopo la sua creazione. Tuttavia, se il gestore della chat room detiene privilegi di **Creatore** in un'altra categoria, può spostare la chat room da una categoria a un'altra. La chat room non viene eliminata e ricreata, ma ne viene modificata l'associazione nel database.

La modifica della categoria di una chat room deve essere un'operazione eseguita raramente. Una categoria determina i membri a cui è consentito accedere alla chat room; se questa viene spostata in un'altra categoria, tutti gli elenchi di controllo di accesso del sistema (SACL) non supportati dalla nuova categoria vengono eliminati. Ad esempio, se un utente membro di una chat room non è più un **AllowedMember** nella nuova categoria, l'appartenenza alla chat risulterà modificata, e l'utente non avrà più accesso alla chat room.

Per informazioni dettagliate sullo spostamento delle chat room attraverso interfaccia della riga di comando Windows PowerShell, vedere "Gestione delle chat room" in [Configurazione del server Chat persistente tramite i cmdlet di Windows PowerShell](configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md).

Per informazioni dettagliate sulla configurazione delle chat room, vedere [Configurare le chat room in Lync Server 2013](lync-server-2013-configure-rooms.md) nella documentazione relativa alla distribuzione.

