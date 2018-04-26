---
title: Eseguire la migrazione di riunioni e di contenuto di riunioni esistenti
TOCTitle: Eseguire la migrazione di riunioni e di contenuto di riunioni esistenti
ms:assetid: 30516731-2ae1-4a6d-a7e1-d3f05778c954
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688011(v=OCS.15)
ms:contentKeyID: 49887501
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eseguire la migrazione di riunioni e di contenuto di riunioni esistenti

 

_**Ultima modifica dell'argomento:** 2013-02-22_

Quando un account utente viene spostato da Lync Server 2010 in un server Lync Server 2013, vengono spostate anche le informazioni seguenti:

  - **Le riunioni già pianificate dall'utente**. Vengono spostate anche le directory e i dati delle conferenze.

  - **Il PIN dell'utente**. Il PIN corrente dell'utente continua a funzionare fino alla scadenza o alla richiesta di un nuovo PIN da parte dell'utente stesso.

Le seguenti informazioni sull'account utente non vengono spostate nel nuovo server.

  - **Contenuto delle riunioni**. Per spostare il contenuto condiviso durante una riunione, ad esempio PowerPoint, Lavagna, allegati o dati dei sondaggi, usare il parametro **-MoveConferenceData** come parte del cmdlet **Move-CsUser**.

