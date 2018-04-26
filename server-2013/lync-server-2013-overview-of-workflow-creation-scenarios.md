---
title: 'Lync Server 2013: Panoramica degli scenari di creazione del flusso di lavoro'
TOCTitle: Panoramica degli scenari di creazione del flusso di lavoro
ms:assetid: 05e0c175-0f1a-4bb1-b048-c68584d00649
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204646(v=OCS.15)
ms:contentKeyID: 49299562
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica degli scenari di creazione del flusso di lavoro in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-17_

Quando si creano flussi di lavoro, i possibili scenari sono due:

  - **L'amministratore crea e configura il flusso di lavoro** — Il membro del ruolo CsResponseGroupAdministrator (o equivalente) crea e attiva il flusso di lavoro e tutti i relativi elementi, ad esempio gruppi di agenti, code, festività, orario di ufficio, musica di attesa e così via.

  - **L'amministratore crea il flusso di lavoro e il responsabile configura le opzioni** — Il membro del ruolo CsResponseGroupAdministrator (o equivalente) definisce l'URI SIP primario, il nome visualizzato, assegna uno o più membri al ruolo CsResponseGroupManager, quindi seleziona una coda e attiva il flusso di lavoro. Il membro del ruolo CsResponseGroupManager può quindi effettuare l'accesso e modificare la configurazione del flusso di lavoro creando gruppi di agenti. Assegna inoltre il gruppo alla coda, configurando numero di telefono, festività, orario di ufficio, musica di attesa e così via.
    

    > [!NOTE]
    > Se si vuole creare un flusso di lavoro gestito è necessario crearlo come attivo. Dopo aver salvato un flusso di lavoro gestito e attivo, sarà possibile modificarlo e disattivarlo.


