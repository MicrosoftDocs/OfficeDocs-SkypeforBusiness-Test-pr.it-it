---
title: Funzionamento del server chat persistente in Lync Server 2013
TOCTitle: Funzionamento del server chat persistente in Lync Server 2013
ms:assetid: 3d04e9a1-3f0c-458e-bcbe-d27c8c464276
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ683096(v=OCS.15)
ms:contentKeyID: 49887527
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Funzionamento del server chat persistente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-21_

Lync Server 2013, server Chat persistente consente agli utenti di partecipare a conversazioni basate su argomenti che coinvolgono più partecipanti e che vengono salvate in modo permanente. server Chat persistente può essere utile all'organizzazione per le operazioni seguenti:

  - Migliorare le comunicazioni tra team interfunzionali distribuiti in aree geografiche diverse

  - Aumentare la partecipazione e ampliare la conoscenza delle informazioni

  - Migliorare le comunicazioni con l'organizzazione estesa

  - Ridurre il sovraccarico di informazioni

  - Migliorare la capacità di analisi delle informazioni

  - Migliorare la diffusione di conoscenze e informazioni importanti

È possibile distribuire il server Chat persistente come ruolo facoltativo con il pool Lync Server 2013. I servizi Chat persistente vengono eseguiti su un pool dedicato e un pool di server Chat persistente dipende da un pool Lync Server per il routing dei messaggi. I client utilizzano eXtensible Chat Communication Over SIP (XCCOS). I Lync ServerFront End Server sono configurati per il routing del traffico a un pool di server Chat persistente.

## Architettura di alto livello

I diagrammi seguenti forniscono prospettive di alto livello dei servizi e dell'architettura del server Chat persistente.

**Architettura di alto livello del server di Chat persistente**

![Architettura del server Chat persistente.](images/JJ683096.5db6f36f-4461-4d87-ba77-463b7ffe609b(OCS.15).jpg "Architettura del server Chat persistente.")

**Servizi di alto livello del server di Chat persistente**

![Componenti del server Chat persistente.](images/JJ683096.b6d743aa-3a86-4081-aaef-4fe3257db4e7(OCS.15).jpg "Componenti del server Chat persistente.")

Due servizi eseguiti nei server Chat persistenteFront End Server:

  - Chat persistente (Channel Service)

  - Conformità

## Chat persistente (Channel Service)

Chat persistente (Channel Service) è il servizio principale responsabile del server Chat persistente. Questo servizio fornisce le funzioni seguenti:

  - Accetta i messaggi in arrivo

  - Registra ed elenca i partecipanti online in una chat Chat persistente

  - Ritrasmette i messaggi ai sottoscrittori di altri canali

  - Implementa la logica per la gestione dei canali, gli inviti alle chat room, le ricerche e le notifiche di nuovi contenuti

Chat persistente (Channel Service) memorizza il contenuto delle chat room e altri metadati di sistema (regole di autorizzazione e così via) e vi accede utilizzando l'archivio Chat persistente. Questo servizio memorizza i file caricati nelle chat room nell'archivio file di Chat persistente.

## Servizio Conformità

Il servizio Conformità è un componente facoltativo del server Chat persistente ed è responsabile dell'archiviazione di eventi e contenuti delle chat nell'archivio di Conformità Chat persistente. Se per l'organizzazione vigono normative che richiedono l'archiviazione dell'attività di Chat persistente, è possibile distribuire il servizio Conformità Chat persistente facoltativo. Questo viene installato in ogni server Chat persistente di un pool Chat persistente. Quando configurato, il servizio Conformità server Chat persistente registra attività utente come la partecipazione e l'abbandono di chat, nonché l'inserimento e la lettura di messaggi. I file da memorizzare vengono inseriti nell'archivio file di Conformità Chat persistente.

## Servizi Web di Chat persistente

Nei Lync ServerFront End Server vengono eseguiti due servizi che dipendono da Internet Information Services (IIS) e sono implementati come componenti Web:

  - **Servizi Web di Chat persistente per il caricamento/download dei file** Responsabili dell'invio e del recupero dei file da chat.

  - **Servizi Web di Chat persistente per la gestione di chat room** Forniscono agli utenti la possibilità di gestire le proprie chat room e di crearne di nuove.

