---
title: 'Lync Server 2013: Posizione del gateway PSTN'
TOCTitle: Posizione del gateway PSTN
ms:assetid: 49693a35-fad3-49ee-a71e-c7e4537b79aa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994031(v=OCS.15)
ms:contentKeyID: 52062154
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Posizione del gateway PSTN in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-03-09_

Le chiamate instradate tramite gateway PSTN e dispositivi PBX potrebbero richiedere restrizioni del routing in base alla posizione a seconda della posizione in cui si trovano tali sistemi. Il routing in base alla posizione può essere abilitato al livello di granularità in base al trunk.

Se abilitato su un trunk, il routing in base alla posizione introduce il set di regole seguenti:

  - Quando il routing in base alla posizione è abilitato in base al trunk, le regole definite per quel trunk verranno applicate solo alle chiamate instradate tramite il trunk in questione.

  - Per impedire il bypass della rete PSTN a tariffa quando le chiamate provengono da un sito di rete diverso dal sito di rete in cui si trova il gateway PSTN, il routing in base alla posizione introduce l'associazione di un sito di rete a un determinato trunk. Questo definisce il sito di rete che consente alle chiamate di essere instradate a un trunk specifico.

È possibile abilitare i trunk per il routing in base alla posizione in due modi:

  - Il trunk è definito per un gateway PSTN che instrada le chiamate in uscita alla rete PSTN. Le chiamate in arrivo instradate da un trunk di questo tipo verranno instradate solo a endpoint che si trovano all'interno dello stesso sito di rete del trunk.

  - Il trunk è definito per un peer del Mediation Server che non instrada le chiamate in uscita alla rete PSTN e gestisce gli utenti con telefoni tradizionali in una posizione statica, ad esempio telefoni PBX. Per questa configurazione particolare, tutte le chiamate in arrivo instradate da un trunk di questo tipo verranno considerate come provenienti dallo stesso sito di rete del trunk. Le chiamate dagli utenti PBX avranno la stessa applicazione del routing in base alla posizione degli utenti di Lync che si trovano nello stesso sito di rete del trunk. Se due sistemi PBX situati in siti di rete separati sono connessi tramite Lync Server, il routing in base alla posizione consentirà il routing da un endpoint PBX in un sito di rete a un altro endpoint PBX nell'altro sito di rete. Questo scenario non sarà bloccato dal routing in base alla posizione. Oltre a questo scenario e analogamente a quanto previsto per un utente di Lync nella stessa posizione, gli endpoint connessi a un peer del Mediation Server con questa configurazione potranno effettuare o ricevere chiamate a e da altri peer del Mediation Server che non instradano le chiamate alla rete PSTN, ad esempio un endpoint connesso a un sistema PBX diverso, indipendentemente dal sito di rete a cui il peer del Mediation Server è associato. Tutte le chiamate in arrivo, le chiamate in uscita, i trasferimenti di chiamata e gli inoltri di chiamata che prevedono l'uso di endpoint PBX saranno soggetti al routing in base alla posizione solo per utilizzare i gateway PSTN definiti come locali per tale peer del Mediation Server.

## Vedere anche

#### Ulteriori risorse

[Linee guida per il routing in base alla posizione in Lync Server 2013](lync-server-2013-guidance-for-location-based-routing.md)

