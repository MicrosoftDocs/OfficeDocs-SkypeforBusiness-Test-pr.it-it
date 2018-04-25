---
title: 'Lync Server 2013: Inizio del processo di pianificazione'
TOCTitle: Inizio del processo di pianificazione
ms:assetid: df3722b3-f859-49e1-b3ff-ee6863483731
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398986(v=OCS.15)
ms:contentKeyID: 49302197
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Inizio del processo di pianificazione per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-11-07_

Sebbene la pianificazione di una distribuzione di comunicazioni unificate locale possa sembrare complessa, in Lync Server sono disponibili due strumenti che possono rivelarsi utili:

  - **Lo Strumento di pianificazione** è una procedura guidata che presenta una serie di domande sull'organizzazione, sulle funzionalità di Lync Server che si desidera abilitare e sulle specifiche esigenze di pianificazione della capacità. Viene quindi creata una topologia di distribuzione consigliata in base alle risposte fornite e viene generato un diagramma di Microsoft Visio della distribuzione.

  - **Generatore di topologie** è un componente dell'installazione di Lync Server. Generatore di topologie consente di creare, modificare e pubblicare la topologia pianificata, nonché di verificarla prima di iniziare l'installazione dei server. Quando si installa Lync Server nei singoli server, durante il processo di installazione viene letta la topologia pubblicata e il programma di installazione distribuisce il server in base alle indicazioni nella topologia.

## Strumento di pianificazione di Lync Server

Strumento di pianificazione inserisce le risposte alle domande nello strumento e genera una topologia in base alle linee guida e alle procedure consigliate di Lync Server. Fornisce inoltre diverse visualizzazioni di una distribuzione in base alle risposte fornite. Mostra una visualizzazione globale dei siti, ossia con siti centrali e siti di succursale, e visualizzazioni dettagliate dei server e di altri componenti in ogni sito.

L'esecuzione di Strumento di pianificazione non impone alcuna specifica distribuzione né avvia alcun processo. In realtà se Strumento di pianificazione viene eseguito anche prima di aver definito un piano completo, è possibile identificare i tipi di domande che è necessario porsi per il processo di pianificazione.

È possibile eseguire più volte Strumento di pianificazione, fornire risposte diverse alle domande e confrontare i risultati. Se si ottiene un progetto quasi soddisfacente ma si desidera apportare modifiche, è possibile tornare in Strumento di pianificazione, caricare il progetto ed effettuare le modifiche. Ogni esecuzione completa di Strumento di pianificazione richiede circa 15 minuti di tempo.

Quando si è soddisfatti, è possibile utilizzare lo Strumento di pianificazione per creare un diagramma della distribuzione pianificata. È possibile utilizzare il diagramma durante la creazione della distribuzione in Generatore di topologie.


> [!NOTE]
> Lo strumento di pianificazione incluso in questa versione di Lync Server 2013 è una versione preliminare. Si noti che i numeri relativi alla pianificazione della capacità nello strumento di pianificazione sono preliminari e non sono supportati per la versione finale.



## Generatore di topologie di Lync Server

Dopo aver definito il piano di implementazione, utilizzare Generatore di topologie per avviare la distribuzione. Al termine, utilizzare Generatore di topologie per eseguire la convalida della topologia e quindi, se ha esito positivo, per pubblicarla. Quando viene pubblicata in Lync Server, la topologia viene inserita nell' archivio di gestione centrale, che viene creato in questa fase se non esiste già. Quando si installa Lync Server in ogni server della distribuzione, la topologia viene letta dall' archivio di gestione centrale e il server viene installato in base al relativo ruolo nella distribuzione.

In alternativa, se si conosce bene Lync Server e sono necessarie indicazioni meno prescrittive, è possibile ignorare Strumento di pianificazione e utilizzare le procedure guidate di Generatore di topologie per la progettazione iniziale della distribuzione e anche per i passaggi di convalida e pubblicazione.

L'utilizzo di Generatore di topologie per pianificare e pubblicare una topologia è un passaggio obbligatorio. Non è possibile ignorare Generatore di topologie e installare Lync Server nei singoli server della distribuzione. Ogni server deve leggere una topologia convalidata e pubblicata nell' archivio di gestione centrale.

## Processo generale di pianificazione

È consigliabile seguire il processo generale seguente per l'utilizzo della documentazione e dello Strumento di pianificazione per pianificare la distribuzione di Lync Server.

1.  Se si conoscono già le versioni precedenti di Lync Server, leggere [Nuove funzionalità in Lync Server 2013](lync-server-2013-new-features.md) per acquisire familiarità con le nuove funzionalità e i requisiti di Lync Server 2013.

2.  Leggere gli altri argomenti in questa sezione della documentazione: [Concetti di base sulla topologia che è necessario conoscere prima della pianificazione per Lync Server 2013](lync-server-2013-topology-basics-you-must-know-before-planning.md), [Topologie di riferimento in Lync Server 2013](lync-server-2013-reference-topologies.md), [Decisioni di pianificazione iniziali per Lync Server 2013](lync-server-2013-initial-planning-decisions.md) e [Client per Lync Server 2013](lync-server-2013-clients.md). Prendere nota delle decisioni relative alla pianificazione rappresentate in [Topologie di riferimento in Lync Server 2013](lync-server-2013-reference-topologies.md).

3.  Dopo aver acquisito una maggiore familiarità con le funzionalità di Lync Server e i tipi di domande a cui fornire una risposta, eseguire lo Strumento di pianificazione e visualizzare la topologia risultante insieme ai relativi dettagli. Assicurarsi che la topologia sia adatta ai requisiti specifici dell'organizzazione.

4.  Per ulteriori informazioni su specifici carichi di lavoro o funzionalità, consultare le sezioni appropriate di [Pianificazione per Lync Server 2013](lync-server-2013-planning.md).

5.  Eseguire nuovamente lo Strumento di pianificazione. È possibile iniziare con la distribuzione creata nel passaggio 3 e modificare i risultati oppure ricominciare daccapo.
    
    Se necessario, eseguire una terza volta lo Strumento di pianificazione e ripeterlo finché non si è soddisfati dell'output.

6.  Dopo aver completato il piano della topologia, utilizzare lo Strumento di pianificazione per creare e stampare un diagramma di Visio della topologia. È possibile utilizzare questa stampa durante l'utilizzo di Generatore di topologie per l'input della topologia.

7.  Prima di iniziare la distribuzione, leggere [Determinazione dei requisiti di sistema per Lync Server 2013](lync-server-2013-determining-your-system-requirements.md) e [Determinazione dei requisiti dell'infrastruttura per Lync Server 2013](lync-server-2013-determining-your-infrastructure-requirements.md) per acquisire familiarità con i prerequisiti e l'infrastruttura necessaria per Lync Server. Assicurarsi inoltre di aver letto tutte le sezioni di [Pianificazione per Lync Server 2013](lync-server-2013-planning.md) applicabili ai carichi di lavoro e alle funzionalità che si intende distribuire.

## Migrazione da versioni precedenti

Se si esegue la migrazione a Lync Server da una versione precedente, vedere la documentazione [Migrazione](migration.md) per istruzioni specifiche per la migrazione e la distribuzione.

