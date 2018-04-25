---
title: Distribuzione del monitoraggio in Lync Server 2013
TOCTitle: Distribuzione del monitoraggio in Lync Server 2013
ms:assetid: 117f4a3e-0670-4388-a553-b9854921145f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398199(v=OCS.15)
ms:contentKeyID: 49299726
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuzione del monitoraggio in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-12-17_

Sono state apportate modifiche rilevanti all'infrastruttura di monitoraggio di Microsoft Lync Server 2013, a partire dal fatto che il ruolo Monitoring Server è stato deprecato. Al posto di ruoli server Monitoring Server separati (che normalmente richiedono la configurazione di computer dedicati come server di monitoraggio nelle organizzazioni), i servizi di monitoraggio sono ora collocati sui singoli server front-end. Questa modifica, tra le altre cose, consente di:

  - Ridurre il numero di ruoli server necessari durante l'implementazione di Lync Server 2013. In questo caso, il decremento del ruolo server Monitoring Server si traduce anche in una riduzione dei costi poiché non è più necessario mantenere server dedicati per il monitoraggio.

  - Ridurre la complessità della configurazione e installazione di Lync Server. Collocando automaticamente i servizi di monitoraggio su ogni server front-end, non è più necessario installare, configurare e gestire il ruolo Monitoring Server.


> [!NOTE]
> Anche il ruolo Server di archiviazione è stato deprecato in Lync Server 2013. Come i servizi di monitoraggio, anche i servizi di archiviazione di Lync Server 2013 ora sono collocati sui singoli server front-end. È importante tenerlo presente semplicemente perché il monitoraggio e l'archiviazione spesso condividono la stessa istanza di database di SQL Server.



È evidente che queste modifiche hanno un impatto considerevole sulle modalità di installazione e gestione dei servizi di monitoraggio. Ad esempio, dato che il ruolo Monitoring Server non esiste più, il nodo Monitoring Server è stato rimosso dal Generatore di topologie di Lync Server. Questo, a sua volta, significa che non viene più utilizzata la procedura guidata per la creazione di server di monitoraggio del Generatore di topologie per aggiungere un nuovo server di monitoraggio alla topologia. Questa procedura guidata, infatti, non esiste più. L'implementazione di servizi di monitoraggio all'interno della topologia, invece, avviene generalmente nei due modi seguenti:

1.  Abilitazione del monitoraggio durante la configurazione di un nuovo pool di Lync Server (in Lync Server 2013 il monitoraggio viene abilitato o disabilitato per singoli pool). Si noti che è possibile abilitare il monitoraggio per un pool senza raccogliere effettivamente dati di monitoraggio. Questo processo è illustrato nella sezione relativa alla configurazione delle impostazioni di registrazione dettagli chiamata e QoE di questa documentazione.

2.  Associazione di un archivio (database) di monitoraggio al nuovo pool. Tenere presente che un archivio di monitoraggio può essere associato a più pool. A seconda del numero di utenti ospitati nei pool di registrazione, questo comporta che non è necessario configurare un database di monitoraggio separato per ogni pool, ma un singolo archivio di monitoraggio può essere utilizzato da più pool.

Sebbene spesso risulti più semplice abilitare il monitoraggio al momento della creazione di un nuovo pool, è anche possibile creare un nuovo pool con il monitoraggio disabilitato. In questo caso, è possibile abilitare il servizio in un secondo momento utilizzando il Generatore di topologie, che consente di attivare o disattivare il monitoraggio di topologie o di associare un pool a un diverso archivio di monitoraggio. Tenere presente che, sebbene non esista più il ruolo Monitoring Server, è comunque necessario creare uno o più archivi di monitoraggio, ovvero i database back-end utilizzati per archiviare i dati raccolti dal servizio di monitoraggio. Questi database back-end possono essere creati mediante Microsoft SQL Server 2008 R2 o Microsoft SQL Server 2012.


> [!NOTE]
> Se è stato abilitato il monitoraggio per un pool, è possibile disabilitare il processo di raccolta dei dati di monitoraggio senza dover modificare la topologia: Lync Server Management Shell consente di disabilitare (e successivamente riabilitare) la raccolta dei dati di registrazione dettagli chiamata (CDR) o relativi alla qualità percepita dagli utenti (QoE). Per ulteriori informazioni, vedere la sezione relativa alla configurazione delle impostazioni di registrazione dettagli chiamata e QoE di questa documentazione.



Un altro importante miglioramento del monitoraggio introdotto in Lync Server 2013 consiste nel fatto che i rapporti di monitoraggio di Lync Server ora supportano IPv6: nei rapporti che utilizzano il campo Indirizzo IP verranno visualizzati gli indirizzi IPv4 o IPv6 a seconda 1) della query SQL utilizzata e 2) del fatto che l'indirizzo IPv6 sia archiviato o meno nel database di monitoraggio.


> [!NOTE]
> Assicurare che il tipo di avvio del servizio SQL Server Agent sia impostato su Automatico e che il servizio SQL Server Agent sia in esecuzione per l'istanza SQL che include i database di monitoraggio, in modo che sia possibile eseguire i processi di manutenzione predefiniti di SQL Server per il monitoraggio in base alla relativa pianificazione sotto il controllo del servizio SQL Server Agent.



In questa documentazione viene illustrato il processo di installazione e configurazione del monitoraggio e di Relazioni monitoraggio per Lync Server 2013. Sono fornite istruzioni dettagliate per le seguenti operazioni:

  - Abilitare il monitoraggio nella topologia e associare un archivio di monitoraggio a un pool Front End.

  - Installare SQL Server Reporting Services e Relazioni monitoraggio di Lync Server, ovvero rapporti preconfigurati che forniscono diverse visualizzazioni delle informazioni archiviate in un database di monitoraggio.

  - Configurare la raccolta dei dati di registrazione dettagli chiamata (CDR) e qualità percepita dagli utenti (QoE). Registrazione dettagli chiamata consente di tenere traccia dell'utilizzo delle funzionalità di Lync Server, quali chiamate telefoniche VoIP, messaggistica istantanea, trasferimenti di file, conferenze audio/video e sessioni di condivisione di applicazioni. Le metriche QoE tengono traccia della qualità delle chiamate audio e video effettuate nell'organizzazione, includendo informazioni quali il numero di pacchetti di rete persi, i rumori di fondo e la quantità di "instabilità" (differenze nel ritardo dei pacchetti.

  - Eliminare manualmente i record CDR e/o QoE dal database di monitoraggio.

