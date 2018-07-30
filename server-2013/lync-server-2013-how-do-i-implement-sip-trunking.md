---
title: 'Lync Server 2013: Come implementare il trunking SIP'
TOCTitle: Come implementare il trunking SIP
ms:assetid: 273a22b1-8a4c-4187-acf8-c57d5c6598ce
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425743(v=OCS.15)
ms:contentKeyID: 49299981
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Come implementare il trunking SIP in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-03-18_

Per implementare il trunking SIP, è necessario instradare la connessione attraverso un Mediation Server, che agisce da proxy per le sessioni di comunicazione tra i client di Lync Server 2013 e il provider del servizio e transcodifica i dati multimediali, quando necessario.

Ogni Mediation Server dispone di un'interfaccia di rete interna e di un'interfaccia di rete esterna. L'interfaccia interna si connette ai Front End Server. L'interfaccia esterna viene generalmente denominata interfaccia gateway perché è sempre stata usata per connettere il Mediation Server a un gateway PSTN (Public Switched Telephone Network) o un sistema IP-PBX. Per implementare un trunk SIP, si connette l'interfaccia esterna del Mediation Server al componente perimetrale esterno dell'ITSP.


> [!NOTE]
> Il componente perimetrale esterno dell'ITSP potrebbe essere un servizio Session Border Controller (SBC), un router o un gateway.



Per informazioni dettagliate sui Mediation Server, vedere [Componente Mediation Server in Lync Server 2013](lync-server-2013-mediation-server-component.md).

## Trunking SIP centralizzato o distribuito

Il trunking SIP *centralizzato* instrada tutto il traffico VOIP (Voice over Internet Protocol), incluso il traffico del sito di succursale, tramite il sito centrale. Il modello di distribuzione centralizzato è semplice, economico e generalmente consigliato per l'implementazione dei trunk SIP con Lync Server 2013.

Il trunking SIP *distribuito* è un modello di distribuzione in base al quale si implementa un trunk SIP locale in uno o più siti di succursale. Il traffico VoIP viene quindi instradato dal sito di succursale direttamente a un provider di servizi senza passare attraverso il sito centrale.

Il trunking SIP distribuito è necessario solo nei casi seguenti:

  - Nel sito di succursale è necessaria una connettività telefonica di tipo Survivable Branch Appliance, ad esempio in caso di problemi con la WAN. Questo requisito deve essere analizzato per ogni sito di succursale. È infatti possibile che solo alcune delle succursali richiedano funzionalità di ridondanza e failover. .

  - Tra due siti centrali è richiesta la resilienza. È necessario verificare che un trunk SIP termini in corrispondenza di ogni sito centrale. Nel caso ad esempio di due siti centrali a Dublino e Tukwila che utilizzano entrambi solo il trunk SIP di un sito, se si verifica un problema con il trunk, gli utenti dell'altro sito non potranno effettuare chiamate PSTN.

  - Il sito di succursale e il sito centrale si trovano in paesi diversi. Per motivi legali e di compatibilità, è necessario almeno un trunk SIP per paese. Nell'Unione Europea ad esempio le comunicazioni non possono uscire da un paese senza terminare localmente in un punto centralizzato.

A seconda della posizione geografica dei siti e del traffico previsto nell'ambito dell'organizzazione, è possibile non instradare tutti gli utenti attraverso il trunk SIP centrale oppure scegliere di instradare alcuni utenti attraverso un trunk SIP presso il sito di succursale. Per valutare le proprie esigenze, analizzare gli aspetti seguenti:

  - Grandezza di ogni sito, ovvero numero di utenti abilitati per VoIP aziendale

  - Numeri DID (Direct Inward Dialing) presso ogni sito che ricevono più telefonate

Per scegliere se distribuire il trunking SIP centralizzato o distribuito, è necessaria un'analisi costi-benefici. In alcuni casi può essere vantaggioso scegliere il modello di trunking SIP distribuito, anche quando non è obbligatorio. In una distribuzione completamente centralizzata tutto il traffico di sito di succursale viene instradato attraverso collegamenti WAN. Anziché pagare per la larghezza di banda necessaria per i collegamenti WAN, è possibile utilizzare il trunking SIP distribuito. È ad esempio possibile distribuire un server Standard Edition in un sito di succursale con federazione con il sito centrale oppure distribuire un Survivable Branch Appliance o un Survivable Branch Server con un piccolo gateway.


