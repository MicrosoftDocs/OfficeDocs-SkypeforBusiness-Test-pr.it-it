---
title: Migrazione di più siti e pool
TOCTitle: Migrazione di più siti e pool
ms:assetid: 3bf677d4-a5af-4f73-8fad-1abf5b668cc1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688025(v=OCS.15)
ms:contentKeyID: 49887524
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Migrazione di più siti e pool

 

_**Ultima modifica dell'argomento:** 2012-08-26_

Lync Server 2013 supporta distribuzioni multisito e per più pool. Per il processo di migrazione di più pool da Office Communications Server 2007 R2 a Lync Server 2013 è necessario tenere conto delle considerazioni seguenti:

1.  Dopo avere distribuito un pool pilota di Lync Server 2013, è necessario definire un sottoinsieme di utenti pilota che verranno spostati nel pool di Lync Server 2013 e una metodologia per la convalida della funzionalità degli utenti.

2.  Dopo avere distribuito un server perimetrale nel pool pilota, è necessario verificare che gli utenti esterni possano comunicare con il pool di Lync Server 2013.

3.  Dopo la transizione alle route federate dai server perimetrali di Office Communications Server 2007 R2 ai server perimetrali di Lync Server 2013 pilota, è necessario assicurarsi che gli utenti federati possano comunicare con il pool di Lync Server 2013.

4.  Dopo avere spostato tutti gli utenti e gli oggetti contatto non utente, è necessario verificare che il pool di Office Communications Server 2007 R2 sia vuoto.

5.  Dopo avere verificato che il pool di Office Communications Server 2007 R2 sia vuoto, sarà possibile disattivare il pool.
    
    Per informazioni dettagliate su come disattivare i server e il pool di Office Communications Server 2007 R2 legacy, vedere [Fase 10: rimuovere le autorizzazioni del sito legacy](phase-10-decommission-legacy-site.md).

