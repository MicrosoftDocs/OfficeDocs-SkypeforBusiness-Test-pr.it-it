---
title: Creare le impostazioni di configurazione di Registrazione avanzata
TOCTitle: Creare le impostazioni di configurazione di Registrazione avanzata
ms:assetid: eddfbdd2-cfd0-4c03-986e-443d6728db7d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182601(v=OCS.15)
ms:contentKeyID: 49302377
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare le impostazioni di configurazione di Registrazione avanzata

 

_**Ultima modifica dell'argomento:** 2013-03-17_

È possibile utilizzare la funzione di registrazione per configurare metodi di autenticazione di server proxy. Il protocollo di autenticazione specificato determina il tipo di richieste dei server del pool per i client. I protocolli disponibili sono i seguenti:

  - **Kerberos**   Costituisce lo schema di autenticazione basato su password più sicuro per i client, ma è in genere disponibile solo per i client aziendali, in quanto richiede la connessione dei client a un Centro distribuzione chiavi (controller di dominio Kerberos). Questa impostazione è appropriata se il server deve eseguire solo l'autenticazione dei client aziendali.

  - **NTLM**   Si tratta di uno schema di autenticazione basato su password disponibile per i client che utilizzano uno schema di hashing di richiesta-risposta sulla password. È l'unica forma di autenticazione disponibile per i client senza connettività a un Centro distribuzione chiavi (controller di dominio Kerberos), ad esempio gli utenti remoti. Se un server autentica solo utenti remoti, è consigliabile scegliere NTLM.

  - **Autenticazione con certificati**   Questo è un nuovo metodo di autenticazione in cui il server deve ottenere certificati da client Lync Phone Edition, telefoni per aree comuni e Lync 2013. Nei Lync Phone Edition, dopo l'accesso e l'autenticazione di un utente mediante PIN, Lync Server 2013 fornisce l'URI SIP al telefono e un certificato firmato di Lync Server o un certificato utente che identifica Joe (ad esempio: SN=joe@contoso.com ) per il telefono. Questo certificato viene utilizzato per l'autenticazione con la funzione di Registrazione avanzata e i servizi Web.


> [!NOTE]
> È consigliabile abilitare sia Kerberos sia NTLM quando un server supporta l'autenticazione per client remoti e aziendali. Il server perimetrale e i server interni comunicano per assicurare che ai client remoti venga offerta solo l'autenticazione NTLM. I server in cui è abilitata solo l'autenticazione Kerberos non sono in grado di autenticare gli utenti remoti. Se il server autentica anche gli utenti aziendali, viene utilizzato Kerberos.



Eseguire la procedura seguente per creare una nuova funzione di registrazione.

## Per creare una funzione di registrazione

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsServerAdministrator o CsAdministrator, accedere a un computer nella rete in cui è stato distribuito Lync Server 2013.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Sicurezza**, quindi su **Funzione di registrazione**.

4.  Nella pagina **Funzione di registrazione** fare clic su **Nuovo**

5.  In **Seleziona un servizio** fare clic sul servizio a cui applicare la funzione di registrazione e quindi su **OK**.

6.  In **Impostazione funzione di registrazione** selezionare una o più opzioni seguenti in base alle funzionalità dei client e al supporto nell'ambiente:
    
      - **Abilita autenticazione Kerberos** per fare in modo che tutti i server del pool emettano richieste utilizzando l'autenticazione Kerberos.
    
      - **Abilita autenticazione NTLM** per fare in modo che tutti i server del pool emettano richieste utilizzando l'autenticazione NTLM.
    
      - **Abilita autenticazione certificato** per fare in modo che i server nel pool emettano i certificati per i client.

7.  Fare clic su **Commit**.

