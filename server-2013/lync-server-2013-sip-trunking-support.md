---
title: 'Lync Server 2013: Supporto per il trunking SIP'
TOCTitle: Supporto per il trunking SIP
ms:assetid: e3042831-e8d8-4ea2-baa2-1a697401ffa0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399005(v=OCS.15)
ms:contentKeyID: 49302257
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supporto per il trunking SIP in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-03_

Se si prevede di utilizzare VoIP aziendale con il trunking SIP, è necessario distribuire un Mediation Server e verificare che le altre infrastrutture e gli altri componenti soddisfino i requisiti di supporto appropriati per il modello di distribuzione. Per informazioni dettagliate su come determinare se implementare il trunking SIP, vedere [Panoramica del trunking SIP in Lync Server 2013](lync-server-2013-overview-of-sip-trunking.md) nella documentazione relativa alla pianificazione.

È possibile utilizzare il programma Microsoft Unified Communications Open Interoperability Program per l'infrastruttura di telefonia aziendale per individuare gateway PSTN (Public Switched Telephone Network), IP-PBX e trunking SIP qualificati, nonché provider di servizi di telefonia IP qualificati. Per informazioni dettagliate, visitare il sito Web del programma Microsoft Unified Communications Open Interoperability Program all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=203309](http://go.microsoft.com/fwlink/p/?linkid=203309).

## Supporto di Mediation Server

Per implementare il trunking SIP, è necessario instradare la connessione tramite un Mediation Server, che funge da proxy per le sessioni di comunicazione tra client Lync Server 2013 e il provider di servizi. Il Mediation Server decodifica il traffico multimediale proveniente da client e server e lo ricodifica prima di inviarlo al provider di servizi. La ricodifica è necessaria perché i trunk SIP non supportano alcuni codec utilizzati, come la negoziazione di protocolli RTA (Real Time Audio) o ICE (Interactive Connectivity Establishment), per l'attraversamento del firewall.

Ogni Mediation Server può includere due schede di rete, che forniscono un'interfaccia di rete interna e una esterna. L'interfaccia esterna viene definita comunemente interfaccia gateway, perché viene solitamente utilizzata per la connessione a un gateway PSTN o a un IP-PBX. Per implementare un trunk SIP, connettere l'interfaccia esterna a un SBC (Session Border Controller) presso un provider di servizi.

## Trunking SIP centralizzato o distribuito

Il trunking SIP *centralizzato* instrada tutto il traffico VoIP (Voice over Internet Protocol), incluso quello dei siti di succursale, attraverso il data center. Il modello di distribuzione centralizzato è semplice e conveniente ed è in genere l'approccio preferito per implementare trunk SIP con Lync Server 2013.

A seconda dei modelli di utilizzo adottati dall'organizzazione, è possibile decidere di non instradare tutti gli utente attraverso il trunk SIP centralizzato. Per analizzare le specifiche esigenze, rispondere alle domande seguenti:

  - Quanto è grande ogni sito? Quanti utenti?

  - Quali numeri DID (Direct Inward Dialing) in ogni sito ricevono la maggior parte delle telefonate?

Il trunking SIP *distribuito* è un modello di distribuzione in cui si implementa un trunk SIP locale in uno o più siti di succursale. Il traffico VoIP viene quindi instradato dal sito di succursale direttamente al provider di servizi, senza passare per il data center.

Il trunking SIP distribuito è necessario solo nei casi seguenti:

  - Il sito di succursale richiede connettività telefonica che continua a funzionare anche, ad esempio, in caso di interruzione della WAN, Se la succursale richiede ridondanza e failover, il provider di servizi addebita costi più alti e la configurazione richiede più tempo. Questo aspetto deve essere analizzato per ogni sito di succursale. Alcune succursali possono richiedere ridondanza e failover, mentre altre no.

  - Il sito di succursale e il data center si trovano in paesi o aree geografiche diverse. Per motivi legali e di compatibilità, è necessario almeno un trunk SIP per ogni paese o area geografica.

Per decidere se distribuire un trunking SIP centralizzato o distribuito, è necessario effettuare un'analisi del rapporto costi/benefici. In alcuni casi può risultare vantaggioso scegliere la modalità distribuita, anche se non è necessario. In una distribuzione completamente centralizzata, tutto il traffico dei siti di succursale viene instradato su collegamenti WAN. Per non incorrere nei costi della larghezza di banda necessaria per i collegamenti WAN, può essere preferibile utilizzare il trunking SIP distribuito.


> [!NOTE]
> Per informazioni dettagliati sui motivi e su come utilizzare il trunking SIP distribuito, vedere <A href="lync-server-2013-branch-site-sip-trunking.md">Trunking SIP dei siti di succursale in Lync Server 2013</A> nella documentazione relativa alla pianificazione.



## Tipi di connessione supportati per il trunking SIP

Lync Server 2013 supporta i tipi di connessione seguenti per il trunking SIP:

  - MPLS (Multiprotocol Label Switching) è una rete privata che indirizza e trasferisce i dati da un nodo di rete al successivo. La larghezza di banda di una rete MPLS è condivisa con altri sottoscrittori e a ogni pacchetto di dati viene assegnata un'etichetta per distinguere i dati di un sottoscrittore da quelli di un altro. Questo tipo di connessione non richiede VPN. Un potenziale svantaggio è che il traffico IP eccessivo può interferire con l'operazione VoIP a meno che non abbai priorità.

  - Una connessione privata senza altro traffico è in genere il tipo più affidabile e sicuro, ad esempio una connessione in fibra ottica dedicata, o linea T1. Questo tipo di connessione offre la massima capacità per il trasferimento delle chiamate, ma è in genere la più costosa. Non è richiesta una VPN. Le connessioni private sono appropriate per organizzazioni con volumi di chiamate elevate o requisiti rigorosi di sicurezza e disponibilità.

  - La rete Internet pubblica è il tipo di connessione meno costosa, ma anche la meno affidabile e quella con la capacità minore di trasferimento di chiamate. Il provider di servizi di telefonia Internet (ITSP, Internet Telephony Service Provider) può proteggere questo tipo di connessione di trunk SIP se supporta TLS (Transport Layer Security) e SRTP (Secure Real-Time Transport Protocol) per la crittografia di segnali e traffico multimediale. Se non è possibile configurare una connessione di trunk SIP tramite Internet per l'utilizzo di TLS e SRTP, è consigliabile utilizzare un tunnel VPN per una maggiore sicurezza. Contattare l'ITSP per verificare se offre il supporto per TLS con SRTP.

## Scelta di un tipo di connessione

Il tipo di connessione per il trunking SIP più appropriato per la propria azienda dipende dalle diverse esigenze e dal budget a disposizione.

  - Per le organizzazioni di dimensioni medio-grandi, in generale una rete MPLS offre più vantaggi, in quanto è in grado di fornire la larghezza di banda necessaria a costi minori rispetto a una rete privata specializzata.

  - Per le grandi aziende può essere necessaria una connessione in fibra ottica privata o T1.

  - Per le piccole imprese o i siti di succursale con un volume di chiamate ridotto, il trunking SIP tramite Internet può rappresentare la scelta ottimale. Questo tipo di connessione, tuttavia, non è consigliato per siti di dimensioni medio-grandi.

## Supporto di codec

Il proxy del provider di servizi deve supportare i codec seguenti:

  - G.711 a-law (utilizzato principalmente al di fuori dell'America del Nord)

  - G.711 µ-law (utilizzato nell'America del Nord)

