---
title: Configurare il gateway XMPP in Lync Server 2013
TOCTitle: Configurare il gateway XMPP in Lync Server 2013
ms:assetid: 00777a34-cc36-4992-9459-08c14543ef6b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ687953(v=OCS.15)
ms:contentKeyID: 49887423
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare il gateway XMPP in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-19_

Quando si configurano criteri per il supporto dei partner federati del protocollo XMPP (Extensible Messaging and Presence Protocol), i criteri vengono applicati agli utenti dei domini federati XMPP, ma non agli utenti dei provider di servizi di messaggistica immediata SIP (Session Initiation Protocol), ad esempio Windows Live, oppure dei domini federati SIP. Configurare un partner federato XMPP per ogni dominio federato XMPP a cui si desidera che gli utenti possano aggiungere contatti e con cui possano comunicare. Dopo l'applicazione dei criteri, le attività aggiuntive includono la configurazione dei certificati del gateway XMPP, la distribuzione del gateway XMPP di Lync Server 2013 e infine l'aggiornamento dei record DNS per il gateway XMPP.

## Configurare i certificati del gateway XMPP nel server perimetrale Lync Server 2013

1.  Nel server perimetrale fare clic su **Riesegui** nella Distribuzione guidata accanto a **Passaggio 3: Richiesta, installazione o assegnazione dei certificati** .
    
    > [!tip]  
    > Se si distribuisce il server perimetrale per la prima volta, sarà disponibile il pulsante Esegui anziché Riesegui.

2.  Nella pagina **Attività certificato disponibili** fare clic su **Crea una nuova richiesta di certificato** .

3.  Nella pagina **Richiesta di certificato** fare clic su **Certificato perimetro esterno** .

4.  Nella pagina **Richieste immediate o ritardate** selezionare la casella di controllo **Prepara la richiesta per l'invio posticipato** .

5.  Nella pagina **File richiesta di certificato** digitare il percorso completo e il nome del file in cui si desidera salvare la richiesta, ad esempio c:\\cert\_perimetro\_esterno.cer.

6.  Nella pagina **Specifica modello di certificato alternativo** , per utilizzare un modello diverso dal modello Web Server predefinito selezionare la casella di controllo **Utilizza modello di certificato alternativo per l'autorità di certificazione selezionata** .

7.  Nella pagina **Impostazioni nome e sicurezza** eseguire le operazioni seguenti:
    
    1.  In **Nome descrittivo** digitare un nome visualizzato per il certificato.
    
    2.  In **Lunghezza bit** specificare la lunghezza in bit (in genere il valore predefinito 2048).
    
    3.  Verificare che la casella di controllo **Contrassegna come esportabile la chiave di certificato privata** sia selezionata.

8.  Nella pagina **Informazioni sull'organizzazione** digitare il nome dell'organizzazione e dell'unità organizzativa, ad esempio una divisione o un reparto.

9.  Nella pagina **Dati geografici** specificare le informazioni sulla posizione.

10. Nella pagina **Nome soggetto / Nomi soggetto alternativi** verranno visualizzate le informazioni compilate automaticamente dalla procedura guidata. Se sono necessari ulteriori nomi alternativi soggetto, specificarli nei prossimi due passaggi.

11. Nella pagina **Impostazione del dominio SIP su nomi alternativi soggetto (SAN)** selezionare la casella di controllo del dominio per aggiungere una voce sip.\<dominiosip\> all'elenco dei nomi alternativi del soggetto.

12. Nella pagina **Configura nomi alternativi soggetto aggiuntivi** specificare eventuali nomi alternativi del soggetto aggiuntivi necessari.
    
    > [!tip]  
    > Se è installato il proxy XMPP, per impostazione predefinita le voci SAN vengono popolate con il nome di dominio, ad esempio contoso.com. Se sono necessarie ulteriori voci, aggiungerle in questo passaggio.

13. Nella pagina **Riepilogo richiesta** esaminare le informazioni sul certificato da utilizzare per generare la richiesta.

14. Al termine dell'esecuzione dei comandi è possibile fare clic su **Visualizza log** o su **Avanti** per continuare.

15. Nella pagina **File richiesta di certificato** è possibile visualizzare il file richiesta di firma del certificato (CSR) generato facendo clic su Visualizza oppure uscire dalla Configurazione guidata certificati facendo clic su **Fine** .

16. Copiare il file di richiesta e inviarlo all'autorità di certificazione pubblica.

17. Dopo aver ricevuto, importato e assegnato il certificato pubblico, è necessario arrestare e riavviare i servizi del server perimetrale. A tale scopo, digitare quanto segue nella console di gestione di Lync Server:
    
    ```
    Stop-CsWindowsService
    ```
    ```
    Start-CsWindowsService
    ```

## Configurare un nuovo gateway XMPP di Lync Server 2013

1.  Aprire il Pannello di controllo di Lync Server.

2.  Sulla barra di spostamento sinistra fare clic su **Federazione e accesso esterno** e quindi su **Partner federati XMPP** .

3.  Per creare una nuova configurazione, fare clic su **Nuovo** .

4.  Definire le impostazioni seguenti:

5.  **Dominio primario**     (Obbligatorio) Il dominio primario è il dominio di base del partner XMPP. È ad esempio possibile immettere **fabrikam.com** come nome di dominio del partner XMPP. Questa è una voce obbligatoria.

6.  **Descrizione**    La descrizione è costituita da note o altre informazioni di identificazione di questa specifica configurazione. Questa voce è facoltativa.

7.  **Domini aggiuntivi**    I domini aggiuntivi sono domini che fanno parte del dominio del partner XMPP che devono essere inclusi come parte delle comunicazioni XMPP consentite. Se ad esempio il dominio primario è **fabrikam.com**, sarà necessario elencare tutti gli altri domini inclusi in fabrikam.com con cui si comunicherà mediante XMPP.

