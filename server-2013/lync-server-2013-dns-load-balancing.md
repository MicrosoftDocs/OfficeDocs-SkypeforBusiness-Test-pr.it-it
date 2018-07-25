---
title: Bilanciamento del carico DNS in Lync Server 2013
TOCTitle: Bilanciamento del carico DNS in Lync Server 2013
ms:assetid: 7ed0ed20-33ad-4253-926d-21d392590ae7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398634(v=OCS.15)
ms:contentKeyID: 49301115
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Bilanciamento del carico DNS in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-01-15_

In Lync Server è abiltato il bilanciamento del carico DNS, una soluzione software che consente di ridurre in modo significativo il sovraccarico a livello amministrativo per il bilanciamento del carico di rete. Questa soluzione consente di bilanciare il traffico di rete specifico di Lync Server, ad esempio il traffico SIP e il traffico multimediale.

Distribuendo il bilanciamento del carico DNS, è possibile ridurre notevolmente il sovraccarico a livello amministrativo per i servizi di bilanciamento del carico hardware nell'organizzazione. È inoltre possibile eliminare la complessità legata alla risoluzione dei problemi relativi a una configurazione errata dei servizi di bilanciamento del carico per il traffico SIP. È anche possibile impedire le connessioni al server, per poter disconnettere i server. Il bilanciamento del carico DNS garantisce infine che i problemi dei servizi di bilanciamento del carico hardware non influiscano su elementi del traffico SIP, ad esempio il routing delle chiamate di base.

Se si utilizza il bilanciamento del carico DNS, è anche possibile acquistare servizi di bilanciamento del carico hardware a un costo più conveniente rispetto a quello da sostenere se si utilizzano servizi di bilanciamento del carico hardware per tutti i tipi di traffico. È consigliabile utilizzare servizi di bilanciamento del carico che abbiano superato i test di interoperabilità con Lync Server. Per informazioni dettagliate sui test di interoperabilità per i servizi di bilanciamento del carico, vedere "Partner per i servizi di bilanciamento del carico di Lync Server 2010", all'indirizzo <http://go.microsoft.com/fwlink/?linkid=202452>.

Il bilanciamento del carico DNS è supportato per i pool Front End, i pool di server perimetrali, i pool di server Director e i pool di Mediation Server autonomi.

## Bilanciamento del carico DNS in pool Front End e pool di server Director

È possibile utilizzare il bilanciamento del carico DNS per il traffico SIP in pool Front End e pool di server Director. Dopo aver distribuito il bilanciamento del carico DNS, è comunque necessario utilizzare anche servizi di bilanciamento del carico hardware per questi pool, ma solo per il traffico HTTPS da client a server. Il servizio di bilanciamento del carico hardware viene utilizzato per il traffico HTTPS dai client nelle porte 443 e 80.

Sebbene siano comunque necessari servizi di bilanciamento del carico hardware per questi pool, la loro impostazione e l'amministrazione saranno principalmente relative al traffico HTTPS a cui gli amministratori dei servizi di bilanciamento del carico hardware sono abituati.

## Bilanciamento del carico DNS e supporto di server e client precedenti

Il bilanciamento del carico DNS supporta il failover automatico solo per i server che eseguono i client Lync Server 2013 o Lync Server 2010, e Lync 2013 e Lync 2010. Le versioni precedenti dei client e Office Communications Server possono comunque connettersi ai pool in cui è in esecuzione il bilanciamento del carico DNS, ma se non sono in grado di stabilire una connessione al primo server indicato dal bilanciamento del carico DNS, non viene eseguito il failover a un altro server del pool.

Se, inoltre, si utilizza la messaggistica unificata di Exchange, solo Exchange 2010 SP1 o con un Service Pack più recente offre supporto integrato per il bilanciamento del carico DNS di Lync Server. Se si utilizza una versione precedente di Exchange, non saranno disponibili funzionalità di failover per i seguenti scenari di messaggistica unificata di Exchange:

  - Riproduzione della segreteria telefonica VoIP aziendale nel telefono

  - Trasferimento delle chiamate da un Operatore automatico messaggistica unificata di Exchange

