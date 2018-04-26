---
title: "Lync Server 2013: Definizione dei requisiti dell'organizzazione per il monitoraggio"
TOCTitle: Definizione dei requisiti dell'organizzazione per il monitoraggio
ms:assetid: d587ff04-9af6-4ac1-ad42-076e7a40ac75
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205284(v=OCS.15)
ms:contentKeyID: 49887777
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definizione dei requisiti dell'organizzazione per il monitoraggio in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-05_

Con la semplificazione della distribuzione e dell'installazione del monitoraggio in Microsoft Lync Server 2013, sono stati semplificati anche i processi di definizione dei requisiti dell'organizzazione per il monitoraggio. Ciò nonostante, sono ancora numerosi gli aspetti chiave di cui tenere conto prima di iniziare a installare e configurare Lync Server 2013:

**Tipi di dati da monitorare.** Lync Server 2013 consente di monitorare due tipi diversi di dati: i dati di registrazione dettagli chiamata e i dati della qualità percepita dagli utenti (QoE). La registrazione dettagli chiamata consente di tenere traccia dell'utilizzo di funzionalità di Lync Server come le chiamate telefoniche Voice over IP (VoIP), la messaggistica istantanea, i trasferimenti di file, le conferenze audio/video (A/V) e le sessioni di condivisione applicazioni. Queste informazioni consentono di conoscere quali funzionalità di Lync Server vengono o non vengono utilizzate e in quali momenti. I dati QoE consentono di registrare la qualità delle chiamate audio e video effettuate nell'organizzazione, fornendo informazioni quali il numero di pacchetti persi, il rumore di fondo e il livello di "instabilità" (differenze nei ritardi dei pacchetti).

Se si sceglie di abilitare il monitoraggio in Lync Server 2013, è possibile abilitare sia il monitoraggio di registrazione dettagli chiamata che il monitoraggio QoE oppure abilitare un tipo di monitoraggio lasciando l'altro disabilitato. Si supponga ad esempio che gli utenti utilizzino solo la messaggistica istantanea e i trasferimenti di file, senza effettuare chiamate audio o video. In tal caso potrebbe non essere necessario abilitare il monitoraggio QoE. Analogamente, Lync Server semplifica l'abilitazione e la disabilitazione del monitoraggio dopo la distribuzione di questa funzionalità. È ad esempio possibile scegliere di distribuire il monitoraggio lasciando inizialmente disabilitato il monitoraggio QoE. Se gli utenti iniziano a riscontrare problemi con le chiamate audio o video, è sempre possibile abilitare il monitoraggio QoE per individuare e risolvere tali problemi.

L'installazione del monitoraggio contemporaneamente all'installazione di Lync Server o dopo l'installazione di Lync Server non comporta particolari vantaggi o svantaggi. Considerare comunque che prima dell'installazione del monitoraggio è necessario selezionare un computer per ospitare l'archivio di monitoraggio back-end. Affinché tale computer possa essere utilizzato per il monitoraggio, deve essere installata e configurata anche una versione supportata di SQL Server. Se è già stato installato SQL Server in un computer pronto per l'utilizzo, sarà possibile installare il monitoraggio contemporaneamente all'installazione di Lync Server. Se invece non si dispone di un computer back-end pronto quando si procede all'installazione di Lync Server, installare il monitoraggio quando il computer back-end sarà pronto per l'utilizzo.

**Quando installare il monitoraggio.** Il monitoraggio può essere installato e configurato contemporaneamente all'installazione e alla configurazione di Lync Server 2013. La Distribuzione guidata di Lync Server consentirà di associare i pool Front End a un database di monitoraggio durante la configurazione. In alternativa, è possibile installare il monitoraggio dopo l'installazione di Lync Server utilizzando Generatore di topologie per associare i pool e i server Front End a un database di monitoraggio e pubblicando quindi la topologia modificata.

