---
title: 'Lync Server 2013: Panoramica del monitoraggio'
TOCTitle: Panoramica del monitoraggio
ms:assetid: 5d5eb658-7fe0-42e6-acaf-700051d0a823
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204937(v=OCS.15)
ms:contentKeyID: 49887582
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica del monitoraggio in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-05_

In Microsoft Lync Server 2013 il monitoraggio viene utilizzato per raccogliere informazioni sull'utilizzo e dati QoE (Quality of Experience) sulle sessioni di comunicazione in cui sono coinvolti gli utenti. Il termine sessione è un termine generico riferito alla connessione di un utente a:

  - Conferenza

  - Una modalità di conferenza, ad esempio audio/video o di condivisione delle applicazioni

  - Un altro utente tramite una conversazione peer-to-peer come la messaggistica istantanea o una chiamata audio


> [!NOTE]
> Lync Server 2013 tiene traccia delle informazioni su ogni sessione, ovvero esecutore e destinatario della chiamata, endpoint utilizzati nella sessione, durata della sessione, qualità percepita della sessione e così via. Lync Server non registra o archivia, tuttavia, la chiamata stessa, incluse le sessioni di messaggistica istantanea. Sebbene Lync Server registri informazioni sulle sessioni di messaggistica istantanea, non registra ogni messaggio istantaneo inviato durante tale sessione.



Le informazioni sui dettagli delle chiamate raccolte da Lync Server possono essere utilizzate per vari scopi, tra i quali:

  - **Rendimento dell'investimento (ROI)** . Gli amministratori possono confrontare i dati di utilizzo raccolti da Monitoring Server con dati simili raccolti per i sistemi di telefonia precedenti, in modo da dimostrare i risparmi e giustificare in modo più convincente la distribuzione di Lync Server.

  - **Gestione dell'inventario dei dispositivi** . Le informazioni di gestione delle risorse consentono agli amministratori di individuare i dispositivi obsoleti ancora in uso che devono essere sostituiti, nonché identificare i dispositivi costosi che risultano inutilizzati.

  - Helpdesk. I dati sulla risoluzione dei problemi consentono ai tecnici dei servizi di supporto di stabilire le cause di una chiamata non riuscita, senza dover raccogliere log sul lato server o client. Questo informazioni sono facilmente accessibili e di immediata comprensione per il personale del supporto tecnico con conoscenze tecniche approfondite di Microsoft Lync 2013 e Lync Server 2013.

  - **Risoluzione dei problemi di sistema** . Gli amministratori hanno la possibilità di rilevare i principali problemi che possono impedire agli utenti finali di eseguire attività di base come partecipare a una conferenza, eseguire una chiamata o inviare un messaggio istantaneo.

Oltre a queste informazioni di base sulle chiamate, Monitoring Server offre anche un meccanismo che consente agli endpoint SIP (come Lync 2013) di rendere disponibili informazioni sulla risoluzione dei problemi che non sarebbero altrimenti accessibili per il server:

  - **Metriche che influiscono sulla qualità** . Queste metriche riguardano l'effettiva trasmissione della chiamata, ovvero offrono una sorta di registro di viaggio del percorso della chiamata in rete. Queste metriche, che includono dati come perdita di pacchetti, instabilità e tempi di round trip, offrono informazioni su cosa accade per la chiamata dal momento in cui lascia l'endpoint di partenza al momento in cui raggiunge l'endpoint di destinazione.

  - **Problemi segnalati all'utente finale** . Queste metriche includono le notifiche di qualità insufficiente presentate da Lync 2013 agli utenti finali nei casi in cui si trovano troppo lontani da un microfono, parlano a voce troppo bassa, utilizzano una connessione di rete di qualità insufficiente o sperimentano servizi di bassa qualità a causa di un altro programma nel computer che sta utilizzando le risorse disponibili.

  - **Informazioni sull'ambiente** . Queste metriche offrono dati dettagliati su aspetti che influiscono sulla qualità delle chiamate, come il tipo di microfono e altoparlanti in uso, se l'utente è connesso tramite VPN e se l'utente sta utilizzando una connessione wireless.

Al termine di ogni chiamata, gli endpoint conformi a SIP trasmettono automaticamente queste informazioni al Front End Server che ha inoltrato la chiamata. Non è necessario eseguire alcuna operazione per fare in modo che gli endpoint trasmettano tali informazioni, perché questo comportamento è incorporato nel protocollo SIP. Se si desidera raccogliere e archiviare tali informazioni, tuttavia, è necessario installare e abilitare il monitoraggio. In questo modo, le informazioni sulle chiamate vengono raccolte dagli agenti in esecuzione nel Front End Server e inoltrate a una coppia di database di SQL Server.

Si noti che il processo di installazione e configurazione del monitoraggio è stato semplificato in Lync Server 2013. Nelle versioni precedenti del software, per eseguire il monitoraggio è necessario un ruolo Monitoring Server separato, che in genere significa un server separato dedicato all'utilizzo come Monitoring Server. In Lync Server 2013, tuttavia, il ruolo Monitoring Server è stato eliminato ed è stato invece collocato in tutti i Front End Server il servizio di monitoraggio, in forma di "agenti di raccolta dati unificati". La collocazione del servizio di monitoraggio offre almeno due vantaggi principali:

  - Riduzione del numero di ruoli del server necessari per l'implementazione di Lync Server 2013. La rimozione del ruolo Monitoring Server contribuisce anche a ridurre i costi, eliminando la necessità di gestire server dedicati per il monitoraggio.

  - Minore complessità di installazione e amministrazione per Lync Server 2013. La collocazione dei servizi di monitoraggio in ogni Front End Server significa che non è più necessario installare, configurare e gestire il ruolo Monitoring Server.

Per ulteriori informazioni, vedere l'argomento [Distribuzione del monitoraggio in Lync Server 2013](lync-server-2013-deploying-monitoring.md) nella guida alla distribuzione di Lync Server 2013.

