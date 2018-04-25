---
title: 'Lync Server 2013: Considerazioni tecniche per il routing in base alla posizione'
TOCTitle: Considerazioni tecniche per il routing in base alla posizione
ms:assetid: 2e2a9199-7c6f-48d3-9adb-3873fc4f8c4e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994027(v=OCS.15)
ms:contentKeyID: 52062125
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Considerazioni tecniche per il routing in base alla posizione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-03-09_

Durante la pianificazione del routing in base alla posizione, è consigliabile tenere conto dell'impatto sugli scenari seguenti.

## Ripristino di emergenza

Durante un failover dal pool principale a un pool di backup, nonché durante il ripristino della normale operatività nel pool principale, il routing in base alla posizione rimane sempre applicato durante una procedura di ripristino di emergenza.

## Survivable Branch Appliance

La configurazione del routing in base alla posizione influisce sulla pianificazione relativa alla posizione di implementazione dei gateway associati al Survivable Branch Appliance. È necessario che il gateway associato all'SBA si trovi nello stesso sito di rete del Survivable Branch Appliance; in caso contrario, agli utenti ospitati nell' Survivable Branch Appliance non sarà consentito effettuare chiamate in uscita se è configurato il routing in base alla posizione. Quando la connessione WAN tra l' Survivable Branch Appliance e il sito centrale non è attiva, le restrizioni del routing in base alla posizione rimangono applicate.

## Vedere anche

#### Ulteriori risorse

[Pianificazione del routing in base alla posizione in Lync Server 2013](lync-server-2013-planning-for-location-based-routing.md)

