---
title: 'Lync Server 2013: Creazione o modifica di una nuova chat room'
TOCTitle: Creazione o modifica di una nuova chat room
ms:assetid: aa8f4349-cfd9-4036-9c4d-de8fb2c4c8a4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ215880(v=OCS.15)
ms:contentKeyID: 49301615
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creazione o modifica di una nuova chat room in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-19_

La configurazione delle chat room di Chat persistente in genere viene gestita dagli utenti. Un amministratore di Chat persistente di solito non configura o gestisce le chat room. I cmdlet di Windows PowerShell per gestire le chat room sono disponibili solo per gli amministratori **CsPersistentChatAdministrator**.

Gli utenti con il ruolo di **Autori** in una determinata categoria possono utilizzare il client Lync per creare e gestire le chat room. Gli utenti designati come responsabili di una specifica chat room possono inoltre occuparsi della gestione continuata della chat room, ad esempio modificandone le proprietà o i membri.

> [!tip]  
> Gli amministratori di Chat persistente possono essere anche autori e non sono soggetti alle restrizioni applicate agli autori.

Facoltativamente, se si è amministratori di Chat persistente, è possibile utilizzare un'interfaccia utente per creare e gestire le chat room invece di avvalersi dei cmdlet di Windows PowerShell. A tale scopo, abilitare per SIP un amministratore del server Chat persistente e quindi utilizzare il client Lync per creare e gestire le chat room.

Se si desidera creare un flusso di lavoro personalizzato per la gestione delle chat room per gli utenti, è possibile impostare la proprietà **RoomManagementUrl** nella configurazione del server Chat persistente in modo da reindirizzare gli utenti alla soluzione personalizzata dal client Lync.

Per informazioni dettagliate sulla configurazione delle chat room mediante interfaccia della riga di comando Windows PowerShell, vedere la sezione relativa alla gestione delle chat room in [Configurazione del server Chat persistente tramite i cmdlet di Windows PowerShell](configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md).

Per informazioni dettagliate sulla configurazione delle chat room, vedere [Configurare le chat room in Lync Server 2013](lync-server-2013-configure-rooms.md) nella documentazione relativa alla distribuzione.

