---
title: 'Lync Server 2013: Componente Mediation Server'
TOCTitle: Componente Mediation Server
ms:assetid: 5b19edef-4a54-43c9-aa12-5643b8108355
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398399(v=OCS.15)
ms:contentKeyID: 49300654
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Componente Mediation Server in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

È necessario distribuire Lync Server 2013, Mediation Server se si distribuisce il carico di lavoro di VoIP aziendale. In questa sezione vengono descritte la funzionalità di base, le dipendenze, le topologie di base e le linee guida per la pianificazione.

Il Mediation Server converte la segnalazione, e in alcuni casi le configurazioni, degli elementi multimediali tra l'infrastruttura VoIP aziendale di Lync Server 2013 interna e un gateway PSTN (Public Switched Telephone Network) pubblico o un trunk SIP (Session Initiation Protocol). Sul lato Lync Server 2013, Mediation Server si pone in attesa su un singolo indirizzo di trasporto MTLS (Mutual TLS). Sul lato del gateway, Mediation Server si pone in attesa su tutte le porte di attesa associate ai trunk definiti nel documento della topologia. Tutti i gateway qualificati devono supportare TLS, ma possono abilitare anche TCP. TCP è supportato per i gateway che non supportano TLS.

Se nell'ambiente è disponibile anche un PBX (Public Branch Exchange) esistente, Mediation Server gestisce le chiamate tra gli utenti di VoIP aziendale e il PBX. Nel caso di un IP-PBX, è possibile creare una connessione SIP diretta tra il PBX e Mediation Server. Se il PBX è di tipo TDM (Time Division Multiplex), è necessario distribuire anche un gateway PSTN tra Mediation Server e il PBX.

Il Mediation Server è collocato con il Front End Server per impostazione predefinita. È inoltre possibile distribuire Mediation Server in un pool autonomo per motivi di prestazioni o se si distribuisce il trunking SIP. In questo caso, la distribuzione del pool autonomo è caldamente consigliata.

Se si distribuiscono connessioni SIP diretto in un gateway PSTN qualificato che supporta il bypass multimediale e il bilanciamento del carico DNS, non è necessario un pool Mediation Server autonomo, in quanto i gateway qualificati supportano il bilanciamento del carico DNS in un pool pool di Mediation Server e possono ricevere traffico da qualsiasi Mediation Server in un pool.

È inoltre consigliabile posizionare Mediation Server su un pool Front End se sono stati distribuiti sistemi IP-PBX o ci si connette al controller SBC (Session Border Controller) di un provider di servizi di telefonia Internet (ITSP), se si verifica una delle condizioni seguenti:

  - Il sistema IP-PBX o SBC è configurato per la ricezione di traffico da qualsiasi server Mediation Server nel pool e può eseguire il routing del traffico in modo uniforme a tutti i server Mediation Server nel pool.

  - Il sistema IP-PBX non supporta il bypass multimediale, ma il pool Front End che ospita Mediation Server può gestire la transcodifica vocale per le chiamate a cui non si applica il bypass multimediale.

È possibile utilizzare Microsoft Lync Server 2013, Strumento di pianificazione per valutare se pool Front End in cui si desidera collocare Mediation Server è in grado di gestire il carico. Se l'ambiente non soddisfa questi requisiti, è necessario distribuire un pool di pool di Mediation Server autonomo.

Le principali funzioni del Mediation Server sono le seguenti:

  - Crittografia e decrittografia di SRTP sul lato Lync Server

  - Conversione di SIP su TCP (per i gateway che non supportano TLS) in SIP su Mutual TLS

  - Conversione di flussi multimediali tra Lync Server e il peer gateway del Mediation Server

  - Connessione di client esterni alla rete a componenti ICE interni per consentire l'attraversamento multimediale di NAT e firewall

  - Intermediazione per i flussi di chiamate non supportate da un gateway, ad esempio quelle effettuate da dipendenti remoti in un client VoIP aziendale

  - Utilizzo del provider di servizi trunking SIP, nelle distribuzioni che includono il trunking SIP, per fornire il supporto PSTN eliminando la necessità di un gateway PSTN

Nella figura seguente sono illustrati i protocolli di segnalazione e multimediali utilizzati dal Mediation Server per le comunicazioni con un gateway PSTN di base e l'infrastruttura VoIP aziendale.

**Protocolli di segnalazione e multimediali utilizzati dal Mediation Server**

![Diagramma dei protocolli del Mediation Server](images/Gg398399.c3d39ba0-e323-4a58-8f07-4e80d3278af2(OCS.15).jpg "Diagramma dei protocolli del Mediation Server")


> [!NOTE]
> Se si utilizza TCP o RTP/RTCP, anziché SRTP o SRTCP, nella rete tra il gateway PSTN e il Mediation Server, è consigliabile prendere misure adeguate per garantire sicurezza e privacy della rete.



## Contenuto della sezione

  - [Trunk con relazioni molti-a-molti in Lync Server 2013](lync-server-2013-m-n-trunk.md)

  - [Controllo di ammissione di chiamata e Mediation Server in Lync Server 2013](lync-server-2013-call-admission-control-and-mediation-server.md)

  - [Servizi di emergenza avanzati e Mediation Server in Lync Server 2013](lync-server-2013-enhanced-9-1-1-e9-1-1-and-mediation-server.md)

  - [Bypass multimediale e Mediation Server in Lync Server 2013](lync-server-2013-media-bypass-and-mediation-server.md)

  - [Componenti e topologie per Mediation Server in Lync Server 2013](lync-server-2013-components-and-topologies-for-mediation-server.md)

  - [Linee guida per la distribuzione di Mediation Server in Lync Server 2013](lync-server-2013-deployment-guidelines-for-mediation-server.md)

