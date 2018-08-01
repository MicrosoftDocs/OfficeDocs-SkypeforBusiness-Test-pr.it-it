---
title: 'Lync Server 2013: Topologia di riferimento per piccole organizzazioni'
TOCTitle: Topologia di riferimento per piccole organizzazioni
ms:assetid: 0453aeee-c41f-44e6-a6e0-aaace526ca08
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398095(v=OCS.15)
ms:contentKeyID: 49299533
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Topologia di riferimento per Lync Server 2013 nelle piccole organizzazioni

 

_**Ultima modifica dell'argomento:** 2013-10-07_

La topologia di riferimento per piccole organizzazioni illustra come distribuire una soluzione avanzata e altamente disponibile distribuendo solo tre server che eseguono Lync Server.

**Topologia di riferimento per piccole organizzazioni**

![Diagramma della topologia di riferimento per la distribuzione di tre server](images/Gg398095.25196d0d-dd07-451b-83ba-94c0ddf59030(OCS.15).jpg "Diagramma della topologia di riferimento per la distribuzione di tre server")

  - **Distribuzione di un coppia di server Standard Edition**   Questa organizzazione conta 4.000 utenti nel sito centrale e ha scelto di distribuire due server Standard Edition e di accoppiarli per abilitare la disponibilità elevata e il ripristino di emergenza. Ogni server ospita 2.000 utenti, ma nei due server vengono sincronizzate le informazioni relative a tutti gli utenti. Se uno dei server si blocca, un amministratore può eseguire il failover dei relativi utenti all'altro server senza creare eccessivi disagi. Per ulteriori informazioni sulle caratteristiche di disponibilità elevata e ripristino di emergenza in Lync Server 2013, vedere [Pianificazione per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md).

  - **È consigliata la distribuzione di un server perimetrale.**    Anche se non è necessario distribuire un server perimetrale per la messaggistica istantanea interna, la presenza e le conferenze, è consigliabile usarne uno persino per le distribuzioni di piccole dimensioni. È possibile massimizzare l'investimento fatto con Lync Server distribuendo un server perimetrale per fornire il servizio ai utenti che attualmente si trovano all'esterno dei firewall dell'organizzazione. I vantaggi sono i seguenti:
    
      - Gli utenti dell'organizzazione possono utilizzare le funzionalità di Lync Server anche se lavorano dalla propria abitazione o mentre sono in viaggio.
    
      - Gli utenti possono invitare utenti esterni a partecipare alle riunioni.
    
      - Se anche nell'organizzazione di un partner, un fornitore o un cliente viene usato Lync Server, è possibile costituire una *relazione federata* con tale organizzazione. In questo modo, la propria distribuzione di Lync Server riconoscerà gli utenti provenienti da tale organizzazione federata e ciò favorirà la collaborazione.
    
      - I propri utenti possono scambiare messaggi istantanei con gli utenti di servizi di messaggistica istantanea pubblici, inclusi uno, più o tutti i seguenti: Windows Live, AOL, Yahoo\! e Google Talk. Potrebbe essere necessaria una licenza separata per la connettività di messaggistica istantanea pubblica con questi servizi.
        
        > [!IMPORTANT]  
        > <ul><li><p>Dal 1 settembre 2012, la licenza di sottoscrizione utenti per la connettività di messaggistica istantanea pubblica di Microsoft Lync (“PIC USL”) non è più disponibile per l'acquisto per i nuovi contratti o quelli in fase di rinnovo. I clienti con licenze attive potranno continuare a eseguire la federazione con Yahoo! Messenger fino alla data di chiusura del servizio. Giugno 2014 è la data di fine servizio annunciata per Yahoo! e AOL. Per informazioni dettagliate, vedere <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Supporto della connettività per messaggistica istantanea pubblica in Lync Server 2013</a>.</p></li>        
        > <li><p>La licenza PIC USL è una licenza di sottoscrizione di tipo mensile per utente, richiesta per la federazione di Lync Server o Office Communications Server con Yahoo! Messenger. La capacità di Microsoft di fornire questo servizio dipende dal supporto offerto da Yahoo! e il contratto sottostante è in fase di chiusura.</p></li>        
        > <li><p>Oggi più che mai, Lync è un potente strumento per la connessione tra diverse organizzazioni e con utenti di tutto il mondo. La federazione con Windows Live Messenger non richiede ulteriori licenze per utente/dispositivo in aggiunta alla licenza CAL Standard per Lync. La federazione con Skype verrà aggiunta a questo elenco, consentendo agli utenti di Lync di raggiungere centinaia di milioni di persone tramite messaggistica istantanea e comunicazioni vocali.</p></li>        </ul>


  - **Funzionamento garantito per i siti di succursale.**    Questa organizzazione esegue il programma pilota per la caratteristica VoIP aziendale di Lync Server. Alcuni utenti usano Lync Server come unica soluzione vocale. Parte di questi utenti del programma pilota per VoIP aziendale si trova presso il sito di succursale. Il sito di succursale non dispone di un collegamento WAN (Wide Area Network) affidabile al sito centrale, pertanto al suo interno è stato distribuito un Survivable Branch Appliance. In questo modo, se il collegamento WAN non funziona, gli utenti presso il sito di succursale possono comunque effettuare e ricevere chiamate (sia all'interno dell'organizzazione che PSTN), disporre della funzionalità di segreteria telefonica e comunicare mediante messaggistica istantanea tra due parti. Gli utenti possono inoltre essere autenticati anche quando il collegamento WAN non è disponibile.

  - **Distribuzione di messaggistica unificata di Exchange.** Questa topologia di riferimento include un server di Messaggistica unificata di Exchange che esegue Microsoft Exchange Server e non Lync Server.
    
    Per informazioni dettagliate su Messaggistica unificata di Exchange, vedere [Pianificazione dell'integrazione della messaggistica unificata di Exchange in Lync Server 2013](lync-server-2013-planning-for-exchange-unified-messaging-integration.md) e [Integrazione della messaggistica unificata di Exchange ospitata in Lync Server 2013](lync-server-2013-hosted-exchange-unified-messaging-integration.md) nella documentazione relativa alla pianificazione.

  - **Server Office Web Apps.** È consigliabile la distribuzione di un server Office Web Apps oppure di una server farm di Office Web Apps in tutte le organizzazioni che usano le conferenze Web. Il server Office Web Apps consente la presentazione di diapositive di PowerPoint nelle conferenze Web. Per ulteriori informazioni, vedere [Configurazione dell'integrazione con Office Web Apps Server e Lync Server 2013](lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md).