## Iniziare a utilizzare server Chat persistente

server Chat persistente è un ruolo server facoltativo all'interno dell'infrastruttura di Lync Server 2013. Se si installa il ruolo server Chat persistente, tutti gli utenti abilitati tramite criterio da un amministratore possono utilizzare Chat persistente con il client Lync 2013. Per dettagli sulla distribuzione di server Chat persistente e sull'abilitazione degli utenti all'impiego di funzionalità tramite criteri, vedere [Distribuzione del server Chat persistente in Lync Server 2013](lync-server-2013-deploying-persistent-chat-server.md).

Per informazioni dettagliate sulla configurazione delle impostazioni per la distribuzione di server Chat persistente, vedere [Distribuzione del server Chat persistente in Lync Server 2013](lync-server-2013-deploying-persistent-chat-server.md) e [Gestione del server chat persistente di Lync Server 2013](managing-lync-server-2013-persistent-chat-server.md).

Per informazioni dettagliate sull'abilitazione degli utenti tramite criteri all'utilizzo delle funzionalità di Chat persistente nel client Lync 2013, vedere [Distribuzione del server Chat persistente in Lync Server 2013](lync-server-2013-deploying-persistent-chat-server.md) e [Gestione del server chat persistente di Lync Server 2013](managing-lync-server-2013-persistent-chat-server.md).

Se è stato distribuito il servizio Conformità Chat persistente, vedere [Gestione del server chat persistente di Lync Server 2013](managing-lync-server-2013-persistent-chat-server.md) per dettagli sulla configurazione delle impostazioni necessarie.

## Flussi di chiamate con Chat persistente

Il client Lync comunica con il servizio Chat persistente utilizzando XCCOS. Le sequenze seguenti descrivono il processo di accesso e un tipico scenario di inserimento di messaggi e sottoscrizione a una chat.

## Accesso

La sequenza seguente descrive il processo di accesso.

1.  Il client Lync invia prima un messaggio SIP SUBSCRIBE per recuperare dal server il documento di provisioning in-band. Questo documento indica se Chat persistente è abilitato o disabilitato per l'utente e riporta l'elenco degli URI SIP relativo al pool di server Chat persistente.

2.  Il client Lync invia un messaggio SIP INVITE all'URI SIP del server Chat persistente ottenuto nel passaggio precedente. La sequenza di INVITE è seguita da messaggi 200 OK e ACK. Il client Lync ha ora aperto una sessione SIP con un endpoint del server Chat persistente e comunica pertanto con questo inviando messaggi SIP INFO contenenti messaggi di chat o comandi che richiedono al server di eseguire un'azione. Tutti questi messaggi vengono riconosciuti con messaggi 200 OK o 503 (ovvero di servizio non disponibile nel caso di carico pesante del server). Se il client riceve una risposta 503, tenta di nuovo l'invio del messaggio. Questo esempio non include una risposta 503. Se il server accetta il messaggio o il comando e invia un messaggio 200 OK, fornisce una risposta al client con un messaggio SIP INFO distinto. Questa risposta include un riferimento al comando di origine.

3.  Il client Lync invia un messaggio SIP INFO contenente il comando XCCOS **getserverinfo**. Il server Chat persistente risponde con un nuovo messaggio SIP INFO che contiene informazioni sulla configurazione del servizio Chat persistente.

4.  Il client Lync invia un messaggio SIP INFO che contiene il comando XCCOS **getassociations**. Il server Chat persistente risponde con un nuovo messaggio SIP INFO contenente l'elenco di chat di cui l'utente è membro. Il client Lync ripete il comando per recuperare l'elenco di chat di cui l'utente è responsabile.

