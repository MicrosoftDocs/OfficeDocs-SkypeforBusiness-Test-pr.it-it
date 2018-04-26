---
title: 'Lync Server 2013: Panoramica dei servizi di emergenza'
TOCTitle: Panoramica dei servizi di emergenza
ms:assetid: c01e6774-bc9f-4c5b-a60b-478b7317b2b7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412936(v=OCS.15)
ms:contentKeyID: 49301868
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica dei servizi di emergenza in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-29_

In Microsoft Lync Server 2013 sono supportate le chiamate ai servizi di emergenza Enhanced 9-1-1 (E9-1-1) da client Lync e dispositivi Lync Phone Edition. Quando si configura Lync Server per E9-1-1, le chiamate di emergenza effettuate da Lync 2013 o Lync Phone Edition includono informazioni ERL (Emergency Response Location) dal database del servizio Informazioni percorso. Le informazioni ERL includono gli indirizzi civici (ovvero la via) e altri dati che consentono di individuare la posizione con maggiore precisione in edifici di uffici e altre strutture con più occupanti. Quando un utente effettua una chiamata di emergenza, Lync Server instrada l'audio della chiamata insieme alle informazioni sulla posizione e la richiamata tramite un Mediation Server a un provider di servizi E9-1-1. Tale provider utilizza l'indirizzo civico del chiamante per instradare la chiamata al centro di raccolta delle chiamate di emergenza (PSAP) responsabile per l'area in cui si trova il chiamante, quindi invia la chiave di query del servizio di emergenza (ESQK, Emergency Service Query Key) che verrà utilizzata dal centro PSAP per cercare le informazioni ERL del chiamante.

In Lync Server sono supportati due metodi per il routing delle chiamate di emergenza a un provider di servizi E9-1-1:

  - Una connessione trunk SIP (Session Initiation Protocol) a un provider di servizi E9-1-1 qualificato

  - Un gateway ELIN (Emergency Location Identification Number) a un provider di servizi E9-1-1 basato su PSTN (Public Switched Telephone Network)

Quando si utilizza un provider di servizi E9-1-1 su trunk SIP, si aggiungono informazioni ERL al database del servizio Informazioni percorso e quindi le posizioni vengono convalidate in base a uno stradario generale gestito dal provider di servizi E9-1-1. Se un provider di servizi E9-1-1 riceve una chiamata senza informazioni sulla posizione o con una posizione che non può essere verificata nello stradario, il provider instrada la chiamata a un centro di risposta alle chiamate di emergenza (ECRC) nazionale/regionale con personale formato appositamente che tenta di ottenere la posizione del chiamante verbalmente, se possibile, e instrada manualmente la chiamata al centro PSAP appropriato. Alcuni provider di servizi E9-1-1 su trunk SIP inoltre forniscono ai clienti un numero DID (Direct Inward Dialing) PSTN per il centro ECRC, offrendo un mezzo alternativo per il routing delle chiamate 9-1-1 in caso di malfunzionamento del trunk SIP per un motivo qualsiasi.

Diversamente dai telefoni TDM (Time Division Multiplexing) e PBX (Private Branch Exchange) basati su IP con posizioni fisse, un endpoint Lync può essere molto mobile. Quando si distribuisce la funzionalità E9-1-1, Lync Server garantisce che la chiamata di emergenza possa essere instradata al centro PSAP responsabile dell'area del chiamante, indipendentemente dalla posizione di quest'ultimo. Se l'ufficio principale dell'utente si trova a Milano, ma l'utente effettua una chiamata di emergenza da un computer in una succursale a Roma, il provider di servizi E9-1-1 su PSTN o su trunk SIP instraderà la chiamata al centro PSAP di Roma e non a quello di Milano.

Quando si utilizza un gateway ELIN, si aggiungono inoltre le informazioni ERL al database del servizio Informazioni percorso, ma si include anche un numero ELIN per ogni posizione. Il numero ELIN diventa il numero chiamante durante la chiamata di emergenza. È quindi necessario verificare che la portante PSTN carichi i numeri ELIN nel database ALI (Automatic Location Identification).


