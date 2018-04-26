---
title: 'Lync Server 2013: Distribuzione di siti di succursale'
TOCTitle: Distribuzione di siti di succursale
ms:assetid: 1475dee0-66ae-4ee5-b6f1-7409b4bbff45
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398217(v=OCS.15)
ms:contentKeyID: 49299768
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuzione di siti di succursale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

Gli utenti dei siti di succursale ottengono la maggior parte delle funzionalità di Lync Server 2013 dal server disponibile presso il sito centrale a cui il sito di succursale è associato. Ogni sito di succursale è associato esattamente a un sito centrale. Per garantire le chiamate alla e dalla rete PSTN (Public Switched Telephone Network), un sito di succursale può includere uno o più elementi seguenti:

  - Un gateway PSTN ed eventualmente un Mediation Server

  - Un trunk SIP

  - Un'infrastruttura vocale esistente con un centralino (PBX)

  - Un Survivable Branch Appliance

  - Un Survivable Branch Server

In caso di problemi della rete WAN o del sito centrale, i siti di succursale con un Survivable Branch Appliance o un Survivable Branch Server sono più resilienti rispetto ai siti di succursale sprovvisti di una di queste soluzioni. Ad esempio, in un sito in cui è distribuito un Survivable Branch Appliance o un Survivable Branch Server gli utenti possono effettuare e ricevere chiamate PSTN anche se la rete che connette il sito di succursale al sito centrale non è attiva. Un altro modo per avere la resilienza dei siti di succursale è quello di utilizzare un gateway PSTN o un trunk SIP con una distribuzione di Lync Server completa presso il sito di succursale.

Per informazioni sul tipo di distribuzione dei siti di succursale appropriato per la propria organizzazione e sui prerequisiti e altre considerazioni per la pianificazione, vedere [Pianificazione per la connettività PSTN in Lync Server 2013](lync-server-2013-planning-for-pstn-connectivity.md) e [Pianificazione della resilienza vocale del sito di succursale in Lync Server 2013](lync-server-2013-planning-for-branch-site-voice-resiliency.md) nella documentazione relativa alla pianificazione.

## Argomenti della sezione

  - [Implementazione della connettività PSTN in un sito di succursale in Lync Server 2013](lync-server-2013-providing-pstn-connectivity-at-a-branch-site.md)

  - [Distribuzione di Survivable Branch Appliance o Survivable Branch Server con Lync Server 2013](lync-server-2013-deploying-a-survivable-branch-appliance-or-server.md)

