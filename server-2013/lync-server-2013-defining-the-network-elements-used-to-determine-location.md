---
title: 'Lync Server 2013: Definizione degli elementi di rete utilizzati per determinare la posizione'
TOCTitle: Definizione degli elementi di rete utilizzati per determinare la posizione
ms:assetid: 7538779d-055d-44ed-8dd7-11c45fc1b9f5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398567(v=OCS.15)
ms:contentKeyID: 49301001
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definizione degli elementi di rete utilizzati per determinare la posizione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-29_

Se si configura l'infrastruttura Lync Server per supportare il rilevamento automatico della posizione dei client, è innanzitutto necessario stabilire quali elementi di rete utilizzare per eseguire il mapping dei chiamanti alle posizioni. In Lync Server 2013, è possibile associare alle posizioni gli elementi di rete di livello 2 e di livello 3 seguenti:

  - Indirizzi BSSID (Basic Service Set Identification) di punti di accesso wireless (livello 2)

  - Porta di commutazione LLDP (livello 2)

  - ID chassis di commutazione LLDP (livello 2)

  - Subnet IP (livello 3)

  - Indirizzi MAC dei client (livello 2)

Gli elementi di rete sono elencati in ordine di precedenza. Se un client può essere individuato utilizzando più di un elemento di rete, in Lync Server viene applicato l'ordine di precedenza per determinare il meccanismo da utilizzare.

Nelle sezioni seguenti sono disponibili ulteriori dettagli sull'utilizzo di ciascun elemento di rete.

> [!IMPORTANT]  
> Quando si utilizzano elementi di rete per eseguire il mapping dei chiamanti alle località, è di primaria importanza che il database di servizio Informazioni percorso sia aggiornato. Ad esempio, se si aggiunge o modifica un elemento di rete, ad esempio se si aggiunge un punto di accesso wireless, è necessario eliminare la voce esistente e aggiungere la nuova nel database delle località.

## Punto di accesso wireless

Quando un client si connette alla rete in modalità wireless, la richiesta della posizione utilizza l'indirizzo BSSID del punto di accesso wireless per determinarne la posizione. Se il client effettua il roaming, il punto di accesso wireless indicato potrebbe non essere quello più vicino ed è anche possibile che venga rilevato un punto di accesso wireless che si trova in un piano diverso dell'edificio. Per indicare che la posizione è approssimativa, è possibile anteporre al valore di posizione un descrittore Near o Close to.

Questo metodo presuppone che l'indirizzo BSSID di ogni punto di accesso wireless sia statico. Se il fornitore del punto di accesso wireless, tuttavia, utilizza BSSID assegnati dinamicamente, l'indirizzo BSSID ottenuto da un punto di accesso wireless può cambiare (ad esempio in seguito a una modifica di configurazione apportata al punto di accesso wireless) e i client wireless possono trovarsi in una situazione in cui non ricevono una posizione. Per evitare questa possibilità, è necessario immettere nel database servizio Informazioni percorso gli ERL per tutti gli indirizzi BSSID possibili utilizzati da ogni punto di accesso wireless.

## Porte e switch LLDP

Switch Ethernet gestiti che supportano LLDP-MED (Link Layer Discovery Protocol-Media Endpoint Discover) possono comunicare informazioni su porta e identità a client compatibili con LLDP-MED, che possono quindi essere soggetti a query sul database delle località per fornire la posizione del dispositivo. È possibile associare ERL unicamente a ID chassis di commutazione oppure è possibile eseguirne il mapping a livello di porta.


> [!NOTE]
> Lync Server 2013 supporta l'utilizzo di LLDP-MED per determinare solo le posizioni di dispositivi Lync Phone Edition e Lync 2013 eseguiti su Windows 8. Se è necessario utilizzare dati di livello 2 a livello di switch per determinare la posizione di client di Lync basati su PC cablati, è necessario utilizzare il metodo degli indirizzi MAC dei client.



## Subnet

Le subnet IP di livello 3 offrono un meccanismo supportato da tutti i client di Lync Server che può essere utilizzato per rilevare automaticamente la posizione dei client. L'utilizzo di subnet IP rappresenta il metodo di individuazione più facile per configurare e gestire client cablati. Prima di scegliere di utilizzare le subnet, tuttavia, è consigliabile rispondere alle domande seguenti per determinare se la specificità di posizione della subnet è sufficiente per individuare accuratamente un client:

  - Una o più subnet del client occupano più piani?

  - Una o più subnet occupano più edifici?

  - Quanto spazio di un piano è occupato da ogni subnet del client?

Se la subnet occupa un'area troppo ampia, può essere necessario utilizzare un altro meccanismo per individuare i client. Se si tratta di una scelta pratica, tuttavia, è consigliabile che gli utenti riorganizzino le proprie subnet IP in modo da soddisfare i requisiti di specificità di posizione ERL anziché affrontare i costi e la complessità di soluzioni basate su SNMP di terze parti.

## Indirizzo MAC del client

Per utilizzare l'indirizzo MAC di un computer client per individuare un chiamante, sono necessari switch Ethernet gestiti ed è necessario distribuire una soluzione SNMP di terze parti in grado di rilevare gli indirizzi MAC dei client Lync connessi a (o tramite) tali switch. La soluzione SNMP esegue continuamente il polling degli switch gestiti per ottenere i mapping correnti degli indirizzi MAC degli endpoint connessi a ogni porta e ottiene gli ID porta corrispondenti. Durante una richiesta di un client Lync al servizio Informazioni percorso, il servizio Informazioni percorso esegue una query sull'applicazione di terze parti utilizzando l'indirizzo MAC del client e restituisce tutti gli indirizzi IP e gli ID porta degli switch corrispondenti. Il servizio Informazioni percorso utilizza quindi queste informazioni per eseguire query sulla mappa delle posizioni di livello 2 pubblicata per trovare un record corrispondente e restituisce la posizione al client. Se si utilizza questa opzione, assicurarsi che gli identificatori di porta degli switch siano coerenti tra l'applicazione SNMP e i record del database delle località pubblicati.


> [!NOTE]
> Alcune soluzioni SNMP di terze parti possono supportare switch di accesso non gestiti. Se lo switch tramite cui viene servito il client Lync non è gestito, ma dispone di un uplink a uno switch di distribuzione gestito, lo switch gestito può segnalare all'applicazione SNMP gli indirizzi MAC dei client connessi allo switch di accesso. Queste informazioni consentono al servizio Informazioni percorso di identificare la posizione dell'utente. Poiché, tuttavia, è possibile assegnare un solo ERL a tutte le porte nello switch non gestito, la specificità di posizione è disponibile solo a livello di chassis dello switch di accesso e non a livello di porta..