> [!NOTE]
> Per informazioni dettagliate sul trunking SIP distribuito, vedere <A href="lync-server-2013-branch-site-sip-trunking.md">Trunking SIP dei siti di succursale in Lync Server 2013</A>.



## Tipi di connessione supportati per il trunking SIP

Lync Server supporta i tipi di connessione seguenti per il trunking SIP:

  - MPLS (Multiprotocol Label Switching). Si tratta di una rete privata che indirizza e trasporta i dati da un nodo di rete al successivo. La larghezza di banda in una rete MPLS è condivisa con altri sottoscrittori e a ogni pacchetto dati è assegnata un'etichetta per distinguere i dati di un sottoscrittore da quelli di un altro. Questo tipo di connessione non richiede una rete privata virtuale (VPN). Un potenziale svantaggio è rappresentato dal rischio che un eccessivo traffico IP possa interferire con il funzionamento di VoIP, a meno che non venga assegnata priorità al traffico VoIP.

  - Una connessione privata senza altro traffico, ad esempio una connessione su fibra ottica dedicata o linea T1. Questo tipo di connessione è in genere il più affidabile e sicuro. Garantisce un'elevata capacità di trasporto delle chiamate, ma è anche il più costoso. Non è richiesta una VPN. Le connessioni private sono appropriate per le organizzazioni con un elevato volume di chiamate o con requisiti di disponibilità e sicurezza rigorosi.

  - Internet. Questo è il tipo di connessione meno costoso, ma anche il meno affidabile. La connessione Internet è l'unico tipo di connessione per trunking SIP di Lync Server che richiede una VPN.

## Scelta di un tipo di connessione

Il tipo di connessione per il trunking SIP più appropriato per la propria azienda dipende dalle diverse esigenze e dal budget a disposizione.

  - Per un'azienda di medie o grandi dimensioni, una rete MPLS in genere è la soluzione più appropriata, poiché offre la larghezza di banda necessaria a una tariffa più conveniente rispetto a una rete privata specializzata.

  - Per le aziende di dimensioni maggiori può essere necessaria una connessione su fibra ottica privata, T1, T3 o superiore (E1, E3 o superiore nell'Unione Europea).

  - Per una piccola azienda o un sito di succursale con un volume di chiamate ridotto, il trunking SIP attraverso Internet può rivelarsi la scelta ottimale. Questo tipo di connessione non è consigliato per siti di medie o grandi dimensioni.

## Requisiti di larghezza di banda

La larghezza di banda richiesta da un'implementazione dipende dalla capacità di chiamata, ovvero dal numero di chiamate simultanee che devono essere supportate. È necessario tenere conto della disponibilità della larghezza di banda in modo da poter usufruire pienamente della capacità di picco per cui si paga. Usare la formula seguente per calcolare il requisito di larghezza di banda di picco di un trunk SIP:

Larghezza di banda di picco di trunk SIP = Numero massimo di chiamate simultanee x (64 kbps + dimensioni delle intestazioni)


> [!NOTE]
> Le dimensioni massime delle intestazioni corrispondono a 20 byte.



## Supporto di codec

Lync Server 2013 supporta solo i codec seguenti:

  - G.711 a-law (utilizzato principalmente al di fuori dell'America del Nord)

  - G.711 µ-law (utilizzato nell'America del Nord)

## Provider di servizi di telefonia Internet

La modalità di implementazione del lato provider di servizi di una connessione trunk SIP varia da un ITSP all'altro. Per informazioni sulla distribuzione, contattare il provider di servizi. Per un elenco di provider di servizi di trunking SIP certificati, vedere il sito Web del [Microsoft Unified Communications Open Interoperability Program](http://go.microsoft.com/fwlink/?linkid=287029).

Per informazioni dettagliate sui provider di trunking SIP certificati Microsoft, contattare il rappresentante Microsoft.

> [!IMPORTANT]  
> È necessario usare un provider di servizi certificato Microsoft per garantire che il provider ITSP supporti tutte le funzionalità che attraversano il trunk SIP, ad esempio la configurazione e la gestione delle sessioni e il supporto di tutti i servizi VoIP estesi. Il supporto tecnico Microsoft non si estende alle configurazioni che usano provider non certificati. Se attualmente si usa un provider di servizi Internet non certificato per il trunking SIP, è possibile scegliere di continuare a usarlo come ISP, passando a un provider certificato Microsoft per il trunking SIP.
