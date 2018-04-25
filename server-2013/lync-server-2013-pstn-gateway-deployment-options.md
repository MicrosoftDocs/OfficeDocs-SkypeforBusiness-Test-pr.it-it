---
title: 'Lync Server 2013: Opzioni di distribuzione di gateway PSTN'
TOCTitle: Opzioni di distribuzione di gateway PSTN
ms:assetid: d1ab4f74-18aa-40c7-a8cf-ec806cf6e28a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398899(v=OCS.15)
ms:contentKeyID: 49302059
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Opzioni di distribuzione di gateway PSTN in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

## Gateway PSTN

I gateway PSTN (Public Switched Telephone Network) sono componenti hardware di terze parti che convertono i segnali e i dati multimediali tra l'infrastruttura di VoIP aziendale e la rete PSTN, direttamente o tramite connessione a trunk SIP. In entrambe le topologie il gateway termina la rete PSTN. È isolato nella propria subnet e connesso alla rete aziendale tramite il Mediation Server.

Un'azienda con più siti in genere distribuisce uno o più gateway in ogni sito. I siti di succursale possono connettersi alla rete PSTN tramite un gateway o un Survivable Branch Appliance, che combina gateway e server in un'unica soluzione. Se i siti di succursale utilizzano un gateway, nel sito sono necessari sia una funzione di registrazione che un Mediation Server, a meno che il collegamento WAN non sia resiliente. Uno o più Mediation Server, collocati in Front End Server, possono instradare le chiamate per uno o più gateway in ogni sito. È consigliabile distribuire la funzione di registrazione, il Mediation Server e il gateway necessari nel sito come Survivable Branch Appliance.

Stabilire il numero, le dimensioni e la posizione dei gateway PSTN rappresenta forse la decisione più importante e onerosa che è necessario prendere quando si pianifica l'infrastruttura di VoIP aziendale.

Vengono elencate di seguito le domande principali relative agli aspetti da prendere in considerazione. Tenere presente che le risposte a queste domande sono tutte interdipendenti.

  - Quanti gateway PSTN sono necessari? La risposta dipende dal numero di utenti, dal numero previsto di chiamate simultanee (carico del traffico) e dal numero di siti (ogni sito ne richiede uno).

  - Quale dimensione devono avere i gateway? La risposta dipende dal numero di utenti nel sito e dal carico del traffico.

  - Dove devono trovarsi i gateway? La risposta dipende in parte dalla topologia e in parte dalla distribuzione geografica dell'organizzazione.

È inoltre consigliabile tenere conto delle opzioni di topologie di gateway. Per informazioni dettagliate, vedere la sezione Topologie di gateway più avanti in questo argomento.

## Supporto di trunk M:N

I Mediation Server possono instradare le chiamate tramite più gateway, controller SBC (Session Border Controller) forniti dai provider di servizi telefonici Internet o una combinazione dei due. Inoltre, più Mediation Server nel pool possono interagire con più gateway. La route logica definita tra un Mediation Server e un gateway è denominata *trunk* . Quando un utente interno effettua una chiamata PSTN, la logica di routing in uscita nel pool Front End sceglie quale trunk utilizzare tra tutte le combinazioni possibili eventualmente disponibili per il routing della chiamata in questione. Grazie al bilanciamento del carico DNS, se una chiamata non riesce a raggiungere un gateway a causa di un problema relativo a un determinato Mediation Server nel pool, viene eseguito un nuovo tentativo di chiamata a un Mediation Server alternativo nel pool.

Per informazioni dettagliate sulla pianificazione di più gateway, vedere [Trunk con relazioni molti-a-molti in Lync Server 2013](lync-server-2013-m-n-trunk.md).

Per informazioni dettagliate su altri miglioramenti apportati al routing in uscita, vedere [Route vocali in Lync Server 2013](lync-server-2013-voice-routes.md).

## Topologie di gateway

Quando si considerano gli aspetti fondamentali della distribuzione dei gateway, eseguire le operazioni seguenti:

1.  Contare i siti nei quali si desidera fornire la connettività PSTN utilizzando VoIP aziendale.

