---
title: "Lync Server 2013: Topolog. di rif. per grandi organizzaz. con più data center"
TOCTitle: Topologia di riferimento per organizzazioni di grandi dimensioni con più data center
ms:assetid: 9a6aeae6-629b-49e6-9804-7ef369d7c3dc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398797(v=OCS.15)
ms:contentKeyID: 49301429
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Topologia di riferimento per Lync Server 2013 per organizzazioni di grandi dimensioni con più data center

 

_**Ultima modifica dell'argomento:** 2012-10-22_

La topologia di riferimento per grandi organizzazioni con più data center è indicata per un'organizzazione di qualsiasi dimensione con più siti centrali. L'esatta topologia nella figura seguente è adeguata per un'organizzazione di 50.000 utenti, con 20.000 utenti nel sito centrale A e 20.000 nel sito centrale B e un totale di 10.000 nel sito centrale C e succursali. Il tipo di topologia illustrato in questa figura può essere adattato a organizzazioni con qualsiasi numero di utenti.

Oltre alla disponibilità elevata fornita dai pool di Front End Server, questa topologia aggiunge il supporto per il ripristino di emergenza. I pool Front End nei siti centrali A e B sono abbinati. Se uno dei due diventa inattivo, l'amministratore può passare i servizi per gli utenti interessati al pool abbinato nel sito non interessato dal problema.

Questa topologia è illustrata in più diagrammi, con una prima panoramica seguita da visualizzazioni dettagliate dei siti centrali.

**Panoramica della topologia di riferimento per grandi organizzazioni con più data center**

![Topologia di riferimento per più data center](images/Gg398797.471e1ce9-be11-44b9-9f4a-59e0551b7b30(OCS.15).jpg "Topologia di riferimento per più data center")

**Topologia di riferimento per grandi organizzazioni: visualizzazione dettagliata del sito centrale A**

![Pianificazione delle topologie di riferimento A](images/Gg398797.dab33f19-e77b-42da-9047-858fb9851264(OCS.15).jpg "Pianificazione delle topologie di riferimento A")

**Topologia di riferimento per grandi organizzazioni: visualizzazione dettagliata del sito centrale B**

![Pianificazione delle topologie di riferimento B](images/Gg398797.5ccaf1d4-bd53-4cb7-96fe-723147334e7f(OCS.15).jpg "Pianificazione delle topologie di riferimento B")

**Topologia di riferimento per grandi organizzazioni: visualizzazione dettagliata del sito centrale C**