5.  Il client Lync ottiene l'elenco delle chat seguite dal documento di "presenza", in cui ogni chat seguita è rappresentata da una categoria "roomSetting". La partecipazione a tutte le chat seguite avviene mediante un singolo messaggio SIP INFO contenente il comando XCCOS **bjoin** che contiene l'elenco degli URI delle chat. Poiché l'elenco delle chat seguite è mantenuto nel server, i client presenti in qualsiasi computer dispongono dello stesso elenco di chat seguite per l'URI utente specificato. Il client Lync mantiene inoltre l'elenco delle chat aperte (se questa opzione viene abilitata dall'utente) nel Registro di sistema del computer locale e partecipa a ognuna di esse al momento dell'accesso inviando un messaggio SIP INFO che contiene il comando XCCOS **join** per ogni chat aperta. Poiché questo elenco viene mantenuto nel Registro di sistema, può essere diverso in due client Lync in esecuzione in computer diversi.

6.  Per ogni chat cui l'utente si unisce, il client Lync invia un messaggio SIP INFO che contiene il comando XCCOS **bccontext**. Il server Chat persistente risponde con un nuovo messaggio SIP INFO che contiene il messaggio chat più recente.

7.  Il client Lync invia un messaggio SIP INFO che contiene un comando XCCOS **getinv** (per ottenere un invito) per richiedere inviti a nuove chat che il client non ha ancora rilevato. In un messaggio SIP INFO separato, server Chat persistente restituisce un elenco di tali chat.

## Sottoscrizione a una chat e inserimento di un messaggio

La sequenza seguente descrive un tipico scenario di sottoscrizione a una chat e di inserimento di un messaggio.

1.  Dal client Lync l'utente 1 fa clic su **Partecipa a una chat room**, su **Cerca** e quindi immette alcuni criteri di ricerca. Il client invia un messaggio SIP INFO che contiene il comando XCCOS **chansrch** (ricerca di chat) insieme ai criteri di ricerca. server Chat persistente esegue query sul database back-end e risponde con un nuovo messaggio SIP INFO che contiene un elenco delle chat disponibili che soddisfano i criteri di ricerca.

2.  L'utente 1 seleziona la chat cui desidera unirsi e quindi fa clic su **Segui questa chat room**. Il client invia al server Chat persistente un messaggio SIP INFO che contiene il comando XCCOS **join** e l'ID della chat selezionata dall'utente. Il server Chat persistente risponde con un messaggio SIP INFO che contiene i dati di provisioning.

3.  Il client Lync invia al server Chat persistente un messaggio SIP INFO che contiene il comando XCCOS **bccontext** (contesto di backchat). Il server Chat persistente recupera la cronologia chat e la restituisce al client in un messaggio SIP INFO separato. A questo punto, l'utente accede alla chat room ed è pronto a partecipare.

4.  L'utente 1 immette un nuovo messaggio e quindi fa clic su **Invia**. Il client Lync inserisce il messaggio nella chat con un comando SIP INFO XCCOS **grpchat**. Il server Chat persistente memorizza una copia del nuovo messaggio nel database back-end Chat persistente.

5.  Il server Chat persistente invia una copia separata del messaggio contenente il comando SIP INFO XCCOS **grpchat** all'utente 2, che già si è unito alla chat room.

## Flussi di chiamate con Conformità Chat persistente

Il server Chat persistente utilizza Accodamento messaggi (noto anche come MSMQ) e un ulteriore database di conformità (mgccomp) per elaborare i dati relativi alla conformità. Come esempio di elaborazione degli eventi di conformità, la sequenza di eventi seguente descrive come viene elaborato un evento di inserimento di un messaggio.

1.  Un utente inserisce un messaggio in una chat.

2.  Il server Chat persistente inserisce le informazioni relative all'evento in una coda di Accodamento messaggi privata.

3.  Il server Conformità Chat persistente legge l'evento dalla coda e lo inserisce nel database mgccomp per elaborarlo in seguito.

4.  Il server Conformità Chat persistente elabora periodicamente un set di eventi nel database e lo invia all'adattatore Conformità Chat persistente per l'elaborazione.

5.  Se l'adattatore elabora correttamente i dati, il server Conformità Chat persistente elimina gli eventi dal database mgccomp.

