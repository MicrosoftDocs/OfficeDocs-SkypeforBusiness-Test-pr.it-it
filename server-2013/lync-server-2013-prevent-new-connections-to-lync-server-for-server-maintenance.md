---
title: Impedire nuove connessioni a Lync Server per la manutenzione del server
TOCTitle: Impedire nuove connessioni a Lync Server per la manutenzione del server
ms:assetid: 22b27adf-a590-43bd-9306-a5789ae108d7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520964(v=OCS.15)
ms:contentKeyID: 49299927
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Impedire nuove connessioni a Lync Server per la manutenzione del server

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Lync Server consente di portare offline un server, per eseguire ad esempio aggiornamenti software o hardware, senza perdita di servizi a livello degli utenti.

Quando si specifica l'opzione per impedire nuove connessioni o chiamate a un server di un pool, smette di accettare nuove connessioni e chiamate non appena si implementa questa opzione. Le nuove connessioni e le nuove chiamate vengono indirizzate attraverso altri server del pool. Un server che impedisce nuove connessioni consente alle sessioni su connessioni esistenti di continuare fino alla loro fine naturale. Quando tutte le sessioni esistenti sono terminate, il server è pronto per essere portato offline.

Quando si impediscono nuove connessioni a un Front End Server, alcuni servizi e funzionalità di Lync Server si basano sul bilanciamento del carico DNS per garantire un corretto funzionamento. Se non si utilizza il bilanciamento del carico DNS nel pool, le connessioni tramite questi servizi potrebbero non essere reindirizzate ad altri server durante il periodo in cui il server impedisce nuove connessioni. Ciò significa che alcune sessioni e chiamate potrebbero essere interrotte quando il server viene disconnesso. Le funzionalità che si basano sul bilanciamento del carico DNS per garantire il corretto funzionamento di queste opzioni sono le seguenti:

  - Attendant

  - applicazione Annuncio conferenza

  - applicazione Response Group

  - applicazione Annuncio

  - applicazione Parcheggio di chiamata

Per informazioni dettagliate sul bilanciamento del carico DNS, vedere [Bilanciamento del carico DNS in Lync Server 2013](lync-server-2013-dns-load-balancing.md) nella documentazione relativa alla pianificazione.

Oltre a impedire nuove connessioni per tutti i servizi in un server che esegue Lync Server, è inoltre possibile impedire nuove connessioni per singoli servizi di Lync Server. Questo metodo è utile, ad esempio, nei casi in cui è necessario installare un aggiornamento di Lync Server che non richiede l'arresto dell'intero server. Si noti che quando si impediscono le connessioni per un servizio, è necessario selezionare un servizio nel modo in cui è raggruppato e visualizzato nell'elenco dei servizi di Windows. Il servizio Lync Server Front-End e l'agente di raccolta dati per il monitoraggio, ad esempio, sono servizi di Lync Server separati, ma nell'elenco dei servizi di Windows sono riuniti e visualizzati come servizio Lync Server Front End. È possibile impedire nuove connessioni per il servizio Lync Server Front End, ma non si possono impedire nuove connessioni per questi due singoli servizi di Lync Server sottostanti separatamente.

> [!IMPORTANT]  
> Quando si riavvia un server che è stato impostato in modo da impedire nuove connessioni, per impostazione predefinita il server inizierà immediatamente ad accettare nuove connessioni subito dopo l'avvio. Per ovviare a questo problema, prima di riavviare il server impostarlo in modo che sia possibile sospendere e riprendere le operazioni solo manualmente.

## Per impedire nuove connessioni a Lync Server:

1.  Accedere al computer locale come membro del gruppo Administrators.

2.  Aprire la console snap-in Servizi. A tale scopo, fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Strumenti di amministrazione** e quindi **Servizi**.

3.  Nell'elenco fare doppio clic sul servizio Windows Lync Server per cui si desidera impedire nuove connessioni.

4.  In **Stato servizio: In sospeso** nella finestra di dialogo Proprietà fare clic su **Pausa**.

5.  Accanto a **Tipo di avvio** fare clic su **Manuale**. Questa operazione è facoltativa, ma consigliata.
    
    > [!IMPORTANT]  
    > Quando si imposta un server per impedire nuove connessioni e quindi si riavvia il server, per impostazione predefinita il server inizierà immediatamente ad accettare nuove connessioni dopo l'avvio. Per evitarlo, impostare il server solo per la sospensione e la ripresa manuali, prima di riavviarlo.

6.  Al termine, fare clic su **OK**.