Tutti gli altri scenari di messaggistica unificata di Exchange funzioneranno correttamente.

## Distribuzione del bilanciamento del carico DNS in pool Front End e pool di server Director

Per la distribuzione del bilanciamento del carico DNS in pool Front End e pool di server Director è necessario eseguire due passaggi aggiuntivi relativi a FQDN e record DNS.

  - Un pool che utilizza il bilanciamento del carico DNS deve disporre di due nomi di dominio completi (FQDN): il nome di dominio completo del pool standard, che viene utilizzato dal bilanciamento del carico DNS (ad esempio pool01.contoso.com) e che viene risolto negli indirizzi IP fisici dei server del pool e un altro nome di dominio completo per i servizi Web del pool (ad esempio web01.contoso.com), che viene risolto nell'indirizzo IP virtuale del pool.
    
    In Generatore di topologie, se si desidera distribuire il bilanciamento del carico DNS per un pool, per creare il nome di dominio completo aggiuntivo per i servizi Web del pool è necessario selezionare la casella di controllo **Sostituisci FQDN pool servizi Web interno** e digitare il nome di dominio completo nella pagina **Specificare l'URL dei servizi Web** per il pool.

  - Per supportare il nome di dominio completo utilizzato dal bilanciamento del carico DNS, è necessario effettuare il provisioning di DNS per risolvere il nome di dominio completo del pool (ad esempio pool01.contoso.com) negli indirizzi IP di tutti i server del pool (ad esempio 192.168.1.1, 192.168.1.2 e così via). Includere solo gli indirizzi IP dei server attualmente distribuiti.
    

    > [!WARNING]
    > Se si hanno più pool Front End o Front End Server, l'FQDN dei servizi Web esterni deve essere univoco. Ad esempio, se si definisce l'FQDN dei servizi Web esterni di un Front End Server come <STRONG>pool01.contoso.com</STRONG>, non sarà possibile utilizzare <STRONG>pool01.contoso.com</STRONG> per un altro pool Front End o Front End Server. Se si distribuisce anche Director, l'FQDN dei servizi Web definito per ciascun Server Director o pool di server Director deve essere univoco rispetto agli altri Server Director o pool di server Director, e univoco anche rispetto agli altri pool Front End e Front End Server. Se si decide di sostituire i servizi Web interni con un FQDN definito autonomamente, ciascun FQDN deve essere diverso da quello degli altri pool Front End, Server Director o pool di server Director.



## Bilanciamento del carico DNS in pool di server perimetrali

È possibile distribuire il bilanciamento del carico DNS in pool di server perimetrali. In tal caso, è necessario tenere presenti alcune considerazioni.

L'utilizzo del bilanciamento del carico DNS nei server perimetrali comporta una perdita della capacità di failover negli scenari seguenti:

  - Federazione con organizzazioni che eseguono versioni di Office Communications Server precedenti a Lync Server 2010.

  - Scambio di messaggi istantanei con utenti di servizi di messaggistica istantanea pubblica, ad esempio AOL e Yahoo\!, oltre ai server e ai provider basati su XMPP, come Google Talk.
    
    > [!important]  
    > <ul>    
> 
> <li><p>Google Talk è attualmente l'unico partner XMPP supportato.</p></li>    
> 
> 
> <li><p>Dal 1 settembre 2012, la licenza di sottoscrizione utenti per la connettività di messaggistica istantanea pubblica di Microsoft Lync (“PIC USL”) non è più disponibile per l'acquisto per i nuovi contratti o quelli in fase di rinnovo. I clienti con licenze attive potranno continuare a eseguire la federazione con Yahoo! Messenger fino alla data di chiusura del servizio. Giugno 2014 è la data di fine servizio annunciata per Yahoo! e AOL. Per informazioni dettagliate, vedere <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Supporto della connettività per messaggistica istantanea pubblica in Lync Server 2013</a>.</p></li>    </ul>


