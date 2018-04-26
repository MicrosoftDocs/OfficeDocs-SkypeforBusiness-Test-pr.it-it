---
title: 'Lync Server 2013: Funzionalità non supportate dal routing in base alla posizione'
TOCTitle: Funzionalità non supportate dal routing in base alla posizione
ms:assetid: c3d54953-a7d6-4465-a6c3-ae411b2d8ea9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994071(v=OCS.15)
ms:contentKeyID: 52062309
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Funzionalità non supportate dal routing in base alla posizione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-03-12_

Il routing in base alla posizione non si applica ai seguenti tipi di interazioni. Non viene applicato quando gli endpoint Lync interagiscono con endpoint PSTN utilizzando queste funzionalità.

  - Conferenza telefonica con accesso esterno PSTN alle conferenze

  - Chiamate PSTN in arrivo e in uscita tramite Response Group

  - Parcheggio o recupero di chiamate PSTN tramite Parcheggio di chiamata

  - Chiamate PSTN in arrivo a Servizio Annuncio

  - Chiamate PSTN in arrivo recuperate tramite Risposta alle chiamate di gruppo

Per applicare le regole di routing in base alla posizione ai tipi di interazione nel seguente elenco, è necessario abilitare il routing in base alla posizione per le conferenze:

  - Conferenza telefonica PSTN con chiamata in uscita da conferenze

  - Escalation da conversazioni audio peer-to-peer a conferenze che coinvolgono endpoint PSTN

  - Trasferimenti con consultazione che coinvolgono endpoint PSTN

Per abilitare il routing in base alla posizione per le conferenze, vedere [Routing in base alla posizione per le conferenze](lync-server-2013-location-based-routing-for-conferencing.md).

## Vedere anche

#### Ulteriori risorse

[Pianificazione del routing in base alla posizione in Lync Server 2013](lync-server-2013-planning-for-location-based-routing.md)

