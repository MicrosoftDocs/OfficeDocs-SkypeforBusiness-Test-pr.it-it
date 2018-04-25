---
title: 'Lync Server 2013: integrazione con Microsoft Exchange Server 2013'
TOCTitle: Integrazione di Lync Server 2013 ed Exchange Server 2013
ms:assetid: 795dc1c6-524f-4012-8b66-103b55198044
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688098(v=OCS.15)
ms:contentKeyID: 49887614
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Integrazione di Microsoft Lync Server 2013 e Microsoft Exchange Server 2013

 

_**Ultima modifica dell'argomento:** 2014-07-09_

Exchange e Lync Server vantano una lunga storia di integrazione e compatibilità. L'integrazione è particolarmente visibile attraverso le rispettive applicazioni client. Ad esempio, le informazioni sulla presenza di Lync possono essere riportate su Microsoft Outlook; analogamente, Lync può servirsi del calendario di Outlook per aggiornare automaticamente le informazioni sulla presenza. (Ad esempio, Lync può impostare lo stato su Non disponibile ogni volta che nel calendario è pianificato un appuntamento). Benché non sia necessario eseguire Exchange per eseguire Lync Server (o viceversa), l'utilizzo dei due prodotti congiuntamente offre notevoli vantaggi.

Ciò è particolarmente vero nelle versioni Microsoft Lync Server 2013 e Microsoft Exchange Server 2013. In aggiunta a caratteristiche quali messaggistica unificata, messaggistica istantanea presenza, che possono essere trovate in Microsoft Exchange Server 2010 e Microsoft Lync Server 2010, nella versione 2013 dei prodotti server sono incluse svariate nuove funzionalità, tra cui:

  - **Integrazione dell'archiviazione di Lync** . In Lync Server 2013, gli amministratori possono archiviare in SQL Server le trascrizioni dei messaggi istantanei e delle conferenze Web, analogamente al modo in cui le trascrizioni sono archiviate in Lync Server 2010. Alternativamente, gli amministratori possono scegliere di archiviare le trascrizioni in Exchange 2013, archiviandole nelle casette postali degli utenti singoli, analogamente alle modalità di archiviazione di Exchange. In questo modo, si ottiene un archivio singolo per tutte le comunicazioni elettroniche (di Exchange e Lync Server), che semplifica la ricerca e il recupero delle comunicazioni archiviate, quando se ne ha bisogno.

  - **Archivio unificato per i contatti** . In Lync Server 2010, gli utenti hanno elenchi di contatti separati per Outlook e Lync; per avere gli stessi contatti in entrambi i prodotti, è necessario mantenere elenchi dei contatti duplicati, uno per Outlook e uno per Lync. Con Lync Server 2013, è possibile archiviare i contatti degli utenti in Exchange 2013 e nell'archivio unificato per i contatti. Un archivio unificato consente agli utenti di avere un solo insieme di contatti, disponibile in Lync 2013, Outlook 2013 e Outlook Web Access 2013.

  - **Pianificazione di riunioni Lync da OWA** . Con l'integrazione di Lync Server 2013 e Exchange 2013 gli utenti possono pianificare riunioni Lync da Outlook Web Access 2013.

  - **Immagini ad alta risoluzione** . Lync 2010 consente di visualizzare un'immagine piccola per i propri contatti, poiché queste immagini sono archiviate in Active Directory, che impone una limitazione delle dimensioni delle immagini archiviate pari a 48 pixel per 48 pixel. Con Lync Server 2013, tuttavia, le immagini possono essere archiviate in Microsoft Exchange, che consente di visualizzare immagini ad alta risoluzione (648 pixel per 648 pixel). In parallelo, Lync 2013 è stato aggiornato per consentire la visualizzazione delle immagini ad alta risoluzione.

Queste nuove caratteristiche richiedono l'utilizzo di Lync Server 2013 e Exchange 2013. Inoltre, gli utenti che desiderano sfruttare appieno le nuove funzionalità, devono disporre di account su Lync Server 2013 e Exchange 2013, e devono utilizzare la versione più recente del software del client (ad esempio, Lync 2013). Ad esempio, l'archivio unificato per i contatti non è disponibile per quegli utenti ospitati su Lync Server 2010; analogamente, le immagini ad alta risoluzione non possono essere visualizzate in Lync 2010.

Questa documentazione fornisce informazioni sull'integrazione di Lync Server 2013 e Exchange 2013. e istruzioni dettagliate per l'abilitazione di nuove caratteristiche, tra cui l'integrazione dell'archiviazione e l'archivio unificato per i contatti. La documentazione non tratta della configurazione iniziale dei due prodotti. Per informazioni dettagliate sulla distribuzione di Lync Server 2013, vedere il Tech Center di Lync Server 2013 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=246127\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=246127%26clcid=0x410). Per informazioni dettagliate sulla distribuzione di Exchange 2013, vedere il Tech Center di Exchange 2013 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268528\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268528%26clcid=0x410).

## Argomenti della sezione

[Prerequisiti per l'integrazione di Microsoft Lync Server 2013 e Microsoft Exchange Server 2013](lync-server-2013-prerequisites-for-integrating-with-exchange-server-2013.md)

[Configurazione delle applicazioni partner in Microsoft Lync Server 2013 e Microsoft Exchange Server 2013](lync-server-2013-configuring-partner-applications-in-lync-server-2013-and-exchange-server-2013.md)

[Configurazione di Microsoft Lync Server 2013 per l'utilizzo dell'archiviazione di Microsoft Exchange Server 2013](configuring-lync-server-2013-to-use-microsoft-exchange-server-2013-archiving.md)

[Configurazione di Microsoft SharePoint Server 2013 per la ricerca di dati archiviati di Microsoft Lync Server 2013](lync-server-2013-configuring-microsoft-sharepoint-server-2013-to-search-for-archived-lync-server-2013-data.md)

[Configurazione di Microsoft Lync Server 2013 per l'utilizzo dell'archivio contatti unificato](lync-server-2013-configuring-lync-server-to-use-the-unified-contact-store.md)

[Configurazione dell'utilizzo delle foto ad alta risoluzione in Microsoft Lync Server 2013](lync-server-2013-configuring-the-use-of-high-resolution-photos.md)

[Configurazione della messaggistica unificata di Microsoft Exchange Server 2013 per la segreteria telefonica di Microsoft Lync Server 2013](lync-server-2013-configuring-microsoft-exchange-server-2013-unified-messaging-for-lync-server-2013-voice-mail.md)

[Integrazione di Microsoft Lync Server 2013 e Microsoft Outlook Web App 2013](lync-server-2013-integrating-lync-server-and-outlook-web-app-2013.md)