![Pianificazione delle topologie di riferimento C](images/Gg398797.7238ca40-340c-491f-b497-ddc2665dadb6(OCS.15).jpg "Pianificazione delle topologie di riferimento C")

  - I **pool Front End sono abbinati per consentire il ripristino di emergenza.**   I pool Front End presso il sito A e il sito B sono abbinati tra loro per supportare il ripristino di emergenza. Se si verifica un malfunzionamento nel pool di uno dei siti, l'amministratore può provvedere al failover con il pool Front End abbinato nell'altro sito con una minima interruzione dei servizi per gli utenti. Ognuno di questi due pool Front End è costituito da sei server, ovvero una quantità sufficiente per tutti i 40.000 utenti in entrambi i pool in caso di failover. Per ulteriori informazioni, vedere [Pianificazione per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md).

  - I **server back-end sono in mirroring**   Per fornire maggiore disponibilità elevata per le funzionalità di base, l'organizzazione ha distribuito una coppia con mirroring di server back-end per ogni pool Front End. Si tratta di una topologia facoltativa ed è possibile scegliere di distribuire invece un singolo server back-end.

  - **Uso di un server Standard Edition nel sito della succursale.**   L'organizzazione considera il sito C come una succursale perché ha solo 600 dipendenti. Tuttavia, gli utenti effettuano numerose conferenze A/V. Se è stata effettuata la distribuzione in Lync Server come succursale, i contenuti multimediali di queste conferenze attraversano la rete WAN verso e da un sito centrale in cui è distribuito un Front End Server. Per evitare questo potenziale carico della larghezza di banda, in questo sito è stata installata una coppia di server Standard Edition che ospita le conferenze. Poiché i server Standard Edition sono installati in sede, Lync Server per definizione la considera un sito centrale e come tale viene trattata in Generatore di topologie e nel Strumento di pianificazione.
    
    Un solo server Standard Edition è già sufficiente per garantire prestazioni soddisfacenti in questo caso, tuttavia l'organizzazione ha distribuito due server abbinati per offrire disponibilità elevata in caso di malfunzionamento di uno dei due.
    
    Sebbene il sito C sia considerato un sito centrale, non è necessario distribuirvi server perimetrali. In questo esempio, il sito C utilizzerà i server perimetrali distribuiti nel sito A.

  - **Monitoraggio e archiviazione**   L'organizzazione ha distribuito i servizi di monitoraggio e archiviazione. Monitoraggio e archiviazione vengono eseguiti su ogni Front End Server. I database di queste funzionalità possono essere collocati nel database back-end o in server distinti. L'organizzazione ha collocato questi database su un server distinto dai server back-end, nel sito centrale B. I database qui ricevono i dati di monitoraggio e archiviazione dai Front End Server di tutti i siti.

  - **Opzioni di distribuzione del sito di succursale.**   L'organizzazione dispone in effetti di 50 succursali di cui solo 3 sono indicate nel diagramma dettagliato. I siti di succursale 1 e 3 non dispongono di un collegamento WAN resiliente al sito centrale, pertanto vi sono stati distribuiti Survivable Branch Appliance per fornire i servizi di telefonia in caso di interruzione del collegamento WAN al sito centrale. Il sito di succursale 2, tuttavia, dispone di un collegamento WAN resiliente, pertanto è necessario soltanto un gateway PSTN. Il gateway PSTN distribuito in questa posizione supporta il bypass multimediale, dunque nel sito di succursale B non è necessario un Mediation Server. Per informazioni dettagliate sulla scelta degli elementi da installare in un sito di succursale, vedere [Pianificazione della resilienza di VoIP aziendale in Lync Server 2013](lync-server-2013-planning-for-enterprise-voice-resiliency.md) nella documentazione sulla pianificazione.

  - **Trunking SIP e Mediation Server.**   Si noti che nel sito centrale B il Mediation Server non è collocato con i Front End Server. Il motivo è che nei siti che utilizzano il trunking SIP è preferibile l'utilizzo di un Mediation Server autonomo. Nella maggior parte degli altri casi, è consigliabile collocare il Mediation Server con il Front End Server. Per informazioni dettagliate sulle topologie di Mediation Server, vedere [Componenti e topologie per Mediation Server in Lync Server 2013](lync-server-2013-components-and-topologies-for-mediation-server.md) nella documentazione sulla pianificazione.

  - **Distribuzione della funzionalità di chat persistente.**   L'organizzazione ha distribuito i server necessari per abilitare la chat persistente. Sono stati distribuiti più Front End Server di chat persistente per gestire il carico per il numero di utenti nel pool e garantire disponibilità elevata. È stata anche distribuita la conformità per la chat persistente e l'archivio della chat persistente e l'archivio di conformità della funzionalità sono stati distribuiti su server separati. Questi archivi possono essere collocati nello stesso server e anche nel server back-end, ma questa organizzazione ha scelto di separarli per offrire prestazioni migliori.

  - **Bilanciamento del carico DNS.**   Nel pool Front End e nel pool di server perimetrali è stato distribuito il bilanciamento del carico DNS. In questo modo non è necessario ricorrere a dispositivi di bilanciamento del carico hardware per l'interfaccia interna dei server perimetrali ed è possibile ridurre drasticamente il tempo da dedicare alla configurazione e alla manutenzione dei dispositivi di bilanciamento del carico hardware per gli altri pool, in quanto tali dispositivi sono necessari solo per il traffico HTTP. Per informazioni dettagliate sul bilanciamento del carico DNS, vedere [Bilanciamento del carico DNS in Lync Server 2013](lync-server-2013-dns-load-balancing.md) nella documentazione sulla pianificazione.

  - **Distribuzione della messaggistica unificata di Exchange.**   Lync Server funziona sia con le distribuzioni *locali* che con le distribuzioni *ospitate* della messaggistica unificata di Exchange. Il sito centrale A include un server di Messaggistica unificata di Exchange che esegue Microsoft Exchange Server, non Lync Server. La funzionalità Messaggistica unificata di Exchange per Lync Server viene eseguita nel pool Front End.
    
    Il sito centrale B utilizza servizi di Exchange ospitati, dunque è ospitata anche la funzionalità server di messaggistica unificata di Exchange.
    
    Per informazioni dettagliate su Messaggistica unificata di Exchange, vedere [Pianificazione dell'integrazione della messaggistica unificata di Exchange in Lync Server 2013](lync-server-2013-planning-for-exchange-unified-messaging-integration.md) e [Integrazione della messaggistica unificata di Exchange ospitata in Lync Server 2013](lync-server-2013-hosted-exchange-unified-messaging-integration.md) nella documentazione relativa alla pianificazione.

  - **Server Office Web Apps.**   È consigliabile distribuire un server Office Web Apps o una farm di server Office Web Apps in ogni organizzazione che usa Web Conferencing. È possibile distribuire una singola farm di server Office Web Apps in un sito che serva il traffico di tutti i siti oppure distribuirla in ogni sito. Il server Office Web Apps consente la presentazione di diapositive di PowerPoint nelle conferenze Web. Per ulteriori informazioni, vedere [Configurazione dell'integrazione con Office Web Apps Server e Lync Server 2013](lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md).

  - **Possibilità di aggiungere server Director.**   Per migliorare la sicurezza contro attacchi di tipo Denial of Service, le organizzazioni possono anche distribuire un pool di server Director. Un Server Director è un ruolo server facoltativo distinto in Lync Server che non ospita account utente né fornisce servizi di presenza o conferenza. Esso funge da server hop successivo interno a cui un server perimetrale instrada il traffico SIP in ingresso destinato ai server interni. Il Server Director esegue la preautenticazione delle richieste in ingresso e le reindirizza al pool principale o al server dell'utente. La preautenticazione nel server Director consente di eliminare le richieste di account utente sconosciuti nella distribuzione . Un Server Director agevola l'isolamento dei Front End Server da traffico dannoso come gli attacchi di tipo DoS (Denial of Service). Se la rete subisce questo tipo di attacco ricevendo una quantità notevole di traffico esterno non valido, tale traffico termina nel Server Director.

  - **System Center Operations Manager è distribuito.**   È consigliabile monitorare l'integrità della distribuzione di Lync Server per assicurare la disponibilità del servizio agli utenti finali. È possibile monitorare Lync con System Center Operations Manager Management Pack per Lync reso disponibile come download gratuito da Microsoft. Con Lync Management Pack, è possibile reagire in modo tempestivo agli avvisi in tempo reale quando si verificano problemi, eseguire transazioni sintetiche per testare le funzionalità Lync end-to-end, ottenere rapporto sulla disponibilità dei servizi e così via.  Ciò consente di reagire in modo proattivo ai problemi della distribuzione prima che siano rilevati dagli utenti finali.
    
    L'organizzazione ha distribuito un server System Center Operations Manager in ogni sito centrale.

