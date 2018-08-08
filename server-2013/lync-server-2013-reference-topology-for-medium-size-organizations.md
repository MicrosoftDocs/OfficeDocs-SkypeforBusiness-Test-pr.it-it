---
title: "Lync Server 2013: Topologia di rif. per organizzazioni di medie dimensioni"
TOCTitle: Topologia di riferimento per le organizzazioni di medie dimensioni
ms:assetid: 446b0914-2198-445e-ab6e-94802acebd5c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425939(v=OCS.15)
ms:contentKeyID: 49300362
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Topologia di riferimento per Lync Server 2013 per le organizzazioni di medie dimensioni

 

_**Ultima modifica dell'argomento:** 2013-10-07_

La topologia di riferimento con disponibilità elevata e un solo data center è specifica per un'organizzazione di piccole-medie dimensioni con un unico sito centrale. L'esatta topologia nel diagramma seguente è per un'organizzazione di 20.000 utenti.

**Topologia di riferimento per le organizzazioni di medie dimensioni**

![Diagramma della topologia di riferimento per un singolo data center](images/Gg425939.12b574fd-0b14-4563-a88c-3c8b0809bb90(OCS.15).jpg "Diagramma della topologia di riferimento per un singolo data center")

  - **Supporto di più utenti con l'aggiunta di ulteriori Front End Server.**     La topologia esatta in questo diagramma prevede tre Front End Server e pertanto supporta fino a 20.000 utenti. Se si dispone di un singolo sito centrale e di più utenti, è possibile semplicemente aggiungere Front End Server al pool. Il numero massimo di utenti per pool è 80.000, con dodici Front End Server.
    
    La topologia del singolo sito può tuttavia supportare un numero ancora maggiore di utenti, semplicemente aggiungendo un altro pool Front End al sito.

  - **Possibilità di aggiungere la funzionalità ripristino di emergenza.**    Per questa organizzazione la disponibilità elevata dei servizi di Lync Server è una funzionalità necessaria, a differenza del ripristino di emergenza. La disponibilità elevata viene fornita dal pool di Front End Server distribuiti nell'organizzazione.
    
    Per aggiungere la funzionalità di ripristino di emergenza, l'organizzazione può prendere in considerazione l'idea di stabilire un altro data center in cui aggiungere un altro pool Front End e di abbinare questo al pool Front End disponibile nel data center corrente. Se, in seguito, si verifica un'emergenza che riguarda il pool principale dell'organizzazione, gli amministratori possono eseguire il failover degli utenti nel pool di backup.

  - **Mirroring dei server back-end.**   Per potenziare la disponibilità elevata per le funzionalità di base dell'utente, l'organizzazione ha distribuito una coppia con mirroring di server back-end per ogni pool Front End. Si tratta di una nuova opzione della topologia per Lync Server 2013, che è facoltativa. È invece possibile scegliere di distribuire un singolo server back-end.

  - **Opzioni di database del Monitoring Server.**    Questa organizzazione ha distribuito la funzionalità di monitoraggio per garantire la qualità delle chiamate VoIP aziendale e delle conferenze A/V. Tale funzionalità viene distribuita in ogni Front End Server. Il database di monitoraggio viene collocato con i server back-end. Sono inoltre supportate topologie in cui il database di monitoraggio viene collocato in un server separato.

  - **Disponibilità elevata dei server perimetrali.**    In questa organizzazione di esempio con 20.000 utenti, per le prestazioni sarebbe sufficiente solo un server perimetrale. Per garantire disponibilità elevata è stato invece distribuito un pool di due server perimetrali.

  - **Opzioni di distribuzione del sito di succursale.**    Nell'organizzazione di questa topologia è distribuito VoIP aziendale come soluzione vocale. Nel Sito di succursale 1 non è presente un collegamento WAN resiliente con il sito centrale e pertanto è distribuito un Survivable Branch Appliance per la gestione di molte funzionalità di Lync Server in caso di errore del collegamento WAN con il sito centrale. Nel Sito di succursale 2 invece è presente un collegamento WAN resiliente e pertanto è necessario solo un gateway PSTN (Public Switched Telephone Network). Poiché il gateway PSTN distribuito supporta il bypass multimediale, non sono necessari Mediation Server nel Sito di succursale 2. Per informazioni dettagliate sulla scelta degli elementi da distribuire in un sito di succursale, vedere [Pianificazione della resilienza vocale del sito di succursale in Lync Server 2013](lync-server-2013-planning-for-branch-site-voice-resiliency.md) nella documentazione relativa alla pianificazione.

  - **Bilanciamento del carico DNS.**    Nel pool Front End e nel pool di server perimetrali è distribuito il bilanciamento del carico DNS per il traffico SIP. In questo modo si evita di dover utilizzare dispositivi di bilanciamento del carico hardware per i server perimetrali, riducendo notevolmente le attività di configurazione e manutenzione dei dispositivi di bilanciamento del carico hardware per gli altri pool, poiché i dispositivi di bilanciamento del carico hardware sono necessari solo per il traffico HTTP. Per informazioni dettagliate sul bilanciamento del carico DNS, vedere [Bilanciamento del carico DNS in Lync Server 2013](lync-server-2013-dns-load-balancing.md) nella documentazione relativa alla pianificazione.

  - **Distribuzione di messaggistica unificata di Exchange.** Questa topologia di riferimento include un server di Messaggistica unificata di Exchange che esegue Microsoft Exchange Server e non Lync Server.
    
    Per informazioni dettagliate su Messaggistica unificata di Exchange, vedere [Pianificazione dell'integrazione della messaggistica unificata di Exchange in Lync Server 2013](lync-server-2013-planning-for-exchange-unified-messaging-integration.md) e [Integrazione della messaggistica unificata di Exchange ospitata in Lync Server 2013](lync-server-2013-hosted-exchange-unified-messaging-integration.md) nella documentazione relativa alla pianificazione.

  - **Server Office Web Apps.** È consigliabile la distribuzione di un server Office Web Apps oppure di una server farm di Office Web Apps in tutte le organizzazioni che usano le conferenze Web. Il server Office Web Apps consente la presentazione di diapositive di PowerPoint nelle conferenze Web. Per ulteriori informazioni, vedere [Configurazione dell'integrazione con Office Web Apps Server e Lync Server 2013](lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md).

  - **Distribuzione di server perimetrali consigliata.**    Anche se l'utilizzo di un server perimetrale non è necessario, è consigliato per distribuzioni di qualsiasi dimensione. È possibile ottimizzare l'investimento con Lync Server distribuendo un server perimetrale in modo da offrire servizi agli utenti attualmente all'esterno dei firewall dell'organizzazione. Tra i vantaggi derivanti dall'utilizzo di server perimetrali sono inclusi i seguenti:
    
      - Gli utenti dell'organizzazione possono utilizzare le funzionalità di Lync Server anche se lavorano dalla propria abitazione o mentre sono in viaggio.
    
      - Gli utenti possono invitare utenti esterni a partecipare alle riunioni.
    
      - Se anche nell'organizzazione di un partner, un fornitore o un cliente viene usato Lync Server, è possibile costituire una *relazione federata* con tale organizzazione. In questo modo, la propria distribuzione di Lync Server riconoscerà gli utenti provenienti da tale organizzazione federata e ciò favorirà la collaborazione.
    
      - I propri utenti possono scambiare messaggi istantanei con gli utenti di servizi di messaggistica istantanea pubblici, inclusi uno, più o tutti i seguenti: Windows Live, AOL, Yahoo\! e Google Talk. Potrebbe essere necessaria una licenza separata per la connettività di messaggistica istantanea pubblica con questi servizi.
        
        > [!IMPORTANT]  
        > <ul><li><p>Dal 1 settembre 2012, la licenza di sottoscrizione utenti per la connettività di messaggistica istantanea pubblica di Microsoft Lync (“PIC USL”) non è più disponibile per l'acquisto per i nuovi contratti o quelli in fase di rinnovo. I clienti con licenze attive potranno continuare a eseguire la federazione con Yahoo! Messenger fino alla data di chiusura del servizio. Giugno 2014 è la data di fine servizio annunciata per Yahoo! e AOL. Per informazioni dettagliate, vedere <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Supporto della connettività per messaggistica istantanea pubblica in Lync Server 2013</a>.</p></li>        
        > <li><p>La licenza PIC USL è una licenza di sottoscrizione di tipo mensile per utente, richiesta per la federazione di Lync Server o Office Communications Server con Yahoo! Messenger. La capacità di Microsoft di fornire questo servizio dipende dal supporto offerto da Yahoo! e il contratto sottostante è in fase di chiusura.</p></li>        
        > <li><p>Oggi più che mai, Lync è un potente strumento per la connessione tra diverse organizzazioni e con utenti di tutto il mondo. La federazione con Windows Live Messenger non richiede ulteriori licenze per utente/dispositivo in aggiunta alla licenza CAL Standard per Lync. La federazione con Skype verrà aggiunta a questo elenco, consentendo agli utenti di Lync di raggiungere centinaia di milioni di persone tramite messaggistica istantanea e comunicazioni vocali.</p></li></ul>


  - **Possibilità di aggiungere server Director.**    Se questa organizzazione desidera aumentare la sicurezza da attacchi di tipo denial-of-service, può anche distribuire un pool di server Director. Un Server Director è un ruolo server separato facoltativo in Lync Server, che non ospita account utenti né fornisce informazioni sulla presenza o servizi di conferenza, ma che può essere utilizzato dal server dell'hop successivo interno in cui un server perimetrale esegue il routing del traffico SIP in ingresso per i server interni. Il Server Director preautentica le richieste in ingresso e le reindirizza al server o al pool principale dell'utente. La preautenticazione effettuata nel server Director consente di eliminare le richieste dagli account utente sconosciuti alla distribuzione. Un Server Director consente di isolare i Front End Server dal traffico dannoso, ad esempio da attacchi di tipo denial-of-service. Se la rete è sommersa da traffico esterno non valido in un attacco di questo tipo, il traffico viene reindirizzato al Server Director.

  - Uso consigliato di **System Center Operations Manager.**   È consigliabile monitorare l'integrità della distribuzione di Lync Server per garantire la disponibilità dei servizi agli utenti finali. È possibile monitorare Lync con il Management Pack di System Center Operations Manager per Lync che può essere scaricato gratuitamente dal sito Microsoft. Grazie al Management Pack di Lync è possibile ricevere avvisi in tempo reale quando si verificano problemi, eseguire transazioni sintetiche per testare le funzionalità di Lync end-to-end, ricevere rapporti sulla disponibilità dei servizi e così via. Ciò consente di risolvere tempestivamente i problemi relativi alla distribuzione prima che possano riscontrarli gli utenti finali.

