---
title: 'Lync Server 2013: Panoramica del routing in base alla posizione'
TOCTitle: Panoramica del routing in base alla posizione
ms:assetid: 4aa494bd-0d66-4335-b9e8-f758d44a7202
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994032(v=OCS.15)
ms:contentKeyID: 52062144
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica del routing in base alla posizione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

Il routing in base alla posizione introduce un nuovo set di regole che modificano il routing delle chiamate PST nazionali e internazionali, per evitare il bypass delle chiamate a tariffa. Il routing in base alla posizione offre la flessibilità di definire come ambito delle regole solo aree geografiche, gateway o set di utenti specifici.

Gli scenari seguenti illustrano i tipi principali di restrizioni applicabili con il routing in base alla posizione:

  - Chiamate in uscita – Il routing in base alla posizione può imporre l'uscita delle chiamate da un gateway PSTN dislocato nella stessa area geografica del chiamante per evitare il bypass delle chiamate a tariffa. In questo modo le chiamate non possono uscire da un gateway PSTN in un'area geografica diversa da quella del chiamante.

  - Chiamate in ingresso – Il routing in base alla posizione può impedire alle chiamate PSTN in arrivo di squillare in endpoint Lync se il gateway PSTN che gestisce il routing della chiamata in arrivo non si trova nella stessa area geografica dell'utente di Lync chiamato.

  - Aree geografiche sconosciute – Il routing in base alla posizione impone restrizioni per le chiamate PSTN in arrivo e in uscita da e verso utenti in posizioni indeterminate, ad esempio utenti remoti che si connettono da Internet o si trovano in aree geografiche sconosciute,

  - Aree geografiche internazionali – Il routing in base alla posizione impone il routing delle chiamate in uscita tramite gateway PSTN internazionali, se non è possibile trovare un gateway locale rispetto alla posizione dell'utente.

## Vedere anche

#### Ulteriori risorse

[Pianificazione del routing in base alla posizione in Lync Server 2013](lync-server-2013-planning-for-location-based-routing.md)

