---
title: Configurare il gateway XMPP in Lync Server 2013
TOCTitle: Configurare il gateway XMPP in Lync Server 2013
ms:assetid: c70282e0-b502-47e2-a0be-a32eb1faf99d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721881(v=OCS.15)
ms:contentKeyID: 49887746
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare il gateway XMPP in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-10-28_

Le ultime operazioni per la migrazione del gateway XMPP consistono nel configurare i certificati per il server perimetrale Lync Server 2013, distribuire il gateway XMPP di Lync Server 2013 e aggiornare i record DNS per il gateway XMPP. Queste operazioni devono essere eseguite in parallelo per ridurre al minimo il tempo di inattività del gateway XMPP. Prima di procedere con queste operazioni, è necessario spostare tutti gli utenti nella distribuzione di Microsoft Lync Server 2013.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La federazione XMPP non è supportata per gli utenti ospitati in Survivable Branch Appliance. Lo stesso vale per la visualizzazione di informazioni sulla presenza e lo scambio di messaggi istantanei.</td>
</tr>
</tbody>
</table>


## Configurare i certificati del gateway XMPP nel server perimetrale Lync Server 2013

1.  Nel server perimetrale fare clic su **Riesegui** nella Distribuzione guidata accanto a **Passaggio 3: Richiesta, installazione o assegnazione dei certificati** .
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Se si distribuisce il server perimetrale per la prima volta, sarà disponibile il pulsante Esegui anziché Riesegui.</td>
    </tr>
    </tbody>
    </table>


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
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Se è installato il proxy XMPP, per impostazione predefinita le voci SAN vengono popolate con il nome di dominio, ad esempio contoso.com. Se sono necessarie ulteriori voci, aggiungerle in questo passaggio.</td>
    </tr>
    </tbody>
    </table>


13. Nella pagina **Riepilogo richiesta** esaminare le informazioni sul certificato da utilizzare per generare la richiesta.

14. Dopo l'esecuzione del comando, è possibile scegliere **Visualizza Log** oppure fare clic su Avanti per continuare.

15. Nella pagina **File richiesta di certificato** è possibile visualizzare il file di richiesta di firma del certificato (CSR) generato facendo clic su **Visualizza** oppure uscire dalla Configurazione guidata certificati facendo clic su **Fine** .

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
    
      - **Negoziazione TLS**    Consente di definire le regole di negoziazione TLS. Un servizio XMPP può richiedere la negoziazione TLS, può definirla come facoltativa oppure l'utente può specificare che la negoziazione TLS non è supportata. Se si seleziona Facoltativa, l'eventuale obbligatorietà della negoziazione viene decisa dal servizio XMPP. Per visualizzare tutte le possibili impostazioni e informazioni per le negoziazioni SASL, TLS e Dialback, inclusi gli errori di configurazione non valida e sconosciuta, vedere [Impostazioni di negoziazione per i partner federati XMPP in Lync Server 2013](lync-server-2013-negotiation-settings-for-xmpp-federated-partners.md).
        
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

