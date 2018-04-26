---
title: 'Lync Server 2013: monitoraggio delle prestazioni di rete'
TOCTitle: Monitoraggio delle prestazioni di rete
ms:assetid: bc3a01da-91eb-4c0c-9598-35e5e46b00f6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn720923(v=OCS.15)
ms:contentKeyID: 62240087
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Monitoraggio delle prestazioni di rete in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-08-17_

Lync Server 2013 è una tecnologia di comunicazione in tempo reale che si basa essenzialmente sulla rete per abilitare le comunicazioni tra gli utenti, tramite messaggi istantanei, videochiamate o comunicazioni video. È quindi indispensabile monitorare costantemente le prestazioni della rete per avere la certezza di offrire la migliore esperienza possibile per la modalità di comunicazione prescelta dall'utente.

Le prestazioni di rete possono essere misurate a due livelli:

  - **Prestazioni complessive di rete**   Questo livello di misurazione consente di delineare un quadro complessivo della rete ed è in genere implementato utilizzando sistemi di monitoraggio della rete di altri fornitori. I dati sulla capacità e sulle prestazioni che i sistemi ricevono dai dispositivi di rete remoti, ad esempio i router, vengono trasmessi in tutta la rete per consentire agli amministratori di stabilire in qualsiasi momento lo stato di integrità di qualunque componente di rete.

  - **Prestazioni di un singolo server**   Questo livello di misurazione, circoscritto a un server specifico, consente agli amministratori di valutare le prestazioni di rete di un determinato server per semplificare la risoluzione di un problema specifico o per misurare le prestazioni di tale server, in un dato intervallo di tempo, nell'ambito di una procedura di pianificazione della capacità.

Per monitorare la rete, è possibile utilizzare gli strumenti descritti nelle seguenti sezioni.

## Strumenti per il monitoraggio delle prestazioni complessive di rete

## System Center Operations Manager 2012

System Center Operations Manager è uno strumento di gestione completa dei servizi che può essere facilmente personalizzato e ampliato per migliorare i livelli di servizio in un ambiente IT. I team responsabili della gestione IT e delle operazioni possono quindi identificare e risolvere i problemi che pregiudicano l'integrità dei servizi IT distribuiti. La gestione completa dei servizi, tuttavia, non è limitata agli ambienti Microsoft. Grazie al supporto per WS-Management (Web Services for Management), SNMP (Simple Network Management Protocol) e soluzioni dei partner, anche i sistemi che non eseguono sistemi operativi Microsoft possono essere inclusi nel monitoraggio dei servizi in System Center Operations Manager 2012.

## System Center Operations Manager 2012 e soluzioni di altri fornitori per la gestione della rete

**EMC Smarts**   EMC Solutions for Operations Manager consente una rapida soluzione dei problemi che interessano tutti i livelli di servizio. Con EMC Solutions for Operations Manager, è possibile gestire e monitorare l'intera catena di distribuzione dei servizi IT con una soluzione integrata e automatizzata. Oltre a semplificare l'individuazione delle cause principali dei problemi di disponibilità e prestazioni, consente di risolverle più rapidamente per una riduzione dei costi e delle conseguenze. Tra i vantaggi principali sono inclusi i seguenti:

  - Gestione intuitiva e avanzata   Consente di concentrarsi sulla creazione del valore strategico per l'azienda, anziché perdere tempo a smistare e filtrare manualmente avvisi poco chiari.

  - **Soluzione più rapida**   Consente di risolvere i problemi IT e di far fronte alle esigenze aziendali con maggiore rapidità, per una riduzione dei costi e delle conseguenze.

  - **Operazioni semplificate**   Consente di ovviare alla complessità IT grazie all'integrazione di numerosi terminali, applicazioni e strumenti di gestione.

Per ulteriori informazioni, vedere gli articoli seguenti:

