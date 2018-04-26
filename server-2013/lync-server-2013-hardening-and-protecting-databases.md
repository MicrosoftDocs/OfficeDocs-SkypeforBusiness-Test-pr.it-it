---
title: 'Lync Server 2013: Protezione avanzata e sicurezza dei database'
TOCTitle: Protezione avanzata e sicurezza dei database di Lync Server 2013
ms:assetid: 6953e721-3511-4235-b848-51bab093dc89
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn518330(v=OCS.15)
ms:contentKeyID: 60490915
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Protezione avanzata e sicurezza dei database di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-12-05_

Microsoft Lync Server 2013 dipende anche dai database di SQL Server per l'archiviazione delle informazioni sugli utenti, dello stato delle conferenze, dei dati di archiviazione e delle registrazioni dettagli chiamata (CDR). Per ottimizzare la disponibilità dei dati di Lync Server 2013 nei database back-end di Lync Server, è possibile partizionare i dati delle applicazioni in modo da migliorare la tolleranza di errore e semplificare la risoluzione dei problemi. Per raggiungere questi obiettivi, partizionare i dati delle applicazioni come indicato di seguito:

  - **Usare le procedure consigliate per il partizionamento del server**   Separare i file del sistema operativo, delle applicazioni e di programma dai file di dati.

  - **Archiviare i file di log delle transazioni e i file di database**   Archiviare separatamente questi file per aumentare la tolleranza di errore e ottimizzare il processo di ripristino, archiviandoli in un disco o un volume crittografato.

  - **Usare cluster di server**   Creare cluster dei server back-end per ottimizzare la disponibilità del sistema Lync Server 2013.

  - **Assicurarsi che tutti i backup dei dati siano crittografati e gestiti adeguatamente**   Perdere, eliminare o riporre nel posto sbagliato i supporti di backup può rappresentare una minaccia significativa per la sicurezza dei dati delle distribuzioni di Lync Server 2013

In qualsiasi server di Lync Server 2013, con l'eccezione del server Standard Edition, l'istanza di SQL Server Express (istanza RTCLOCAL) non è accessibile da remoto e non vengono create eccezioni del firewall locali, se non per SQL Server Express in un server Standard Edition. In un server Standard Edition, sia il database back-end che l'archivio di gestione centrale sono configurati in modo da consentire l'accesso remoto. Per migliorare la protezione dei database di SQL Server, è possibile eseguire le operazioni seguenti:

  - Personalizzare il firewall di SQL Server Express nei server Standard Edition, limitando l'ambito dei server con accesso remoto al database. Per impostazione predefinita, l'accesso remoto al database è consentito a qualsiasi indirizzo IP.

  - Usare Gestione configurazione SQL Server per specificare i protocolli, gli indirizzi IP e le porte per l'accesso remoto a SQL Server:
    
      - Lync Server 2013 usa il protocollo TCP/IP e supporta IP versione 4 (IPv4), ma non IP versione 6 (IPv6).
        

        > [!NOTE]
        > Lync Server 2013 può funzionare in una rete con un dual stack IP abilitato.

    
      - Lync Server 2013 supporta più indirizzi IP (schede di rete multihomed). È possibile impostare SQL Server per l'attesa di indirizzi IP specifici (singoli indirizzi o in base alla subnet) e per l'uso di protocolli specifici.
    
      - Lync Server 2013 supporta porte di SQL Server statiche e dinamiche.

  - Eseguire SQL Server su una porta statica (non predefinita) e non eseguire SQL Server Browser (in modo che non possa indicare la porta di attesa al client). Ciò richiede una configurazione personalizzata in ogni client di SQL Server, inclusi i server Front End, Monitoring Server, il server di archiviazione e le console di amministrazione (con Lync Server Management Shell, il Pannello di controllo di Lync Server o Generatore di topologie) e tutti gli altri server che eseguono database di Lync Server).


> [!NOTE]
> L'accesso ai database deve essere limitato ad amministratori di database attendibili. Un amministratore malintenzionato potrebbe inserire o modificare dati nei database per acquisire privilegi per i server di Lync Server 2013 oppure ottenere informazioni riservate dai servizi, anche se non gli è stato concesso l'accesso diretto o il controllo dei server di Lync Server 2013.



Per informazioni dettagliate sulle configurazioni personalizzate e la protezione avanzata dei database di SQL Server, vedere l'articolo del blog NextHop relativo all'uso di Lync Server 2010 con una configurazione di rete di SQL Server personalizzata all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=214008](http://go.microsoft.com/fwlink/p/?linkid=214008).


> [!NOTE]
> È anche possibile migliorare la protezione dei server per sistemi operativi e applicazioni, oltre a usare Criteri di gruppo per implementare blocchi di sicurezza nella distribuzione di Lync Server. Per informazioni dettagliate, vedere <A href="lync-server-2013-hardening-and-protecting-servers-and-applications.md">Protezione avanzata e sicurezza di server e applicazioni per Lync Server 2013</A>.


