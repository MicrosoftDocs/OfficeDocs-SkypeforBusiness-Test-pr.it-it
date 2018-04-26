---
title: 'Lync Server 2013: Configurare le chat room'
TOCTitle: Configurare le chat room
ms:assetid: 8956bd2c-c863-4704-bc65-5c0d83556258
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205067(v=OCS.15)
ms:contentKeyID: 49301247
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare le chat room in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-06_

La configurazione delle Chat persistente room è solitamente gestita da utenti o altri team centrali attraverso interfaccia della riga di comando Windows PowerShell; raramente gli amministratori gestiscono le chat room. Tuttavia, se si ha bisogno di creare e gestire chat room, è possibile utilizzare interfaccia della riga di comando Windows PowerShell o aggiungere se stessi come membri della chat room e utilizzare il client Lync 2013.

Per informazioni dettagliate sulla configurazione delle chat room mediante interfaccia della riga di comando Windows PowerShell, vedere la sezione relativa alla gestione delle chat room in [Configurazione del server Chat persistente tramite i cmdlet di Windows PowerShell](configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md).

## Gestione dei dati nelle chat room

server Chat persistente consente agli utenti di collaborare attraverso la pubblicazione di messaggi nelle Chat persistente room. I dati restano sul server, e i membri della chat room possono accedere ai dati, compresi quelli della cronologia. Tuttavia, utenti con ruoli diversi avranno un tipo di accesso diverso ai dati sul server, come illustrato nell'elenco di seguito.

  - Gli amministratori possono eliminare dalla chat room il contenuto meno recente, ad esempio il contenuto pubblicato prima di una certa data, affinché il database non raggiunga dimensioni troppo elevate. Possono inoltre eliminare o spostare messaggi considerati inappropriati per una particolare chat room.

  - Gli utenti finali, compresi gli autori dei messaggi, non possono eliminare il contenuto da una chat room.

  - I gestori di chat room possono disattivare le chat room, ma non eliminarle. Solo gli amministratori possono eliminare una chat room dopo che è stata creata.

Dopo avere eliminato un messaggio, non è possibile annullare l'operazione. Tuttavia, se esiste un backup, è possibile ripristinare i messaggi eliminati. Se è abilitato un server di conformità della Chat persistente, i messaggi restano nel database di conformità.


> [!NOTE]
> Questo tipo di utilizzo dei dati delle chat room si applica, in Lync Server 2013, all'applicazione API di server Chat persistente, ad eccezione dei casi in cui è coinvolto il ruolo di amministratore. L'API della server Chat persistente non può essere utilizzata per eseguire le operazioni dell'amministratore, che devono invece essere eseguite in Lync Server Management Shell.


