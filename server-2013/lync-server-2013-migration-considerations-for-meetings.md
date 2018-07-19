---
title: Considerazioni sulla migrazione per le riunioni
TOCTitle: Considerazioni sulla migrazione per le riunioni
ms:assetid: a9807d58-99a3-4cff-b4c6-74950d106a2b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412800(v=OCS.15)
ms:contentKeyID: 61142650
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Considerazioni sulla migrazione per le riunioni

 

_**Ultima modifica dell'argomento:** 2014-02-10_

In questa sezione vengono trattati gli argomenti seguenti:

  - Modifiche apportate alle riunioni in Microsoft Lync Server 2013

  - Migrazione degli utenti in base alle esigenze per le conferenze

  - Migrazione di riunioni esistenti e del contenuto delle riunioni

  - Esperienza utente durante la migrazione di Lync Server 2010

  - Esperienza utente durante la migrazione di Office Communications Server 2007 R2

  - Compatibilità di Microsoft Lync 2013 con riunioni con versioni di server precedenti

## Modifiche apportate alle riunioni in Lync Server 2013

**Funzionalità di Lync Server 2013.**   Lync Server 2013 offre nuove funzionalità per le conferenze che divengono disponibili per gli utenti dopo che i relativi account vengono spostati in Lync Server 2013 e che gli utenti stessi effettuano l'accesso al nuovo client di Lync 2013. Le nuove funzionalità sono descritte in [Nuove funzionalità di conferenza in Lync Server 2013](lync-server-2013-new-conferencing-features.md) e in [Novità per i client in Lync Server 2013](lync-server-2013-what-s-new-for-clients.md).

**URL riunione.**   Come in Lync Server 2010, tutte le nuove riunioni pianificate in Lync Server 2013 sono caratterizzate da un prefisso URL https:// e le riunioni esistenti vengono migrate unitamente agli account utente. Lync Server 2013 non supporta tuttavia la conferenza telefonica di Office Communications Server 2007 R2 (prefisso URL conf://) o la conferenza Web (prefisso URL meet://). Per ulteriori informazioni, vedere "Migrazione di riunioni da Office Communications Server 2007 R2" più avanti in questo argomento.

**Supporto per client.**   A differenza di Lync Server 2010, Lync Server 2013 non supporta i client di Office Communicator per le conferenze. Non è quindi possibile utilizzare i seguenti client per partecipare a riunioni pianificate tramite il componente aggiuntivo per riunioni online per Lync 2013:

  - Office Communicator 2007 R2

  - Microsoft Office Communications Server 2007 R2 Attendant

  - Office Communicator 2007

  - Office Live Meeting 2007

Durante la migrazione e finché l'aggiornamento dei client non viene completato gli utenti di Office Communicator 2007 R2 devono utilizzare Lync Web App 2013 per partecipare a riunioni di Lync Server 2013. Si noti che gli utenti di Office Communicator 2007 R2 possono continuare a utilizzare il client esistente in Lync Server 2013 per le funzionalità di presenza e messaggistica immediata, tuttavia le funzionalità per le conferenze non sono supportate.


## Migrazione degli utenti in base alle esigenze per le conferenze

**Organizzatori di riunioni frequenti.**   È consigliabile eseguire nella prima parte del processo la migrazione degli organizzatori di riunioni frequenti, in modo che possano usufruire dei vantaggi offerti dalle nuove funzionalità di Lync Server 2013 e Lync 2013 descritte in [Nuove funzionalità di conferenza in Lync Server 2013](lync-server-2013-new-conferencing-features.md) e [Novità per i client in Lync Server 2013](lync-server-2013-what-s-new-for-clients.md).

**Utenti di Live Meeting.**   Se si intende eseguire la migrazione da Office Communications Server 2007 R2 e sono presenti utenti che devono utilizzare funzionalità di conferenza Web specifiche di Live Meeting, in particolare il supporto per riunioni di grandi dimensioni e le sale private, è possibile scegliere tra le opzioni seguenti:

  - Consigliare agli organizzatori di utilizzare il servizio Live Meeting, se disponibile nell'organizzazione.

  - Lasciare gli organizzatori nella versione precedente di Office Communications Server, in modo che possano continuare a pianificare conferenze Web di Live Meeting basate sul server.

## Migrazione di riunioni esistenti e del contenuto delle riunioni

## Migrazione di riunioni da Lync Server 2010

Quando si sposta un utente da Lync Server 2010 a Lync Server 2013, insieme all'account utente vengono spostate anche le seguenti informazioni:

  - Le riunioni già pianificate dall'utente. Vengono spostate anche le directory e i dati delle conferenze.

  - Il PIN dell'utente. Il PIN corrente dell'utente continua a funzionare fino alla scadenza o alla richiesta di un nuovo PIN da parte dell'utente stesso.

Le seguenti informazioni sull'account utente non vengono tuttavia spostate nel nuovo server:

  - Contenuto della riunione, ad esempio presentazioni di PowerPoint, contenuto della lavagna e dati dei sondaggi

