---
title: 'Lync Server 2013: Caratteristiche e funzionalità per dispositivi mobili'
TOCTitle: Caratteristiche e funzionalità per dispositivi mobili
ms:assetid: 12517a88-2531-44a5-bea5-d8884aff53eb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh689983(v=OCS.15)
ms:contentKeyID: 49299735
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Caratteristiche e funzionalità per dispositivi mobili in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-19_

    The information in this topic pertains to Cumulative Updates for Lync Server 2013: February 2013.

La funzionalità per dispositivi mobili introdotta negli aggiornamenti cumulativi per Lync Server 2013: febbraio 2013 supporta la funzionalità client per dispositivi mobili di Lync 2010 Mobile e Lync 2013. Quando si distribuisce il servizio Mobility di Lync Server 2013, gli utenti possono utilizzare dispositivi mobili Apple iOS, Android e Windows Phone o Nokia Symbian supportati per eseguire attività quali l'invio e la ricezione di messaggi istantanei, la visualizzazione dei contatti e la visualizzazione della presenza. I dispositivi mobili inoltre supportano alcune funzionalità di VoIP aziendale, tra cui la possibilità di partecipare a una conferenza mediante clic del mouse, la chiamata tramite ufficio, il numero unico, la segreteria telefonica e le chiamate senza risposta. Le nuove funzionalità introdotte negli aggiornamenti cumulativi per Lync Server 2013: febbraio 2013 includono la funzionalità VoIP (Voice over IP) e video (H.264) per i partecipanti alla riunione.

La funzionalità per dispositivi mobili introdotta negli aggiornamenti cumulativi per Lync Server 2013: febbraio 2013 supporta la funzionalità client per dispositivi mobili di Lync 2013. Gli aggiornamenti cumulativi per Lync Server 2013: febbraio 2013 installano l'API Web Unified Communications o UCWA. UCWA è il componente utilizzato per i client di dispositivi mobili di Lync 2013. In Lync Server 2013 viene utilizzato Mcx per i client di Lync 2010 Mobile. Gli aggiornamenti cumulativi per Lync Server 2013: febbraio 2013 introducono UCWA come il nuovo punto di ingresso per i servizi Mobility. Contemporaneamente, Lync Server 2013 implementa il servizio Mobility (Mcx) introdotto negli aggiornamenti cumulativi per Lync Server 2010: novembre 2011 e fornisce il supporto per Lync 2010 Mobile. Quando si distribuiscono gli aggiornamenti cumulativi per Lync Server 2013: febbraio 2013, gli utenti possono utilizzare i dispositivi mobili Apple iOS, Android e Windows Phone supportati per eseguire le attività seguenti:

> [!important]  
> Le funzionalità supportate dal servizio Mobility negli aggiornamenti cumulativi per Lync Server 2010: novembre 2011 sono evidenziate con (Mcx). Tutte le funzionalità elencate sono supportate dall'API UCWA, introdotta negli aggiornamenti cumulativi per Lync Server 2013: febbraio 2013.

  - Invio e ricezione di messaggi istantanei (Mcx)

  - Visualizzazione della presenza (Mcx)

  - Visualizzazione dei contatti (Mcx)

  - Partecipazione a una riunione tramite clic del mouse (Mcx)

  - Chiamata tramite ufficio (Mcx)

  - Numero unico (Mcx)

  - Segreteria telefonica (Mcx)

  - Notifica delle chiamate senza risposta (Mcx)

  - VoIP (Voice over IP)

  - Video partecipanti (H.264)


> [!NOTE]
> Lync 2010 Mobile offre un client per i dispositivi Nokia Symbian. Lync 2013 Mobile non disporrà di un client per i dispositivi Nokia basati su Symbian.



Gli utenti di Apple iPad avranno accesso a funzionalità avanzate. Quando si partecipa a una riunione utilizzando la richiamata audio, un utente di iPad sarà in grado di visualizzare presentazioni di Microsoft PowerPoint caricate in una riunione, condividere applicazioni e desktop, visualizzare l'elenco dei partecipanti alla riunione e ricevere notifiche di altri tipi di contenuti condivisi all'interno della riunione.

> [!tip]  
> Con il numero unico, un utente riceve sul telefono cellulare le chiamate effettuate al suo numero dell'ufficio. Con la chiamata tramite ufficio, l'utente effettua una chiamata in uscita dal client di Lync Mobile utilizzando il numero di un telefono di lavoro anziché il numero del cellulare. Con la chiamata in uscita il client invia una richiesta a Mcx o UCWA (in base alla versione di Lync Mobile) per effettuare la chiamata per suo conto. Il server perciò avvia la chiamata e quindi richiama l'utente sul cellulare. Quando l'utente risponde, il server completa la chiamata componendo il numero dell'altra parte. Mediante la chiamata tramite ufficio, gli utenti possono mantenere la loro identità di lavoro durante una chiamata, pertanto il destinatario non vedrà il numero di cellulare del chiamante e a quest'ultimo non verranno addebitati i costi della chiamata in uscita.


> [!NOTE]
> Non tutte le funzionalità hanno esattamente lo stesso comportamento su tutti i dispositivi mobili. Per informazioni dettagliate sulle funzionalità supportate dai dispositivi mobili, vedere Tabelle di confronto dei client mobili all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=234777">http://go.microsoft.com/fwlink/p/?LinkId=234777</A>. Per informazioni dettagliate sui dispositivi e sui sistemi operativi supportati, vedere gli argomenti relativi ai requisiti in <A href="lync-server-2013-planning-for-mobile-clients.md">Pianificazione dei client mobili</A>.



Quando si utilizza la funzione di individuazione automatica di Lync Server 2013, le applicazioni per dispositivi mobili sono in grado di individuare automaticamente i servizi Web di Lync Server 2013 senza che gli utenti debbano immettere manualmente gli URL nelle impostazioni del dispositivo. Tale immissione manuale degli URL è comunque supportata, principalmente per la risoluzione dei problemi.

> [!important]  
> Mcx e UCWA sono servizi complementari ed entrambi vengono distribuiti per supportare i client di Lync 2010 Mobile e Lync 2013 Mobile. Lync 2013 Mobile non potrà accedere alle distribuzioni di Lync Server 2010. Lync 2010 Mobile e Lync 2013 Mobile saranno in grado di utilizzare una distribuzione di Lync Server 2013 se vengono applicati gli aggiornamenti cumulativi per Lync Server 2013: febbraio 2013.

La funzionalità per dispositivi mobili inoltre supporta le *notifiche Push* per i dispositivi mobili che non supportano le applicazioni eseguite in background. Una notifica Push è una notifica inviata a un dispositivo mobile relativamente a un evento che si verifica mentre un'applicazione per dispositivi mobili non è attiva. Una notifica Push ad esempio può essere inviata per eventi quali inviti di messaggistica istantanea non letti.

Mcx, UCWA, il servizio di individuazione automatica e il supporto per le notifiche Push vengono forniti in Lync Server 2013. Le funzionalità client aggiornate, le capacità e l'utilizzo di UCWA come punto di ingresso per i dispositivi mobili sono introdotti negli aggiornamenti cumulativi per Lync Server 2013: febbraio 2013.

