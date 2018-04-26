---
title: 'Lync Server 2013: Topologie supportate'
TOCTitle: Topologie supportate
ms:assetid: 3475d430-0394-491b-a09b-ba85bd62be70
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425833(v=OCS.15)
ms:contentKeyID: 49300132
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Topologie supportate in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-01-14_

Lync Server 2013 supporta la distribuzione di siti in locale in un'organizzazione e l'integrazione delle distribuzioni in locale con le distribuzioni di Skype for Business online, nota come distribuzione ibrida. In questo tipo di distribuzione alcuni utenti sono ospitati in locale, mentre altri online.

Per le distribuzioni in locale, Lync Server 2013 supporta la distribuzione di uno o più siti in cui è possibile implementare la scalabilità per soddisfare requisiti di disponibilità elevata e di posizione. È possibile strutturare tali siti e i relativi componenti in modo da soddisfare i requisiti di accesso e resilienza dell'organizzazione.

Caratteristiche di una distribuzione di Lync Server 2013 in locale:

  - La distribuzione deve includere almeno un sito centrale, noto anche come data center. In ogni sito centrale deve essere contenuto almeno un pool Enterprise Edition Front End o un server Standard Edition, costituiti come indicato di seguito:
    
      - Pool Enterprise Edition Front End, costituito da uno o più server front-end (in genere almeno due per la scalabilità) e un server back-end separato. Un pool Front End può includere un massimo di dodici server front-end. In presenza di più server front-end è richiesto il bilanciamento del carico. Per il traffico SIP è consigliato il bilanciamento del carico DNS, ma è supportato anche il bilanciamento del carico hardware. Se si usa il bilanciamento del carico DNS per il traffico SIP, è comunque necessario un dispositivo di bilanciamento del carico hardware per il traffico HTTP. È consigliabile usare il mirroring di SQL Server per garantire una disponibilità dei database elevata. Il database back-end richiede un'istanza separata, ma è possibile collocare insieme a esso il database di Archiviazione, il database di Monitoraggio, il database di Chat persistente e il database di Conformità Chat persistente. Lync Server 2013 supporta inoltre l'uso di un cluster condiviso per le condivisioni file della distribuzione. Per informazioni dettagliate sui requisiti di archiviazione dei database, vedere [Supporto per il software di database in Lync Server 2013](lync-server-2013-database-software-support.md). Per informazioni dettagliate sui requisiti di archiviazione dei file, vedere [Supporto dell'archiviazione di file in Lync Server 2013](lync-server-2013-file-storage-support.md).
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Se si posizionano database di Lync Server, è consigliabile valutare tutti i fattori che possono influire sulla disponibilità e sulle prestazioni. Per verificare le capacità di failover, è consigliabile testare tutti gli scenari di failover.</td>
        </tr>
        </tbody>
        </table>
    
      - Server Standard Edition, che include un database di SQL Server Express collocato.

  - Nella distribuzione possono inoltre essere presenti uno o più siti di succursale associati a un sito centrale.

Questa sezione descrive i siti e i componenti di una distribuzione di Lync Server 2013. Per informazioni dettagliate sul sito, sulla topologia e sulla pianificazione dei componenti di Lync Server 2013, vedere [Concetti di base sulla topologia che è necessario conoscere prima della pianificazione per Lync Server 2013](lync-server-2013-topology-basics-you-must-know-before-planning.md) e [Topologie di riferimento in Lync Server 2013](lync-server-2013-reference-topologies.md) nella documentazione relativa alla pianificazione. Per informazioni dettagliate sull'integrazione di componenti delle release precedenti, vedere [Percorsi di migrazione supportati e scenari di coesistenza in Lync Server 2013](lync-server-2013-supported-migration-paths-and-coexistence-scenarios.md).


> [!NOTE]
> I pool estesi non sono supportati per i ruoli server front-end, server perimetrale, Mediaton Server e server Director.



## Topologie e componenti di un sito centrale (in locale)

Una topologia di un sito centrale deve includere un solo pool Front End o un solo server Standard Edition, tuttavia ogni sito centrale può includere anche gli elementi seguenti:

  - Più pool Front End, che possono trovarsi nello stesso dominio o in domini diversi. Tutti i Front End Server di un pool Front End e il relativo server back-end devono tuttavia trovarsi nello stesso dominio.

  - Più server Standard Edition.

  - Il Server Office Web Apps, che viene utilizzato con Office Web Applications in Lync Server 2013 per gestire la condivisione e il rendering delle presentazioni di Microsoft PowerPoint.

  - Un server perimetrale o un pool di server perimetrali nella rete perimetrale, se si vuole che la distribuzione supporti i partner federati, la connettività per messaggistica istantanea pubblica, un gateway XMPP (Extensible Messaging and Presence Protocol, l'accesso degli utenti remoti, la partecipazione di utenti anonimi alle riunioni o Messaggistica unificata di Exchange. Non è possibile collocare altri ruoli del server con un server perimetrale. È consigliabile usare il bilanciamento del carico DNS, se appropriato, ma è supportato anche il bilanciamento del carico hardware. L'interfaccia perimetrale interna e quella esterna devono utilizzare lo stesso tipo di bilanciamento del carico. Non è possibile utilizzare il bilanciamento del carico DNS in un'interfaccia perimetrale e il bilanciamento del carico hardware nell'altra interfaccia perimetrale. Per informazioni dettagliate sui requisiti e il supporto del bilanciamento del carico, vedere [Pianificazione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-planning-for-external-user-access.md) nella documentazione relativa alla pianificazione e [Distribuzione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-deploying-external-user-access.md) nella documentazione relativa alla distribuzione.

  - Un Mediation Server o un pool di Mediation Server, se si desidera supportare il VoIP aziendale o le conferenze telefoniche con accesso esterno in un pool Front End nel sito centrale. A seconda della modalità di distribuzione del supporto del VoIP aziendale, è possibile collocare il Mediation Server in un pool Front End (impostazione predefinita) oppure distribuire un Mediation Server autonomo o un pool di Mediation Server. È possibile usare il bilanciamento del carico DNS, hardware o delle applicazioni (se appropriato) per distribuire il traffico proveniente dal peer gateway di un pool di Mediation Server, inclusi un gateway PSTN (Public Switched Telephone Network), un IP-PBX (IP-Public Branch Exchange) o un SBC (Session Border Controller) di un trunk SIP. Per informazioni dettagliate sulla pianificazione della topologia appropriata del Mediation Server, vedere [Linee guida per la distribuzione di Mediation Server in Lync Server 2013](lync-server-2013-deployment-guidelines-for-mediation-server.md) nella documentazione relativa alla pianificazione.

  - server Chat persistente, se si vuole che gli utenti partecipino a conversazioni basate su argomenti tra più utenti che permangono nel tempo. Per garantire una capacità maggiore e una migliore affidabilità, la topologia può includere più computer che eseguono server Chat persistente. Non è possibile collocare il server Chat persistente con alti ruoli server in un pool Enterprise. È invece possibile collocare il server Chat persistente in un server Standard Edition. Chat persistente richiede un database e, se si implementa la conformità Chat persistente, un database di Conformità Chat persistente. Tuttavia i database possono essere collocati insieme al database di Archiviazione, al database di Monitoraggio o nel server back-end di un pool Enterprise Edition Front End pool. Per informazioni dettagliate sulla pianificazione della topologia di server Chat persistente appropriata, vedere [Pianificazione del server Chat persistente in Lync Server 2013](lync-server-2013-planning-for-persistent-chat-server.md) nella documentazione relativa alla pianificazione.

  - Monitoraggio, se si desidera supportare la raccolta dati per la qualità audio/video percepita dagli utenti (QoE) e la registrazione dettagli chiamata per le conferenze audio/video e il VoIP aziendale nella distribuzione. Facoltativamente, è possibile installare Microsoft System Center Operations Manager (in precedenza Microsoft Operations Manager), in cui vengono usati i dati QoE e di registrazione dettagli chiamata di Monitoraggio per generare avvisi quasi in tempo reale con indicazione dello stato di affidabilità delle chiamate e della qualità multimediale. Quando viene distribuito, Monitoraggio viene collocato nei Front End Server o in un server Standard Edition. Monitoraggio richiede un database che può essere tuttavia collocato insieme al database di Archiviazione, al database di Chat persistente, al database di Conformità Chat persistente o nel server back-end di un pool Enterprise Edition Front End.

  - Archiviazione, se si vuole archiviare le comunicazioni di messaggistica istantanea e il contenuto delle riunioni (per motivi di conformità) nella distribuzione. Quando viene distribuita, Archiviazione viene collocata nei Front End Server o in un server Standard Edition. L'archivio di Archiviazione richiede la distribuzione di un database di Archiviazione o l'integrazione con l'archivio Exchange 2013. Se si usano entrambi, ovvero si segue la *modalità mista* , l'archiviazione Exchange 2013 viene utilizzata per archiviare i dati di archiviazione per gli utenti ospitati in Exchange 2013 e il database di archiviazione viene utilizzato per archiviare i dati di tutti gli altri utenti della distribuzione. Se è richiesto un database di archiviazione, questo può essere collocato nel database di Monitoraggio, nel database di Chat persistente, nel database di Conformità Chat persistente o nel server back-end di un pool Enterprise Edition Front End. Per informazioni dettagliate sulla pianificazione della topologia di archiviazione appropriata, vedere [Pianificazione dell'archiviazione in Lync Server 2013](lync-server-2013-planning-for-archiving.md) nella documentazione relativa alla pianificazione.

  - Un Director o un pool di server Director, se si desidera facilitare la resilienza e il reindirizzamento delle richieste utente di Lync Server 2013 al pool principale dell'utente, che può essere un pool Enterprise Edition Front End o un server Standard Edition. È consigliabile distribuire un Director o un pool di server Director in ogni sito centrale che supporta l'accesso degli utenti esterni e in ogni sito centrale in cui vengono distribuiti uno o più pool Front End. Ogni pool di server Director può includere un massimo di dieci Director. Non è possibile collocare un Director con altri ruoli del server. Per informazioni dettagliate sulla pianificazione della topologia di Director appropriata, vedere [Scenari per il server Director in Lync Server 2013](lync-server-2013-scenarios-for-the-director.md) nella documentazione relativa alla pianificazione.

  - Un proxy inverso, che non è un componente di Lync Server 2013 ma è necessario se si vuole supportare la condivisione di contenuto Web per gli utenti federati o per supportare il traffico di Mobility. Non è possibile collocare un server proxy inverso con ruoli del server di Lync Server 2013, ma è possibile implementare il supporto del proxy inverso per una distribuzione di Lync Server 2013 configurando il supporto di un server proxy inverso esistente nell'organizzazione usato per altre applicazioni. Per informazioni dettagliate sui server proxy inversi, vedere [Configurare server proxy inversi per Lync Server 2013](lync-server-2013-setting-up-reverse-proxy-servers.md) nella documentazione relativa alla distribuzione.


> [!NOTE]
> In Lync Server 2013, A/V Conferencing, Monitoraggio e Archiviazione vengono eseguiti sui Front End Server e non sono più ruoli di server separati.



Tutti i pool Front End e i server Standard Edition distribuiti nel sito centrale condividono gli elementi seguenti distribuiti per il sito centrale:

  - Director o pool di server Director

  - Mediation Server autonomo o pool di Mediation Server

  - Server Office Web Apps

  - Server perimetrale o pool di server perimetrali

  - Pool o server di Chat persistente

  - Monitoraggio

  - Archiviazione


> [!NOTE]
> È possibile implementare un server di Messaggistica unificata di Exchange con la distribuzione di Lync Server 2013 se si vuole supportare l'integrazione della messaggistica istantanea di Exchange 2013 ma non si tratta di un componente del sito Lync Server 2013.



Più siti centrali possono inoltre condividere gli elementi seguenti distribuiti in un sito centrale:

  - Mediation Server autonomo o pool di Mediation Server

  - Server perimetrale o pool di server perimetrali

  - Pool o server di Chat persistente

  - Archiviazione

  - Monitoraggio


> [!NOTE]
> È possibile implementare un server di Messaggistica unificata di Exchange con la distribuzione di Lync Server 2013. Il server può inoltre essere condiviso da più siti centrali, ma non è un componente del sito di Lync Server 2013.



Per informazioni dettagliate sui ruoli e sulle funzionalità del server di Lync Server 2013, vedere [Ruoli del server in Lync Server 2013](lync-server-2013-server-roles.md) nella documentazione relativa alla pianificazione.

Per un riepilogo del supporto della collocazione dei server di Lync Server 2013, vedere [Collocazione di server supportata in Lync Server 2013](lync-server-2013-supported-server-collocation.md).

Oltre ai ruoli e alle funzionalità del server descritti precedentemente in questa sezione, Lync Server 2013 supporta ulteriori componenti e opzioni, tra cui:

  - Firewall

  - Gateway PSTN (con la distribuzione di VoIP aziendale)

  - Server di Messaggistica unificata di Exchange

  - Bilanciamento del carico DNS

  - Dispositivi di bilanciamento del carico hardware

  - Database di SQL Server

  - Condivisioni file

Per informazioni dettagliate su tutti i componenti, le funzionalità e le opzioni di Lync Server 2013 vedere la documentazione relativa alla pianificazione.

## Topologie e componenti di un sito di succursale (in locale)

Un sito di succursale è associato a un sito centrale e ogni Survivable Branch Appliance di un sito di succursale è associato a un pool Enterprise Edition Front End o a un server Standard Edition del sito centrale associato. Poiché i siti di succursale dipendono dal sito centrale per la maggior parte delle funzionalità, i componenti di un sito di succursale includono solo gli elementi seguenti:

  - Un Survivable Branch Appliance, che combina un gateway PSTN (Public Switched Telephone Network) con alcune funzionalità di Lync Server. Il Mediation Server può essere collocato con l'istanza della funzione di registrazione nel Survivable Branch Appliance ed è possibile distribuire un Mediation Server autonomo o un pool di Mediation Server.

  - Un Survivable Branch Server, ovvero un server che esegue Windows Server in cui è installato il software della funzione di registrazione e dei Mediation Server di Lync Server 2013.

  - Un gateway PSTN autonomo (che non fa parte del Survivable Branch Appliance) e un Mediation Server autonomo.

I requisiti per i Survivable Branch Server solo gli stessi previsti per qualsiasi ruolo del server di Lync Server 2013.

