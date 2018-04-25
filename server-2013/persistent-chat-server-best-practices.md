---
title: Procedure consigliate per il server Chat persistente
TOCTitle: Procedure consigliate per il server Chat persistente
ms:assetid: dc18e7f7-599b-4d32-abf7-cd9e691426a2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398970(v=OCS.15)
ms:contentKeyID: 49302182
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Procedure consigliate per il server Chat persistente

 

_**Ultima modifica dell'argomento:** 2012-10-06_

Quando si creano categorie e chat room di Chat persistente e si definiscono ambiti e appartenenze, i suggerimenti seguenti possono rivelarsi utili per la pianificazione:

  - Se l'organizzazione non richiede l'applicazione di un "ethical wall", ovvero una zona priva di comunicazione tra reparti distinti di una società o di un'organizzazione per evitare conflitti di interesse, non restringere in alcun modo l'ambito nell'albero delle categorie. Inserire tutti gli utenti nell'ambito di una categoria e creare tutte le chat room all'interno di tale categoria. Utilizzare quindi solo gli elenchi dei membri per concedere o limitare l'accesso per ogni chat room.

  - Nella maggior parte dei casi, è consigliabile consentire agli utenti di creare nuove chat room, in modo che sia possibile avviare discussioni relative a nuovi argomenti in qualsiasi momento. Per ottenere questo risultato, definire un elenco **Creators** uguale all'elenco **AllowedMembers**. Se tuttavia si desidera consentire la creazione di chat room solo a un team di supporto centrale o a utenti designati, definire l'elenco **Creators** come sottoinsieme appropriato.

  - Assegnare a ogni chat room un nome completo e un riepilogo descrittivo per consentirne l'individuazione nell'organizzazione. Poiché gli utenti non possono visualizzare il nome della categoria di appartenenza, non è possibile basarsi su tale nome per consentire agli utenti di individuare il forum di discussione previsto per la chat room.

  - Se si desidera implementare convenzioni di denominazione oppure altri controlli di accesso o convalide, è possibile definire un flusso di lavoro personalizzato per la creazione di chat room. La configurazione di Chat persistente consente di personalizzare il valore di **RoomManagementUrl** impostandolo su una soluzione ospitata. Quando ad esempio gli utenti fanno clic su **Crea una chat room** nel client Lync, possono essere reindirizzati alla soluzione personalizzata.

  - Creare un'ampia gamma di componenti aggiuntivi per migliorare l'utilizzo delle chat room con l'aggiunta di altri dati business. Gli amministratori devono registrare i componenti aggiuntivi che desiderano abilitare nel sistema. I responsabili e i creatori delle chat room possono scegliere dall'elenco dei componenti aggiuntivi consentiti quelli più pertinenti per le proprie chat room.

## Vedere anche

#### Ulteriori risorse

[Gestione di categorie, chat room e componenti aggiuntivi in Lync Server 2013](lync-server-2013-managing-categories-rooms-and-add-ins.md)