[Microsoft System Center Operations Manager](http://go.microsoft.com/fwlink/p/?linkid=243651)

[Soluzioni per Microsoft System Center Operations Manager](http://www.emc.com/collateral/software/data-sheet/h6135-server-manager-ds.pdf)

## Soluzioni di altri fornitori

**HP Network Management Center (precedentemente noto come HP OpenView)**   [HP Network Management Center](https://h10078.www1.hp.com/cda/hpms/display/main/hpms_content.jsp?zn=bto%26cp=1-11-15-119_4000_100__) è uno strumento di gestione degli errori e delle prestazioni integrato che consente di migliorare le prestazioni e la disponibilità della rete. Network Management Center fa parte della soluzione HP per la gestione automatizzata della rete a livello di errori, prestazioni, configurazione e modifiche.

**Prodotti Cisco per la gestione e l'automazione di rete**   Per le aziende Cisco propone diversi prodotti di gestione, come CiscoWorks LAN Management Solution e Cisco Network Analysis Module, che consentono di migliorare l'efficienza operativa e ridurre i tempi di inattività. Per ulteriori informazioni su questi prodotti, fare riferimento al sito Web di Cisco disponibile all'indirizzo [http://www.cisco.com/en/US/products/sw/netmgtsw/index.html](http://www.cisco.com/en/us/products/sw/netmgtsw/index.html).

Simple Network Management Protocol (SNMP)   Simple Network Management Protocol (SNMP) è uno standard di gestione delle reti che definisce una strategia per la gestione delle reti TCP/IP. SNMP consente di acquisire informazioni sullo stato e sulla configurazione della rete e le invia a un computer riservato per il monitoraggio degli eventi. Questo protocollo di gestione delle reti basato su standard utilizza un'architettura distribuita in cui sono inclusi i seguenti elementi:

  - Più nodi gestiti, ciascuno dei quali è dotato di un'entità SNMP, denominata agente, che consente di accedere in remoto alla strumentazione di gestione.

  - Almeno un'entità SNMP, denominata gestore, che esegue le applicazioni gestionali per il controllo e il monitoraggio degli elementi gestiti (host, router e così via). Il monitoraggio e il controllo avvengono tramite l'accesso alle relative informazioni di gestione.

  - Un protocollo di gestione, SNMP, è utilizzato per comunicare le informazioni sulla gestione tra gli agenti e le stazioni di gestione. Tali informazioni sono costituite da una raccolta di oggetti gestiti che risiedono in un archivio di informazioni virtuale denominato MIB (Management Information Base).


> [!NOTE]
> Nelle sezioni precedenti sono forniti esempi di soluzioni per il monitoraggio delle reti offerte da fornitori diversi. L'elenco non è esaustivo e Microsoft non predilige una soluzione specifica. Contattare un provider dei servizi di rete o il proprio provider di soluzioni tecnologiche per stabilire la soluzione di monitoraggio più adatta per la propria organizzazione.



## Strumenti per monitorare le prestazioni di rete di un singolo server

## System Center Operations Manager 2012

System Center Operations Manager 2012 consente agli amministratori di visualizzare le prestazioni di rete dei singoli server tramite il Management Pack di Windows Server 2012. Il Management Pack del sistema operativo Windows Server include a sua volta un altro Management Pack delle prestazioni che consente agli amministratori di monitorare l'integrità e le prestazioni della scheda di rete.

## Windows Network Monitor

Consente di raccogliere, visualizzare, analizzare l'utilizzo delle risorse in un server e misurare il traffico di rete. Network Monitor esegue solo il monitoraggio dell'attività delle reti. Con l'acquisizione e l'analisi dei dati di rete, insieme ai registri delle prestazioni, è possibile stabilire l'utilizzo della rete, individuare eventuali problemi e prevedere le esigenze future.

Per ulteriori informazioni su Network Monitor 3.4 o per scoprire come installare e configurare Network Monitor per l'acquisizione e l'analisi dei dati, consultare la sessione della panoramica di Network Monitor 3.3. Visitare inoltre il blog di Network Monitor all'indirizzo: <http://blogs.technet.com/b/netmon/>.

