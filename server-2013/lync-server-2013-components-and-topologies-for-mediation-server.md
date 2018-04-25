---
title: 'Lync Server 2013: Componenti e topologie per Mediation Server'
TOCTitle: Componenti e topologie per Mediation Server
ms:assetid: 71397168-36c3-4d21-b8ef-db6a751634ee
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398537(v=OCS.15)
ms:contentKeyID: 49300937
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Componenti e topologie per Mediation Server in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

In questo argomento vengono descritti i componenti da cui dipende Mediation Server e le topologie in cui è possibile distribuire Mediation Server

## Dipendenze

Mediation Server ha le dipendenze seguenti:

  - **Registrazione avanzata.** Obbligatorio. Il servizio Registrazione avanzata è l'hop successivo per i segnali nelle interazioni di Mediation Server con la rete di Lync Server 2013. Si noti che Mediation Server può essere distribuito nella stessa posizione di un Front End Server insieme a Registrazione avanzata, oltre a poter essere installato in un pool autonomo costituito solo da Mediation Server. Il servizio Registrazione avanzata si trova nella stessa posizione di un server Mediation Server e del gateway PSTN in un sistema Survivable Branch Appliance.

  - **Monitoring Server.** Facoltativo ma consigliato. Monitoring Server consente a Mediation Server di registrare metriche della qualità associate alle sessioni multimediali.

  - **Edge server (Server perimetrale).** Obbligatorio per il supporto degli utenti esterni. server perimetrale consente a Mediation Server di interagire con gli utenti che si trovano dietro un sistema NAT o un firewall.

## Topologie

In Lync Server 2013, Mediation Server si trova per impostazione predefinita nella stessa posizione di un'istanza del servizio Registrazione avanzata di un server Standard Edition, pool Front End o Survivable Branch Appliance. Tutti i Mediation Server di un pool Front End devono essere configurati in modo identico.

Quando le prestazioni rappresentano un problema, può essere preferibile distribuire uno o più server Mediation Server in un pool autonomo dedicato. In alternativa, se si intende distribuire il trunking SIP, è consigliabile distribuire un pool di pool di Mediation Server autonomo.

Se si distribuiscono connessioni Direct SIP in un gateway PSTN qualificato che supporta il bypass multimediale e il bilanciamento del carico DNS, non è necessario un pool di pool di Mediation Server autonomo, in quanto i gateway qualificati sono capaci di bilanciamento del carico DNS in un pool di Mediation Server e possono ricevere traffico da qualsiasi server Mediation Server in un pool.

È inoltre consigliabile posizionare Mediation Server su un pool Front End se sono stati distribuiti sistemi IP-PBX o ci si connette al controller SBC (Session Border Controller) di un provider di servizi di telefonia Internet (ITSP), se si verifica una delle condizioni seguenti:

  - Il sistema IP-PBX o SBC è configurato per la ricezione di traffico da qualsiasi server Mediation Server nel pool e può eseguire il routing del traffico in modo uniforme a tutti i server Mediation Server nel pool.

  - Il sistema IP-PBX non supporta il bypass multimediale, ma il pool Front End che ospita Mediation Server può gestire la transcodifica vocale per le chiamate a cui non si applica il bypass multimediale.

È possibile utilizzare Microsoft Lync Server 2013, Strumento di pianificazione per valutare se pool Front End in cui si desidera collocare Mediation Server è in grado di gestire il carico. Se l'ambiente non soddisfa questi requisiti, è necessario distribuire un pool di pool di Mediation Server autonomo.

Per informazioni dettagliate su quale topologia distribuire, vedere [Linee guida per la distribuzione di Mediation Server in Lync Server 2013](lync-server-2013-deployment-guidelines-for-mediation-server.md).

Nella figura seguente viene illustrata una semplice topologia costituita da due siti connessi tramite un collegamento WAN. Mediation Server si trova nella stessa posizione del servizio Registrazione avanzata in un pool Front End nel sito 1. Mediation Server nel sito 1 controlla sia il gateway PSTN nel sito 1 sia il gateway nel sito 2. In questa topologia il bypass multimediale è abilitato a livello globale per utilizzare informazioni su siti e aree ed è abilitato anche per i trunk a ogni gateway PSTN (GW1 e GW2).

**Esempio di siti connessi tramite un collegamento WAN a un server Mediation Server nel sito 1 e a un gateway PSTN nel sito 2**

![Topologia vocale con Mediation Server e gateway WAN](images/Gg398537.67872e61-1444-447b-918c-abe89abc3004(OCS.15).jpg "Topologia vocale con Mediation Server e gateway WAN")

Nella figura seguente viene illustrata una semplice topologia in cui Mediation Server si trova nella stessa posizione del servizio Registrazione avanzata nel pool Front End nel sito 1 e ha una connessione Direct SIP al sistema IP-PBX nel sito 1. In questa figura Mediation Server controlla anche un gateway PSTN nel sito 2. Si supponga che gli utenti di Lync siano presenti in entrambi i siti e che il sistema IP-PBX disponga di un processore multimediale associato che deve essere attraversato da tutti i contenuti multimediali provenienti da endpoint di Lync prima dell'invio agli endpoint multimediali controllati dal sistema IP-PBX. In questa topologia il bypass multimediale è abilitato a livello globale per utilizzare informazioni su siti e aree ed è abilitato anche per i trunk al sistema PBX e al gateway PSTN.

**Esempio di siti connessi tramite un collegamento WAN a un server Mediation Server nel sito 1 e a un sistema PBX nel sito 2**

![Topologia vocale con Mediation Server e PBX WAN](images/Gg398537.df6c8a5b-8431-4187-907d-ff5ca26eeeec(OCS.15).jpg "Topologia vocale con Mediation Server e PBX WAN")

Per informazioni dettagliate sulla pianificazione di topologie PBX, vedere [Linee guida per la distribuzione di Mediation Server in Lync Server 2013](lync-server-2013-deployment-guidelines-for-mediation-server.md) e [Opzioni di distribuzione SIP diretta in Lync Server 2013](lync-server-2013-direct-sip-deployment-options.md).

Nell'ultima figura di questo argomento viene illustrata una topologia in cui Mediation Server è connesso al controller SBC di un provider di servizi di telefonia Internet (ITSP). Per informazioni sulle topologie di trunking SIP, vedere [Trunking SIP in Lync Server 2013](lync-server-2013-sip-trunking.md).