> [!NOTE]
> I dispositivi analogici connessi a Lync non consentono la ricezione di informazioni sulla posizione dal servizio Informazioni percorso o la trasmissione di queste informazioni al provider di servizi E9-1-1. Se si utilizzata l'opzione del provider di servizi E9-1-1 su trunk SIP ed è necessario supportare i servizi E9-1-1 da telefoni analogici, sono disponibili due opzioni: 
> <UL>
> <LI>
> <P><STRONG>Opzione PS-ALI tradizionale</STRONG>&nbsp;&nbsp;&nbsp;Se sono disponibili gateway PSTN locali in ogni sito in cui sono distribuiti telefoni analogici e ogni telefono analogico dispone di un DID, è possibile eseguire il provisioning della posizione del dispositivo analogico direttamente con un provider di servizi PS-ALI (Private Switch/Automatic Location Identification). In questo caso, è necessario configurare criteri vocali di Lync appositi e assegnarli agli oggetti contatto dei dispositivi analogici, in modo che le chiamate E9-1-1 da tali telefoni vengano instradate direttamente tramite il gateway locale al provider PSTN che fornisce i servizi al sito, anziché instradare la chiamata al trunk SIP di un provider di servizi E9-1-1. Quando viene effettuata una chiamata di emergenza, un database presso un provider PS-ALI associato al trunk PSTN mappa il DID di ogni telefono analogico a una posizione fisica, quindi fornisce tale posizione al centro PSAP. Questi record devono essere aggiornati presso il provider di servizi PS-ALI ogni volta che i telefoni vengono spostati in posizioni ERL diverse.</P>
> <LI>
> <P><STRONG>Opzione provider di servizi E9-1-1</STRONG>&nbsp;&nbsp;&nbsp;È possibile registrare i DID dei telefoni analogici e le posizioni ERL corrispondenti presso il provider di servizi E9-1-1, se tale provider lo supporta. In questo modo, se il provider riceve da Lync Server una chiamata che non include dati PIDF-LO, potrà verificare se esiste una corrispondenza nel database per il numero DID del chiamante. In base alle informazioni ERL recuperate dal database, il provider può instradare automaticamente la chiamata di emergenza al centro PSAP corretto, che riceverà il DID del dispositivo analogico e un record ESQK che consente al dispatcher di cercare la posizione del chiamante.</P></LI></UL>Se si utilizza l'opzione del gateway ELIN ed è necessario supportare i servizi E9-1-1 da telefoni analogici, è possibile eseguire il provisioning della posizione del dispositivo analogico direttamente con il provider di servizi PS-ALI, come descritto in precedenza nella prima opzione.



Dal punto di vista di Lync Server, il processo E9-1-1 può essere separato in due fasi:

  - Fase 1: acquisizione di una posizione

  - Fase 2: instradamento della chiamata di emergenza a un provider di servizi E9-1-1

In questa sezione viene descritto il funzionamento di queste due fasi.

Se si prevede di configurare l'infrastruttura per il rilevamento automatico della posizione dei client, è innanzitutto necessario decidere quali elementi di rete verranno utilizzati per il mapping tra chiamanti e posizioni. Per informazioni dettagliate sulle possibili opzioni, vedere [Definizione degli elementi di rete utilizzati per determinare la posizione in Lync Server 2013](lync-server-2013-defining-the-network-elements-used-to-determine-location.md).

## Contenuto della sezione

  - [Acquisizione di una posizione in Lync Server 2013](lync-server-2013-acquiring-a-location.md)

  - [Routing delle chiamate di emergenza tramite un trunk SIP in Lync Server 2013](lync-server-2013-routing-e9-1-1-calls-by-using-a-sip-trunk.md)

  - [Routing delle chiamate di emergenza tramite un gateway ELIN in Lync Server 2013](lync-server-2013-routing-e9-1-1-calls-by-using-an-elin-gateway.md)

