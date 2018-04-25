---
title: 'Lync Server 2013: Modalità di bypass multimediale'
TOCTitle: Modalità di bypass multimediale
ms:assetid: 38c06c81-7e45-4423-9e00-7fbfa4befe46
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425862(v=OCS.15)
ms:contentKeyID: 49300214
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modalità di bypass multimediale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-05_

È necessario configurare il bypass multimediale sia a livello globale che per i singoli trunk PSTN. Quando si abilita il bypass multimediale a livello globale, sono disponibili due opzioni, ovvero **Ignora sempre** e **Usa le informazioni del sito e dell'area** .

Come indicato dal nome, **Ignora sempre** indica che verrà tentato di eseguire il bypass per tutte le chiamate PSTN. L'opzione **Ignora sempre** viene utilizzata per le distribuzioni in cui non è necessario abilitare il servizio Controllo di ammissione di chiamata né specificare informazioni di configurazione dettagliate in cui indicare quando tentare di eseguire il bypass multimediale. L'opzione **Ignora sempre** viene utilizzata inoltre quando esiste la connettività completa tra i client e i gateway PSTN. In questa configurazione tutte le subnet sono mappate a un solo ID bypass, calcolato dal sistema.

Con **Utilizza configurazione siti e aree** , l'ID bypass associato alla configurazione dei siti e delle aree viene utilizzato per decidere se eseguire il bypass. Questa configurazione consente di configurare il bypass per le topologie più comuni, poiché offre un controllo granulare su quando eseguire il bypass, oltre a supportare le interazioni con il servizio Controllo di ammissione di chiamata. Il sistema tenta di semplificare l'attività assegnando automaticamente gli ID bypass come indicato di seguito.

  - Il sistema assegna automaticamente un singolo ID bypass univoco a ogni area.

  - Ogni sito connesso a un'area tramite un collegamento WAN senza vincoli di larghezza di banda eredita lo stesso ID bypass dell'area.

  - A un sito associato all'area tramite un collegamento WAN con vincoli di larghezza di banda è assegnato un ID bypass diverso rispetto a quello dell'area.

  - Le subnet associate a ogni sito ereditano l'ID bypass del sito.

## Vedere anche

#### Concetti

[Panoramica del bypass multimediale in Lync Server 2013](lync-server-2013-overview-of-media-bypass.md)  
[Bypass multimediale e controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-media-bypass-and-call-admission-control.md)  
[Requisiti tecnici per il bypass multimediale in Lync Server 2013](lync-server-2013-technical-requirements-for-media-bypass.md)