8.  **Tipo di partner**    L'impostazione **Tipo di partner** è obbligatoria. È necessario selezionare una delle opzioni seguenti per descrivere e applicare i contatti che possono essere aggiunti. È possibile selezionare le opzioni seguenti:
    
      - **Federato**    Un tipo di partner **Federato** rappresenta un livello di trust elevato tra la distribuzione di Lync Server e il partner XMPP. Questo tipo di partner è consigliato per la federazione con i server XMPP della stessa azienda o in scenari di rapporti professionali consolidati. I contatti XMPP nei partner federati possono eseguire le operazioni seguenti:
        
        1.  Aggiungere contatti Lync e visualizzare le relative informazioni sulla presenza senza autorizzazione esplicita da parte dell'utente Lync.
        
        2.  Inviare messaggi istantanei a contatti Lync indipendentemente dal fatto che siano stati aggiunti nell'elenco contatti dell'utente Lync.
        
        3.  Visualizzare le note sullo stato di un utente Lync.
    
      - **Verificato pubblico**    Un partner **Verificato pubblico** è un provider XMPP pubblico considerato attendibile per la verifica dell'identità dei relativi utenti. I contatti XMPP nelle reti di tipo Verificato pubblico possono aggiungere contatti Lync, visualizzare le relative informazioni sulla presenza e inviare loro messaggi istantanei senza autorizzazione esplicita degli utenti Lync. I contatti XMPP nelle reti di tipo Verificato pubblico non visualizzano mai le note sullo stato di un utente Lync. Questa impostazione non è consigliata.
    
      - **Non verificato pubblico**    Un partner **Non verificato pubblico** è un provider XMPP pubblico non considerato attendibile per la verifica dell'identità dei relativi utenti. Gli utenti XMPP delle reti di tipo Non verificato pubblico non possono comunicare con gli utenti Lync a meno che non siano stati esplicitamente autorizzati dall'utente Lync con l'aggiunta nell'elenco contatti. Gli utenti XMPP nelle reti di tipo Non verificato pubblico non visualizzano mai le note sullo stato degli utenti Lync. Questa impostazione è consigliata per le federazioni con provider XMPP pubblici come Google Talk.

9.  **Tipo di connessione** Consente di definire le diverse regole e impostazioni di dialback.
    
      - **Negoziazione TLS** : consente di definire le regole di negoziazione TLS. Un servizio XMPP può rendere TLS obbligatorio, può rendere TLS facoltativo oppure è possibile definire TLS come non supportato. Se si sceglie Facoltativo, la decisione relativa all'obbligatorietà per la negoziazione verrà affidata al servizio XMPP. Per visualizzare tutte le impostazioni possibili e i dettagli relativi alla negoziazione SASL, TLS e Dialback, inclusi valori non validi ed errori di configurazione noti, vedere [Impostazioni di negoziazione per i partner federati XMPP in Lync Server 2013](lync-server-2013-negotiation-settings-for-xmpp-federated-partners.md)
        
          -   
            **Necessaria**    Il servizio XMPP richiede la negoziazione TLS.
        
          -   
            **Facoltativa**    Il servizio XMPP indica se esiste l'obbligo di negoziare con TLS.
        
          -   
            **Non supportata**    Il servizio XMPP non supporta la negoziazione TLS.
    
      - **Negoziazione SASL**    Consente di definire le regole di negoziazione SASL. Un servizio XMPP può richiedere la negoziazione SASL, può definirla come facoltativa oppure l'utente può specificare che la negoziazione SASL non è supportata. Se si seleziona Facoltativa, l'eventuale obbligatorietà della negoziazione viene decisa dal servizio XMPP del partner.
        
          -   
            **Necessaria**    Il servizio XMPP richiede la negoziazione SASL.
        
          -   
            **Facoltativa**    Il servizio XMPP indica se esiste l'obbligo di negoziare con SASL.
        
          -   
            **Non supportata**    Il servizio XMPP non supporta la negoziazione SASL.
    
      - **Supporto server Dialback Negotiation** In questo processo vengono utilizzati Domain Name System (DNS) e un server autorevole per verificare che la richiesta provenga da un XMPP valido. A tale scopo, il server di origine crea un messaggio di un tipo specifico con una chiave di dialback generata e ricerca il server ricevente in DNS. Il server di origine invia la chiave in un flusso XML al risultato della ricerca DNS, presumibilmente il server ricevente. Alla ricezione della chiave mediante il flusso XML, il server ricevente non risponde al server di origine, ma invia la chiave a un server autorevole conosciuto, che ne verifica la validità. Se la chiave non è valida, il server ricevente non risponde al server di origine. Se invece è valida, notifica al server di origine che l'identità e la chiave sono valide e che la conversazione può iniziare.
        
        Sono disponibili due stati validi per la negoziazione di tipo **Dialback**:
        
          -   
            **True**    Il server XMPP è configurato per l'utilizzo della negoziazione Dialback se viene ricevuta una richiesta da un server di origine.
        
          -   
            **False**    Il server XMPP non è configurato per l'utilizzo della negoziazione Dialback e le eventuali richieste provenienti da un server di origine verranno ignorate.

10. Fare clic su **Commit** per salvare le modifiche apportate ai criteri utente o sito.

## Aggiornare i record DNS per il gateway XMPP di Lync Server 2013

1.  Per configurare DNS per la federazione XMPP, aggiungere il record SRV seguente al DNS esterno:\_xmpp-server.\_tcp.\<nome dominio\>. Il record SRV verrà risolto nell'FQDN Access Edge del server perimetrale, con valore di porta 5269.

