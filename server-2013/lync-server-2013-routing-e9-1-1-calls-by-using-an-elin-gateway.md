---
title: 'Lync Server 2013: Routing delle chiamate di emergenza tramite un gateway ELIN'
TOCTitle: Routing delle chiamate di emergenza tramite un gateway ELIN
ms:assetid: 5a3997e3-898d-49cb-922a-4184c3373350
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204919(v=OCS.15)
ms:contentKeyID: 49300646
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Routing delle chiamate di emergenza tramite un gateway ELIN in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-05_

Alcuni partner che partecipano al programma Unified Communications Open Interoperability offrono gateway qualificati con supporto ELIN (Emergency Location Identification Number), utilizzabili come alternativa a una connessione trunk SIP a un provider di servizi E9-1-1 qualificato. I gateway ELIN supportano connettività ISDN o CAMA (Centralized Automatic Message Accounting) a servizi E9-1-1 basati su PSTN (Public Switched Telephone Network). Per informazioni dettagliate sui partner che offrono gateway ELIN e collegamenti alla rispettiva documentazione, vedere [http://go.microsoft.com/fwlink/p/?LinkId=248425](http://go.microsoft.com/fwlink/p/?linkid=248425).

Come le connessioni trunk SIP a provider di servizi E9-1-1, anche i gateway ELIN offrono gli strumenti necessari per il routing delle chiamate di emergenza al punto PSAP (Public Safety Answering Point) più appropriato per il chiamante, ma tali gateway utilizzano un numero ELIN come identificatore di posizione. È necessario definire i numeri ELIN per ogni posizione ERL (Emergency Response Location) nell'organizzazione. Per informazioni dettagliate, vedere [Gestione delle posizioni per i gateway ELIN in Lync Server 2013](lync-server-2013-managing-locations-for-elin-gateways.md).

Quando si utilizza un gateway ELIN per le chiamate di emergenza, si utilizza la stessa infrastruttura E9-1-1 di Lync Server che si utilizzerebbe per una connessione trunk SIP. Ovvero, il database del servizio Informazioni percorso fornisce la posizione al client Lync Server e i criteri di percorso abilitano la funzionalità e definiscono il routing. Con un gateway ELIN, tuttavia, è necessario aggiungere i numeri ELIN al database del servizio Informazioni percorso e fare in modo che il gestore PSTN li carichi nel database ALI (Automatic Location Identification).

Quando un client Lync ottiene la posizione dal servizio Informazioni percorso, tale posizione include il numero ELIN. Durante una chiamata di emergenza, il numero ELIN viene incluso insieme alla posizione inviata al gateway ELIN. Il gateway ELIN identifica la chiamata come chiamata di emergenza e scambia il numero chiamante con il numero ELIN. Il gateway ELIN instrada quindi la chiamata alla rete PSTN con il numero ELIN come numero chiamante. Il provider E9-1-1 PSTN cerca il numero ELIN nel database ALI, ovvero un database complementare al database MSAG (Master Street Address Guide). La rete PSTN invia quindi la chiamata al punto PSAP più appropriato in base alla ricerca nel database ALI e il punto PSAP invia i primi che rispondono alla posizione del chiamante in base alla ricerca nel database ALI. Il numero chiamante viene memorizzato nella cache nel gateway ELIN per un periodo di tempo predefinito per le richiamate automatiche. Durante una richiamata automatica, il punto PSAP raggiunge il gateway ELIN che scambia il numero ELIN con il numero DID (Direct Inward Dialing) del chiamante.

I gateway ELIN supportano chiamate di emergenza solo dall'interno della rete dell'organizzazione. Non sono supportate chiamate di emergenza effettuate dall'esterno della rete.


> [!NOTE]
> Per informazioni dettagliate sull'utilizzo di una connessione trunk SIP per le chiamate di emergenza, vedere <A href="lync-server-2013-routing-e9-1-1-calls-by-using-a-sip-trunk.md">Routing delle chiamate di emergenza tramite un trunk SIP in Lync Server 2013</A>.



Il diagramma seguente illustra il routing di una chiamata di emergenza da Lync Server al punto PSAP quando si utilizza un gateway ELIN.

**Routing delle chiamate E9-1-1 con un gateway ELIN**

![Routing delle chiamate ELIN](images/JJ204919.ea68f88a-0fc4-43d4-9660-79a7e8936df1(OCS.15).jpg "Routing delle chiamate ELIN")

1.  A Lync Server viene inviata una richiesta SIP INVITE contenente la posizione, il numero di richiamata automatica del chiamante e (facoltativo) l'URL di notifica e il numero di richiamata automatica per le conferenze.

2.  Lync Server individua il numero di emergenza corrispondente e quindi instrada la chiamata (in base al valore **Utilizzo PSTN** definito nei criteri di percorso applicabili) a un Mediation Server, quindi da tale server a un gateway ELIN.

3.  Il gateway ELIN instrada la chiamata su un trunk ISDN o CAMA alla rete PSTN.

4.  La rete PSTN identifica quindi la chiamata come chiamata di emergenza e la instrada a un router selettivo E9-1-1 nella rete. Tale router selettivo E9-1-1 cerca il numero del chiamante nel database ALI per ottenere la posizione geografica. Il router selettivo E9-1-1 invia la chiamata al punto PSAP più appropriato in base alle informazioni sulla posizione recuperate dal database ALI.

5.  Se sono stati configurati criteri di percorso per le notifiche, a uno o più responsabili della sicurezza dell'organizzazione viene inviato un messaggio istantaneo di notifica dell'emergenza speciale di Lync. Questo messaggio viene sempre visualizzato sullo schermo dei responsabili della sicurezza come popup e contiene nome del chiamante, numero telefonico, ora e posizione. Il personale di sicurezza ha così la possibilità di rispondere rapidamente al chiamante tramite un messaggio istantaneo o una chiamata vocale.

6.  In caso di interruzione prematura della chiamata, il punto PSAP utilizza il numero ELIN per contattare direttamente il chiamante. Il gateway ELIN scambia quindi il numero ELIN con il DID del chiamante.