Questi scenari funzionano a condizione che tutti i server perimetrali nel pool siano in esecuzione, ma se un server perimetrale non è disponibile, tutte le richieste per questi scenari inviate a tale server avranno esito negativo, anziché essere instradate a un altro server perimetrale.

Se si utilizza la messaggistica unificata di Exchange, è necessario utilizzare almeno Exchange 2013 per ottenere il supporto per il bilanciamento del carico DNS di Lync Server nei server perimetrali. Se si utilizza una versione precedente di Exchange, gli utenti remoti non potranno disporre delle funzionalità di failover per i seguenti scenari di messaggistica unificata di Exchange:

  - Riproduzione della segreteria telefonica VoIP aziendale nel telefono

  - Trasferimento delle chiamate da un Operatore automatico messaggistica unificata di Exchange

Tutti gli altri scenari di messaggistica unificata di Exchange funzioneranno correttamente.

Per l'interfaccia perimetrale interna e per quella esterna è necessario utilizzare lo stesso tipo di bilanciamento del carico. Non è possibile utilizzare il bilanciamento del carico DNS in un'interfaccia perimetrale e il bilanciamento del carico hardware nell'altra.

## Distribuzione del bilanciamento del carico DNS in pool di server perimetrali

Per distribuire il bilanciamento del carico DNS nell'interfaccia esterna del pool di server perimetrali, sono necessarie le voci DNS seguenti:

  - Per il servizio Access Edge è necessaria una voce per ogni server nel pool. Ogni voce deve consentire di risolvere il nome di dominio completo del servizio Access Edge di (ad esempio sip.contoso.com) nell'indirizzo IP del servizio Access Edge in uno dei server perimetrali del pool.

  - Per il servizio Web Conferencing Edge è necessaria una voce per ogni server nel pool. Ogni voce deve consentire di risolvere il nome di dominio completo del servizio Web Conferencing Edge (ad esempio webconf.contoso.com) nell'indirizzo IP del servizio Web Conferencing Edge di in uno dei server perimetrali del pool.

  - Per il servizio Audio/Video Edge, è necessaria una voce per ogni server nel pool. Ogni voce deve consentire di risolvere il nome di dominio completo del servizio Audio/Video Edge (ad esempio, av.contoso.com) nell'indirizzo IP del servizio Web Conferencing Edge in uno dei server perimetrali del pool.

Per distribuire il bilanciamento del carico DNS nell'interfaccia interna del pool di server perimetrali, è necessario aggiungere un record A DNS, che consente di risolvere il nome di dominio completo interno del pool di server perimetrali nell'indirizzo IP di ogni server del pool.

## Utilizzo del bilanciamento del carico DNS in pool di Mediation Server

È possibile utilizzare il bilanciamento del carico DNS in pool di Mediation Server autonomi. Tutto il traffico SIP e multimediale viene bilanciato dal bilanciamento del carico DNS.

Per distribuire il bilanciamento del carico DNS in un pool di Mediation Server, è necessario effettuare il provisioning di DNS per risolvere il nome di dominio completo del pool (ad esempio, mediationpool1.contoso.com) negli indirizzi IP di tutti i server del pool (ad esempio 192.168.1.1, 192.168.1.2 e così via).

## Interruzione del traffico a un server con bilanciamento del carico DNS

Se ci si serve del bilanciamento del carico DNS e si ha bisogno di bloccare il traffico diretto verso un computer specifico, non è sufficiente rimuovere le voci di indirizzo IP dal Pool FQDN, ma è necessario rimuovere dal computer anche la voce DNS.

Per il traffico server-to-server, Lync Server 2013 si serve di un bilanciamento del carico basato sulla topologia. I server leggono la topologia pubblicata in archivio di gestione centrale per ottenere i nomi FQDN dei server in essa contenuti, e distribuiscono automaticamente il carico tra i server. Per escludere un server dalla ricezione del traffico server-to-server, è necessario rimuoverlo dalla topologia.

