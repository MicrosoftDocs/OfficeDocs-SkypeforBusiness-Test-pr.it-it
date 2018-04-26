---
title: Migrazione di più siti e pool
TOCTitle: Migrazione di più siti e pool
ms:assetid: a6d726d2-564d-4b39-a97c-5656a673292a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205165(v=OCS.15)
ms:contentKeyID: 49301580
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Migrazione di più siti e pool

 

_**Ultima modifica dell'argomento:** 2012-09-17_

Lync Server 2013 supporta distribuzioni multisito e per più pool. Per il processo di migrazione di più pool da Lync Server 2010 a Lync Server 2013 è necessario tenere conto delle considerazioni seguenti:

1.  Dopo avere distribuito un pool pilota di Lync Server 2013, è necessario definire un sottoinsieme di utenti pilota che verranno spostati nel pool di Lync Server 2013 e una metodologia per la convalida della funzionalità degli utenti. Ad esempio, dopo avere spostato un utente nel pool pilota, verificare che i criteri di conferenza dell'utente siano stati spostati in Lync Server 2013.

2.  Dopo avere distribuito un server perimetrale nel pool pilota, è necessario verificare che gli utenti esterni possano comunicare con il pool di Lync Server 2013.

3.  Dopo la transizione alle route federate dai server perimetrali di Lync Server 2010 ai server perimetrali di Lync Server 2013 pilota, è necessario assicurarsi che gli utenti federati possano comunicare con il pool di Lync Server 2013.

4.  Dopo avere spostato tutti gli utenti e gli oggetti contatto non utente, è necessario verificare che il pool di Lync Server 2010 sia vuoto.

5.  Dopo avere verificato che il pool di Lync Server 2010 sia vuoto, sarà possibile disattivare il pool.
    
    Per informazioni dettagliate su come disattivare i server e il pool di Lync Server 2010 legacy, vedere [Fase 8: rimuovere le autorizzazioni dei pool legacy](phase-8-decommission-legacy-pools.md).