2.  Fare una stima del traffico in ogni sito (numero di utenti e numero medio di chiamate all'ora per utente).

3.  Distribuire uno o più gateway in ogni sede per gestire il traffico previsto.

Nella figura che segue è illustrata la topologia distribuita dei gateway risultante.

**Topologia dei gateway distribuita**

![Diagramma della topologia con gateway distribuiti](images/Gg398899.f0f65a0b-a462-491a-878b-4d4bf0a96f6d(OCS.15).jpg "Diagramma della topologia con gateway distribuiti")

Con questa topologia, le chiamate tra i dipendenti di ogni sito e tra i siti vengono tutte instradate tramite la rete Intranet. Le chiamate alla rete PSTN vengono instradate tramite la rete IP aziendale ai gateway più vicini alla posizione dei numeri di destinazione. Se però l'organizzazione supporta decine, centinaia o addirittura migliaia di siti distribuiti in uno o più continenti, come avviene in molti istituti finanziari e altre grandi aziende, la distribuzione di un gateway separato in ogni sito non è una soluzione pratica.

Per risolvere questo problema, molte aziende di grandi dimensioni preferiscono distribuire uno o alcuni siti centrali di telefonia di grandi dimensioni, come illustrato nella figura che segue.

**Topologia di un sito centrale di telefonia**

![Diagramma della topologia con gateway di data center](images/Gg398899.927f4808-bf74-405a-be20-2cd9cd87af6d(OCS.15).jpg "Diagramma della topologia con gateway di data center")

In questa topologia vengono distribuiti in ogni sito centrale diversi gateway di grandi dimensioni, sufficienti per gestire il carico di utenti previsto. Tutte le chiamate agli utenti dell'azienda vengono inoltrate dal provider di servizi telefonici dell'azienda a un sito centrale. La logica di routing nel sito centrale determina se la chiamata deve essere instradata tramite la rete Intranet o alla rete PSTN.

## Posizione dei gateway

Anche la posizione dei gateway può determinare la scelta dei tipi di gateway e la modalità di configurazione. Sono disponibili decine di protocolli PSTN, nessuno dei quali rappresenta uno standard mondiale. La presenza di tutti i gateway nello stesso paese non costituisce un problema. Se invece i gateway vengono distribuiti in diversi paesi, è necessario configurare ognuno di essi in base agli standard PSTN locali. Inoltre, i gateway certificati per il funzionamento in Canada, ad esempio, potrebbero non essere certificati in India, in Brasile o nell'Unione Europea.

## Dimensione e numero di gateway

I gateway PSTN distribuiti nella maggior parte delle organizzazioni variano in dimensione da 2 a 960 porte. Sono disponibili anche gateway più grandi, ma vengono utilizzati principalmente dai provider di servizi telefonici. Per stimare il numero di porte richieste nell'organizzazione, attenersi alle linee guida seguenti:

  - Per le organizzazioni che fanno un uso limitato della telefonia (una chiamata PSTN all'ora per ogni utente) è necessario allocare una porta ogni 15 utenti. Se, ad esempio, gli utenti sono 20, è necessario un gateway con due porte.

  - Per le organizzazioni che fanno un uso moderato della telefonia (due chiamate PSTN all'ora per ogni utente) è necessario allocare una porta ogni 10 utenti. Se ad esempio gli utenti sono 100, è necessario un totale di 10 porte allocate tra uno o più gateway.

  - Per le organizzazioni che fanno un uso intenso della telefonia (tre o più chiamate PSTN all'ora per ogni utente) è necessario allocare una porta ogni cinque utenti. Se ad esempio gli utenti sono 47.000, è necessario un totale di 9.400 porte allocate tra almeno 10 gateway di grandi dimensioni.

  - Con l'aumento del numero di utenti o del traffico nell'organizzazione, è possibile acquisire porte aggiuntive.

Per ogni determinato numero di utenti da supportare, è possibile scegliere se supportare meno gateway di dimensioni maggiori o più gateway di dimensioni minori. Di norma, è consigliabile distribuire un minimo di 2 gateway per un'organizzazione, in modo da poter garantire la disponibilità nel caso che uno si blocchi.

A ogni gateway PSTN distribuito deve essere associato almeno un Mediation Server corrispondente.

