---
title: 'Lync Server 2013: Creare o modificare la configurazione dei partner XMPP'
TOCTitle: Creare o modificare la configurazione dei partner XMPP
ms:assetid: 362dbe5e-8ee9-4aba-8c26-5907312b4a60
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ552447(v=OCS.15)
ms:contentKeyID: 49300156
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare la configurazione dei partner XMPP in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-09-03_

Microsoft Lync Server 2013 integra un proxy XMPP (Extensible Messaging and Presence Protocol) nel server perimetrale e un gateway XMPP nel Front End Server o nel pool Front End. Per consentire le connessioni da altre distribuzioni di XMPP, è necessario configurare XMPP nel Pannello di controllo di Lync Server. Le impostazioni devono essere configurate sulla base del dominio XMPP. Per creare una nuova associazione di partner, procedere come segue:

## Per creare un nuovo partner federato o modificare una configurazione esistente

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Federazione e accesso esterno**, quindi su **Partner federati XMPP**.

4.  Per creare una nuova configurazione, fare clic su **Nuovo**

5.  Per modificare una configurazione esistente, selezionarla e fare clic su **Modifica**

6.  Per creare o modificare le configurazioni per i **Partner federati XMPP**, è necessario definire le impostazioni seguenti:

7.  **Dominio primario** (obbligatorio). Il dominio primario è il dominio di base del partner XMPP. È ad esempio possibile immettere **fabrikam.com** come nome di dominio del partner XMPP. Questa è una voce obbligatoria.

8.  **Descrizione**. La descrizione è costituita da note o altre informazioni di identificazione di questa specifica configurazione. Questa voce è facoltativa.

9.  **Domini aggiuntivi**. I domini aggiuntivi sono domini che fanno parte del dominio del partner XMPP che dovrebbero essere inclusi come parte della comunicazione XMPP consentita. Se ad esempio il dominio primario è **fabrikam.com**, si dovrebbero elencare tutti gli altri domini al di sotto di fabrikam.com con cui si comunicherà mediante il protocollo XMPP. Ad esempio, si potrebbe immettere **corp.fabrikam.com** e **it.fabrikam.com** per i domini XMPP Corporate e Information Technologies sotto il dominio XMPP principale di fabrikam.com.

10. **Tipo di partner**. Il **Tipo di partner** è un'impostazione obbligatoria che prevede la possibilità di scegliere tra tre opzioni di un menu a discesa. È necessario scegliere una delle opzioni seguenti per descrivere e specificare i contatti che si possono aggiungere. Le opzioni sono:
    
      - **Federato**. Un tipo di partner **Federato** è una connessione affidabile tra una distribuzione partner Lync Server o Office Communications Server 2007 R2.
    
      - **Verificato pubblico**. Un partner **Verificato pubblico** consente di aggiungere all'elenco dei contatti dell'utente i contatti che fanno parte di una distribuzione verificata dal provider. L'utente di Lync può inviare inviti al contatto del partner oppure l'utente di Lync può accettarli da tale contatto.
    
      - **Non verificato pubblico**. Una relazione di tipo **Non verificato pubblico** implica che tra le due distribuzioni non sussiste uno stato stabilito e verificabile. Per consentire a un contatto non verificato di aggiungere un utente di Lync al proprio elenco dei contatti, l'utente di Lync deve invitare tale contatto. Ad esempio, Google GTalk non è un servizio XMPP pubblico verificato rispetto a Lync Server. Un utente di GTalk non potrà aggiungere l'utente di Lync come contatto, senza un invito esplicito inviato dall'utente di Lync.

