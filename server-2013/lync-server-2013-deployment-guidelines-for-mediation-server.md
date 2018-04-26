---
title: 'Lync Server 2013: Linee guida per la distribuzione di Mediation Server'
TOCTitle: Linee guida per la distribuzione di Mediation Server
ms:assetid: 7cc22b87-18d9-45e6-8402-015abd20f2e5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398622(v=OCS.15)
ms:contentKeyID: 49301105
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Linee guida per la distribuzione di Mediation Server in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-12_

In questo argomento vengono fornite alcune linee guida per la pianificazione della distribuzione di Mediation Server. Dopo aver preso visione di queste linee guida, è consigliabile utilizzare Strumento di pianificazione per creare e visualizzare possibili topologie alternative, che possono essere utilizzate come modelli per la topologia personalizzata finale che si sceglierà di distribuire.

## Scelta tra Mediation Servercollocati o autonomi

Per impostazione predefinita, Mediation Server è collocato nel server Standard Edition o in un Front End Server nei siti centrali del pool Front End. Il numero di chiamate PSTN che possono essere gestite e il numero di computer necessari nel pool dipendono dagli aspetti seguenti:

  - Numero di peer gateway controllati dal pool di Mediation Server

  - Traffico nelle ore di punta attraverso tali gateway

  - Percentuale di chiamate che ignorano Mediation Server (Media Bypass)

Durante la pianificazione, è necessario tenere in considerazione i requisiti di elaborazione per le chiamate PSTN e A/V Conferencing non configurati attraverso Media Bypass, nonché la capacità di elaborazione necessaria per gestire le interazioni di segnalazione per il numero di chiamate delle ore di punta che devono essere supportate. Se la capacità della CPU non è sufficiente, è necessario distribuire un pool di Mediation Serverautonomi, e i gateway PSTN, i sistemi IP-PBX e i servizi SBC dovranno essere suddivisi in sottoinsiemi controllati dai Mediation Server collocati in un pool e dai Mediation Server autonomi in uno o più pool autonomi.

Se sono stati distribuiti gateway PSTN, sistemi IP-PBX o servizi SBC che non supportano le funzionalità corrette per interagire con un pool di Mediation Server, tra cui quelle indicate di seguito, sarà necessario associarli a un pool autonomo costituito da un singolo Mediation Server:

  - Esecuzione del bilanciamento del carico DNS a livello di rete tra Mediation Server in un pool (o instradamento, in altro modo, del traffico in maniera uniforme a tutti i server Mediation Server di un pool)

  - Accettazione del traffico proveniente da qualsiasi server Mediation Server in un pool

È possibile utilizzare Microsoft Lync Server 2013, Strumento di pianificazione per valutare se il pool Front End in cui si desidera collocare il server Mediation Server è in grado di gestire il carico. Se l'ambiente non soddisfa questi requisiti, è necessario distribuire un pool di pool di Mediation Server autonomo.

## Considerazioni relative al sito centrale e al sito derivato

I server Mediation Server nel sito centrale possono essere utilizzati per instradare le chiamate per IP-PBX o gateway PSTN nei siti derivati. Se tuttavia si distribuiscono trunk SIP, è necessario distribuire un server Mediation Server presso il sito in cui ogni trunk termina. Per fare in modo che un server Mediation Server nel sito centrale instradi le chiamate per un IP-PBX o un gateway PSTN in un sito derivato, non è necessario utilizzare Media Bypass. Se tuttavia è possibile abilitare Media Bypass, sarà possibile ridurre la latenza del percorso del contenuto multimediale e, di conseguenza, migliorare la qualità multimediale in quanto non sarà più necessario che il percorso del contenuto multimediale segua il percorso di segnalazione. Media Bypass consente inoltre di diminuire il carico di elaborazione nel pool.


> [!NOTE]
> La funzionalità di bypass multimediale non funziona con tutti i gateway PSTN, i sistemi IP-PBX e i servizi SBC. Microsoft ha testato una serie di gateway PSTN e i servizi SBC con partner certificati e ha eseguito alcuni test con i sistemi IP-PBX di Cisco. Il bypass multimediale è supportato solo con le versioni e i prodotti elencati nel sito Web relativo al programma Unified Communications Open Interoperability Program - Lync Server all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=268730">http://go.microsoft.com/fwlink/p/?LinkId=268730</A>.



Se è necessaria la resilienza del sito derivato, è necessario distribuire nel sito derivato un Survivable Branch Appliance o una combinazione di Front End Server, Mediation Server e gateway. Per quando riguarda la resilienza del sito derivato, si presuppone che la presenza e il servizio conferenze non siano resilienti nel sito. Per ulteriori informazioni sulla pianificazione del sito derivato per i servizi vocali, vedere [Pianificazione della resilienza vocale del sito di succursale in Lync Server 2013](lync-server-2013-planning-for-branch-site-voice-resiliency.md).

Per le interazioni con un sistema IP-PBX, se il sistema IP-PBX non supporta correttamente le interazioni multimediali anticipate con interazioni RFC 3960 e dialoghi anticipati multipli, potrebbe venire tagliato il saluto iniziale per le chiamate in arrivo dal sistema IP-PBX per gli endpoint Lync. Questo comportamento può essere più grave se un server Mediation Server in un sito centrale instrada le chiamate per un sistema IP-PBX in cui la route termina in un sito derivato, in quanto è necessario più tempo per il completamento dei segnali. Se si verifica questo problema, la distribuzione di un serve Mediation Server nel sito derivato rappresenta l'unico modo per ridurre il problema del taglio del saluto iniziale .

Infine, se nel sito centrale è presente un sistema PBX TDM o se il sistema IP-PBX richiede un gateway PSTN, è necessario distribuire un gateway nella route di chiamata che connette il Mediation Server e il sistema PBX.


> [!NOTE]
> Per migliorare le prestazioni multimediali del Mediation Server indipendente, è opportuno abilitare RSS (Receive-Side Scaling) nelle schede di rete dei server. RSS consente la gestione parallela dei pacchetti in ingresso da parte di più processori del server. Per informazioni dettagliate, vedere l'articolo relativo ai miglioramenti di RSS (Receive-Side Scaling) in Windows Server all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=268731">http://go.microsoft.com/fwlink/p/?LinkId=268731</A>. Per altri dettagli su come abilitare RSS, vedere la documentazione sull'adattatore di rete.