**Numero di database di monitoraggio back-end necessari.** Un singolo database di monitoraggio può supportare decine di migliaia di utenti. Per Microsoft Lync Server 2010 è stato calcolato che un database collocato utilizzato sia per il monitoraggio che per l'archiviazione è in grado di supportare 240.000 utenti. Un singolo database di monitoraggio può essere utilizzato inoltre da più pool Front End. Se si dispone di tre pool Front End nell'organizzazione, è possibile associarli tutti e tre allo stesso archivio back-end.

Questo significa semplicemente che per molte organizzazioni la capacità dei database non costituirà il fattore decisivo per determinare il numero di database di monitoraggio back-end necessari. È possibile invece che rivesta un'importanza maggiore la velocità di rete. Si supponga di disporre di tre pool Front End, di cui uno con una connessione di rete lenta. In tal caso sarà possibile utilizzare due database di monitoraggio: uno per la gestione dei due pool con una buona connessione di rete e un'altro per la gestione del pool con la connessione di rete più lenta.

Quando si pianifica l'infrastruttura di monitoraggio, è consigliabile inoltre considerare che Lync Server 2013 supporta l'utilizzo di database mirror. Il "mirroring del database" consente di disporre simultaneamente di due copie di un database, ognuna in un server diverso. Ogni volta che vengono scritti dati in un database primario, gli stessi dati vengono scritti anche nel database mirror. Se si verifica un errore o un problema di non disponibilità del database primario, è possibile eseguire il "failover" al database mirror utilizzando un semplice comando di Lync Server PowerShell, ad esempio:

    Invoke-CsDatabaseFailover -PoolFqdn atl-cs-001.litwareinc.com -DatabaseType "Monitoring" -NewPrincipal "Mirror"

Questo è importante ai fini della pianificazione semplicemente perché per utilizzare il mirroring è necessario raddoppiare il numero di database: oltre a ogni database primario, sarà necessario un secondo database da utilizzare come database mirror.

**Configurazioni di monitoraggio personalizzate per i siti di Lync Server.** Quando si installa Lync Server 2013, si installano anche raccolte globali di impostazioni di configurazione QoE e di registrazione dettagli chiamata. Queste raccolte globali consentono di applicare le stesse impostazioni QoE e di registrazione dettagli chiamata all'intera organizzazione. In molti casi questo è sufficiente, poiché spesso si desidera abilitare ad esempio il monitoraggio di registrazione dettagli chiamata per tutti gli utenti.

È tuttavia possibile che in alcuni casi si desideri applicare impostazioni diverse a siti diversi, ad esempio utilizzare il monitoraggio sia QoE che di registrazione dettagli chiamata nel sito di Redmond e solo di registrazione dettagli chiamata nel sito di Dublino. Analogamente, è possibile che si desideri mantenere i dati di monitoraggio per 60 giorni nel sito di Redmond, ma solo per 30 giorni nel sito di Dublino. Lync Server 2013 consente di creare raccolte separate di impostazioni di configurazione QoE e di registrazione dettagli chiamata nell'ambito del sito. In questo modo è possibile gestire ogni sito diversamente. Questo si applica sia all'abilitazione e alla disabilitazione del monitoraggio che alla configurazione di impostazioni di gestione come la durata di mantenimento dei dati.

Si noti che è possibile prendere questa decisione prima o dopo la distribuzione del monitoraggio. È ad esempio possibile distribuire il monitoraggio e quindi gestire l'intera organizzazione utilizzando le impostazioni globali. Se successivamente si cambia idea, è possibile creare una raccolta separata di impostazioni, ad esempio per il sito di Redmond, e quindi utilizzarle per la gestione del monitoraggio per Redmond. Le impostazioni applicate nell'ambito del sito hanno sempre la priorità su quelle applicate nell'ambito globale. Se si cambia di nuovo idea, è possibile semplicemente eliminare le impostazioni di configurazione applicate al sito di Redmond. Quando viene rimossa una raccolta di impostazioni di sito, viene applicata automaticamente al sito la raccolta globale di impostazioni.