Per spostare il contenuto condiviso nelle riunioni, utilizzare il parametro MoveMeetingContent del cmdlet Move-CsUser. Per informazioni dettagliate su come utilizzare questo cmdlet, vedere [Move-CsUser](https://docs.microsoft.com/en-us/powershell/module/skype/Move-CsUser) nella documentazione dei cmdlet di Lync Server 2013.

## Migrazione di riunioni da Office Communications Server 2007 R2

Le riunioni di Office Communications Server 2007 R2 possono essere conferenze telefoniche (prefisso URL conf://) o conferenze Web (prefisso URL meet://). In Lync Server 2013 tali conferenze conf:// e meet:// non sono supportate, pertanto non ne verrà eseguita la migrazione congiuntamente all'account utente. Dopo la migrazione sarà necessario comunicare agli utenti di aggiornare i collegamenti per le eventuali riunioni online pianificate. Gli utenti potranno effettuare tale operazione dopo aver installato il client di Lync 2013 aprendo una convocazione di riunione pianificata, in modo da aggiornare l'URL della riunione, e quindi inviando di nuovo la convocazione ai partecipanti.

## Esperienza utente durante la migrazione di Lync Server 2010

In questa sezione viene riepilogata l'esperienza utente con le conferenze quando si esegue la migrazione da Lync 2010. Per ulteriori informazioni sull'interazione e la coesistenza dei client di Lync Server 2013 con versioni precedenti di client e server, vedere [Interoperabilità dei client in Lync 2013](lync-server-2013-client-interoperability-in-lync-2013.md).

## Partecipazione a riunioni di Lync Server 2010 con un client di Lync 2013

Durante la migrazione da Lync Server 2010 potrebbe verificarsi un periodo di coesistenza in cui gli utenti possono partecipare a riunioni di Lync Server 2010 con un client di Lync 2013. Tali utenti hanno accesso alle funzionalità di Lync 2013 con le eccezioni seguenti:

  - Nelle opzioni di gestione **Partecipanti**, accessibili tramite l'icona Persone nella finestra della riunione, l'opzione **Messaggistica istantanea della riunione non disponibile** non funziona.

  - La Visualizzazione Raccolta non funziona nelle conferenze video. L'utente vede solo l'interlocutore attivo, anziché tutti gli interlocutori. Nell'elenco delle opzioni **Scegliere un Layout** l'opzione **Visualizzazione Raccolta** non è disponibile.

  - Per impostazione predefinita, nelle conferenze video viene visualizzato l'elenco dei partecipanti.

  - Quando si fa clic con il pulsante destro del mouse su un utente nell'elenco dei partecipanti, le opzioni di gestione dei partecipanti **Blocca l'evidenza video** e **Aggiungi alla raccolta** non sono disponibili.

## Esperienza utente durante la migrazione di Office Communications Server 2007 R2

In questa sezione viene riepilogata l'esperienza utente con le conferenze quando si esegue la migrazione da Office Communications Server 2007 R2, sia prima che dopo l'installazione di Lync 2013. Per ulteriori informazioni sull'interazione e la coesistenza dei client di Lync Server 2013 con versioni precedenti di client e server, vedere [Interoperabilità dei client in Lync 2013](lync-server-2013-client-interoperability-in-lync-2013.md).

## Dopo la migrazione dell'account ma prima dell'installazione di Lync 2013

Dopo la migrazione di un utente al server di Lync Server 2013, ma prima che vengano installati nuovi client, gli utenti di Office Communicator 2007 R2 possono continuare a utilizzare il client esistente in Lync Server 2013 per le funzionalità di presenza e messaggistica immediata, tuttavia le funzionalità per le conferenze non sono supportate.

## Dopo la migrazione dell'account e l'installazione di Lync 2013

Quando un utente di cui è stata eseguita la migrazione installa Lync 2013, viene installato anche il componente aggiuntivo per riunioni online per Lync 2013. Questo produce i seguenti effetti:

  - Tutte le riunioni pianificate a partire da questo momento si basano sul nuovo formato di riunione, che usa l'indirizzo https:// anziché quello legacy meet:// di Live Meeting.

  - In una distribuzione di Lync 2013 gestita dal reparto IT, l'amministratore può scegliere di disinstallare il Componente aggiuntivo per conferenze per Microsoft Office Outlook, che viene utilizzato per pianificare le riunioni basate su server e servizi di Live Meeting. Se però sono presenti utenti che desiderano continuare a pianificare riunioni con i servizi di Live Meeting, è possibile consentire la coesistenza di entrambi i componenti aggiuntivi.

## Riunioni con organizzazioni federate che utilizzano client precedenti

Gli utenti di organizzazioni federate che utilizzano Microsoft Office Communicator 2007 non possono partecipare a riunioni di Lync Server 2013 nell'organizzazione se tali riunioni sono bloccate dall'organizzatore. È necessario ripianificare queste riunioni in Lync Server 2013, in modo che quando accedono alla riunione tramite il nuovo URL https:// meeting URL, i partecipanti federati possano utilizzare Lync Web App.

