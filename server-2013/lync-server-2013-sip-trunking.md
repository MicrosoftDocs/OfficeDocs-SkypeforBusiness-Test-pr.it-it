---
title: 'Lync Server 2013: Trunking SIP'
TOCTitle: Trunking SIP
ms:assetid: 7c586401-d0e5-4017-b3e1-fe5e7f8fc6db
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398619(v=OCS.15)
ms:contentKeyID: 49301089
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Trunking SIP in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-08-13_

Il protocollo SIP (Session Initiation Protocol) viene utilizzato per avviare e gestire sessioni di comunicazioni Voice over IP (VoIP) per servizi telefonici di base e per altri servizi di comunicazione in tempo reale, ad esempio messaggistica istantanea, conferenze, informazioni sulla presenza e sessioni multimediali. In questa sezione vengono fornite informazioni sulla pianificazione per l'implementazione di *trunk SIP* , un tipo di connessione SIP che si estende oltre i confini della rete locale.

## Cos'è il trunking SIP?

Un trunk SIP è una connessione IP che consente di stabilire un collegamento di comunicazione SIP tra l'organizzazione e un provider di servizi di telefonia Internet (ITSP) oltre il firewall. In genere, un trunk SIP viene utilizzato per connettere il sito centrale dell'organizzazione a un ITSP. In alcuni casi, è anche possibile scegliere di utilizzare il trunking SIP per connettere un sito derivato a un ITSP.

## Confronto tra trunk SIP e connessioni SIP dirette

Il termine *trunk* deriva dalla tecnologia a commutazione di circuito e fa riferimento a una linea fisica dedicata che connette le apparecchiature di commutazione telefonica. Analogamente ai trunk TDM (Time Division Multiplexing) precedenti, i trunk SIP rappresentano le connessioni tra due reti SIP distinte, Lync Server 2013 Enterprise e l'ITSP. A differenza dei trunk a commutazione di circuito, i trunk SIP sono connessioni virtuali che possono essere stabilite tramite uno qualsiasi dei tipi di connessione trunking SIP supportati. Per ulteriori informazioni sui tipi di connessione supportati, vedere [Come implementare il trunking SIP in Lync Server 2013](lync-server-2013-how-do-i-implement-sip-trunking.md)

Le connessioni SIP dirette sono invece connessioni SIP che non oltrepassano il confine di rete locale, ovvero si connettono a un gateway PSTN o un PBX nella rete interna. Per ulteriori informazioni sull'utilizzo di connessioni SIP dirette con Lync Server 2013, vedere [Connessioni SIP dirette in Lync Server 2013](lync-server-2013-direct-sip-connections.md).

## Contenuto della sezione

  - [Panoramica del trunking SIP in Lync Server 2013](lync-server-2013-overview-of-sip-trunking.md)

  - [Come implementare il trunking SIP in Lync Server 2013](lync-server-2013-how-do-i-implement-sip-trunking.md)

  - [Componenti e topologie per il trunking SIP in Lync Server 2013](lync-server-2013-components-and-topologies-for-sip-trunking.md)

  - [Trunking SIP dei siti di succursale in Lync Server 2013](lync-server-2013-branch-site-sip-trunking.md)

  - [Elenco di controllo di distribuzione per i trunk SIP per Lync Server 2013](lync-server-2013-sip-trunk-deployment-checklist.md)