11. Note sulla negoziazione dei flussi e sui metodi di sicurezza TLS (Transport Layer Security) e SASL (Software Authentication and Security Layer):
    
    **XMPP Standards Foundation** (XSF) e **Internet Engineering Task Force** (IETF) definiscono un insieme di regole e standard per l'uso e la gestione dei certificati client TLS, dei certificati server TLS e del meccanismo SASL. L'utilizzo di TLS e SASL è la procedura richiesta per proteggere il flusso XMPP. Nella sintesi del documento **XEP-0178** gli standard XMPP specificano un flusso di protocollo consigliato per l'uso del meccanismo SASL EXTERNAL con i certificati PKIX, soprattutto nei casi in cui un servizio XMPP indica che è necessaria la negoziazione TLS. PKIX, come indicato nella documentazione relativa a XSF, fa riferimento all'infrastruttura a chiave pubblica, nota anche come PKI.
    
    Vedere il documento XSF XEP-0178 per altri dettagli sui requisiti del protocollo XMPP. Per informazioni dettagliate, vedere "XEP-0178: Best Practices for Use of SASL EXTERNAL with Certificates". <http://xmpp.org/extensions/xep-0178.html>
    
    Vedere la sezione 5 del documento relativo a IETF "Extensible Messaging and Presence Protocol (XMPP): Core": STARTTLS Negotiation <http://tools.ietf.org/html/rfc6120>.
    
      - **Negoziazione TLS** . Consente di definire le regole di negoziazione TLS. Un servizio XMPP può richiedere la negoziazione TLS, può definirla come facoltativa oppure l'utente può specificare che la negoziazione TLS non è supportata. Se si seleziona Facoltativa, l'eventuale obbligatorietà della negoziazione viene decisa dal servizio XMPP. Per visualizzare tutte le possibili impostazioni e informazioni per le negoziazioni SASL, TLS e Dialback, inclusi gli errori di configurazione non valida e sconosciuta, vedere [Impostazioni di negoziazione per i partner federati XMPP in Lync Server 2013](lync-server-2013-negotiation-settings-for-xmpp-federated-partners.md).
        
          -   
            **Necessaria**. Il servizio XMPP richiede la negoziazione TLS.
        
          -   
            **Facoltativa**. Il servizio XMPP indica se esiste l'obbligo di negoziare con TLS.
        
          -   
            **Non supportata**. Il servizio XMPP non supporta la negoziazione TLS.
    
      - **Negoziazione SASL**. Consente di definire le regole di negoziazione SASL. Un servizio XMPP può richiedere la negoziazione SASL, può definirla come facoltativa oppure l'utente può specificare che la negoziazione SASL non è supportata. Se si seleziona Facoltativa, l'eventuale obbligatorietà della negoziazione viene decisa dal servizio XMPP del partner.
        

        > [!WARNING]
        > In SASL è richiesto TLS. Per poter usare SASL, è necessario specificare se TLS deve essere obbligatorio o facoltativo. Qualsiasi configurazione che definisca SASL come obbligatorio o facoltativo deve prevedere il supporto di TLS. Se non si specifica se TLS deve essere obbligatorio o facoltativo e si fa clic su <STRONG>Commit</STRONG> per salvare le modifiche, viene visualizzato un avviso che segnala che SASL deve prevedere il supporto di TLS e che le modifiche non verranno salvate. Per risolvere l'errore, impostare TLS su <STRONG>Richiesto</STRONG> o su <STRONG>Facoltativo</STRONG>. Se l'uso di SASL è facoltativo e il supporto della negoziazione TLS non è possibile, è necessario impostare la negoziazione SASL su <STRONG>Non supportato</STRONG>. Verificare con il servizio XMPP quali sono flussi di negoziazione appropriati per TLS e SASL per evitare che il servizio venga interrotto.

        
          -   
            **Necessaria**. Il servizio XMPP richiede la negoziazione SASL.
        
          -   
            **Facoltativa**. Il servizio XMPP indica se esiste l'obbligo di negoziare con SASL.
        
          -   
            **Non supportata**. Il servizio XMPP non supporta la negoziazione SASL.
    
      - **Dialback Negotiation**. Dialback Negotiation è definito da XSF nel documento **XEP-220: Server Dialback**<http://xmpp.org/extensions/xep-0220.html>. Il processo Server Dialback usa il DNS (Domain Name System) e un server autorevole per verificare che la richiesta provenga da un partner XMPP valido. A questo scopo, il server di origine crea un messaggio di un tipo specifico con una chiave dialback generata ed esegue la ricerca del server destinatario in DNS. Il server di origine invia la chiave in un flusso XML alla ricerca DNS risultante, presumibilmente il server destinatario. Alla ricezione della chiave nel flusso XML, il server destinatario non risponde al server di origine ma invia la chiave a un server autorevole noto che a sua volta verifica la validità della chiave. Se la chiave non è valida, il server destinatario non risponde al server di origine. In caso contrario, il server destinatario informa il server di origine che l'identità e la chiave sono validi e che la conversazione può iniziare.
        
        Sono disponibili due stati validi per la negoziazione di tipo **Dialback**:
        
          -   
            **True**. Il server XMPP è configurato per usare Dialback Negotiation se viene ricevuta una richiesta da un server di origine
        
          -   
            **False**. Il server XMPP non è configurato per l'utilizzo di Dialback Negotiation e le eventuali richieste provenienti da un server di origine verranno ignorate

