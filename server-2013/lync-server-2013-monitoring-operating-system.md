---
title: 'Lync Server 2013: monitoraggio del sistema operativo'
TOCTitle: Monitoraggio del sistema operativo
ms:assetid: 72406d3e-54c8-4796-8d6d-2144a5b6f030
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn720918(v=OCS.15)
ms:contentKeyID: 62240082
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Monitoraggio del sistema operativo in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-01-26_

In Lync Server 2013 è necessario monitorare le prestazioni di tutti i server e i componenti. Uno dei componenti più importanti, naturalmente, è il sistema operativo stesso. Lync Server 2013 supporta le edizioni x64 di:

  - Windows Server 2008 R2

  - Windows Server 2012 e Windows Server 2012 R2

Il metodo più intuitivo per monitorare un sistema operativo consiste nell'utilizzare il Management Pack del sistema operativo Windows Server, che fornisce informazioni di base sul monitoraggio, ad esempio in termini di prestazioni, integrità e disponibilità, per i computer che eseguono Windows Server 2012, Windows Server 2012 R2 e Windows Server 2008 R2.

I Management Pack consentono di rilevare indicatori di prestazioni ed eventi importanti, inviare avvisi e fornire una risposta automatica, così da ridurre i tempi necessari per la risoluzione dei problemi e migliorare complessivamente le prestazioni e le disponibilità dei sistemi che eseguono sistemi operativi Windows Server.

Oltre ai Management Pack di Windows Server pertinenti per System Center Operations Manager, è possibile monitorare l'integrità del sistema operativo utilizzando le risorse e gli strumenti descritti di seguito (in base alla versione del sistema operativo).

## Windows Server 2008 R2

In Windows Server 2008 R2 sono inclusi gli strumenti e le funzionalità aggiuntive riportate di seguito, che semplificano le attività di base della gestione e del monitoraggio dei sistemi operativi per gli amministratori:

  - **Monitoraggio risorse** è uno strumento avanzato che consente di comprendere in modo approfondito l'utilizzo delle risorse di sistema da parte dei processi e dei servizi. Oltre a effettuare il monitoraggio dell'utilizzo delle risorse in tempo reale, Monitoraggio risorse consente di analizzare i processi che non rispondono, identificare le applicazioni che utilizzano file e controllare processi e servizi.

  - **Componente di analisi dell'affidabilità** è un agente incorporato che fornisce informazioni dettagliate sull'esperienza relative all'utilizzo del sistema e all'affidabilità. Queste informazioni vengono esposte tramite un'interfaccia di Strumentazione gestione Windows (WMI), rendendole disponibili per l'utilizzo da parte di sistemi per lettori portatili. L'esposizione del Componente di analisi dell'affidabilità tramite un'interfaccia WMI consente agli sviluppatori di monitorare e analizzare le applicazioni, aumentando affidabilità e prestazioni.

  - **Windows Server 2008 R2** utilizzano Componente di analisi dell'affidabilità incorporato per calcolare un indice di affidabilità che fornisce, nel tempo, informazioni sull'utilizzo complessivo del sistema e sulla stabilità. Il Componente di analisi dell'affidabilità tiene anche traccia di qualsiasi importante modifica al sistema che potrebbe avere un impatto sulla stabilità, ad esempio aggiornamenti di Windows e installazioni di applicazioni.

## Monitoraggio affidabilità e Monitoraggio prestazioni di Windows Windows Server 2008

Le funzionalità Monitoraggio affidabilità e Monitoraggio prestazioni di Windows costituiscono uno snap-in MMC (Microsoft Management Console) nel quale sono combinate le funzionalità di strumenti autonomi precedenti, tra cui Avvisi e registri di prestazioni, Server Performance Advisor (SPA) e Monitor di sistema. Lo snap-in è provvisto di un'interfaccia grafica per la personalizzazione di insiemi di dati sulle prestazioni e di sessioni di traccia degli eventi.

È inoltre incluso Monitoraggio affidabilità, uno snap-in MMC che consente di tenere traccia delle modifiche apportate al sistema e di confrontarle con le variazioni in termini di stabilità del sistema in una visualizzazione grafica delle relative relazioni.

## Monitoraggio affidabilità e Monitoraggio prestazioni di Windows

Oltre a combinare funzionalità incluse negli strumenti autonomi precedenti, come Avvisi e registri di prestazioni, Server Performance Advisor (SPA) e Monitor di sistema, offre nuove funzionalità per Windows Server 2008 e Windows Server 2008 R2, come le seguenti:

  - Insiemi agenti di raccolta dati

  - Visualizzazione risorse

  - Monitoraggio affidabilità

  - Creazioni guidate e modelli per la creazione di registri

**Insieme agenti di raccolta dati** raggruppa gli agenti di raccolta dati in elementi riutilizzabili per l'utilizzo in scenari diversi di monitoraggio delle prestazioni. Dopo l'archiviazione di un gruppo di agenti di raccolta dati come Insieme agenti di raccolta dati, è possibile eseguire operazioni come ad esempio la pianificazione sull'intero insieme modificando una sola proprietà. Sono inclusi anche modelli di insieme agenti di raccolta dati che consentono agli amministratori di sistema di cominciare a raccogliere immediatamente i dati delle prestazioni specifici di un ruolo di server o di uno scenario di monitoraggio.

La pagina iniziale di Monitoraggio affidabilità e Monitoraggio prestazioni di Windows è la nuova schermata di **Visualizzazione risorse** che offre una panoramica grafica in tempo reale dell'utilizzo della CPU, del disco, della rete e della memoria. Espandendo ognuno di questi elementi monitorati, gli amministratori di sistema possono identificare quali processi vengono utilizzati dalle singole risorse. Nelle versioni precedenti di Windows, i dati in tempo reale specifici di un processo sono disponibili soltanto in modo limitato in Gestione attività.

In **Monitoraggio affidabilità** viene calcolato un indice di stabilità del sistema che indica se eventuali problemi imprevisti hanno ridotto l'affidabilità del sistema. In un grafico dell'indice di stabilità del sistema nel tempo vengono identificate rapidamente le date in cui i problemi hanno iniziato a verificarsi. Nel relativo Rapporto stabilità sistema vengono riportati i dettagli per risolvere la causa principale della riduzione dell'affidabilità. La visualizzazione delle modifiche del sistema, ad esempio l'installazione o la rimozione delle applicazioni, gli aggiornamenti al sistema operativo oppure l'aggiunta o la modifica di driver, affiancata agli errori, ad esempio gli errori delle applicazioni, gli arresti anomali del sistema operativo o gli errori hardware, consente di sviluppare rapidamente una strategia per risolvere i problemi.

È possibile ora aggiungere contatori ai file di registro e pianificarne l'avvio, l'interruzione e la durata tramite un'**interfaccia della creazione guidata**. È inoltre possibile salvare questa configurazione come modello per la raccolta dello stesso registro su computer successivi senza ripetere la selezione dell'agente di raccolta dati e pianificare i processi. In Monitoraggio affidabilità e Monitoraggio prestazioni di Windows sono state incorporate le funzionalità Avvisi e registri di prestazioni per l'utilizzo con qualsiasi insieme agenti di raccolta dati.

