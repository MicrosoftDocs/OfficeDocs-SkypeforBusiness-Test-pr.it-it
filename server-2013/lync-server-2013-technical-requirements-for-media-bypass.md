---
title: 'Lync Server 2013: Requisiti tecnici per il bypass multimediale'
TOCTitle: Requisiti tecnici per il bypass multimediale
ms:assetid: 6162a204-0e7c-460a-8eb2-e592c6590a8a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398435(v=OCS.15)
ms:contentKeyID: 49300746
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti tecnici per il bypass multimediale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

Per ogni chiamata alla rete PSTN, il Mediation Server determina se i dati multimediali dall'endpoint Lync di origine possono essere inviati direttamente a un peer Mediation Server senza passare attraverso il Mediation Server. Il peer può essere un gateway PSTN, un IP-PBX o un SBC (Session Border Controller) presso un provider di servizi di telefonia Internet (ITSP) associato al trunk tra il Mediation Server in cui viene instradata la chiamata.

Il bypass multimediale può essere utilizzato quando vengono soddisfatti i requisiti seguenti:

  - Un peer Mediation Server deve supportare le capacità necessarie per il bypass multimediale, la più importante delle quali è la possibilità di gestire più risposte inoltrate, note come "dialoghi anticipati". Rivolgersi al produttore del gateway o del PBX o al provider di servizi di telefonia Internet per ottenere il numero massimo di dialoghi anticipati accettato da gateway, PBX o SBC.

  - Il peer Mediation Server deve accettare traffico multimediale direttamente dagli endpoint di Lync. Molti provider di servizi di telefonia Internet consentono la ricezione del traffico ai controller SBC solo dal Mediation Server. Contattare il provider di servizi di telefonia Internet per stabilire se il relativo SBC accetta traffico multimediale direttamente dagli endpoint di Lync.

  - I client Lync e un peer Mediation Server devono essere ben connessi, ovvero posizionati nella stessa area di rete oppure in siti di rete che si connettono all'area tramite collegamenti WAN senza limitazioni di larghezza di banda.

## Vedere anche

#### Concetti

[Modalità di bypass multimediale in Lync Server 2013](lync-server-2013-media-bypass-modes.md)  
[Bypass multimediale e controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-media-bypass-and-call-admission-control.md)

