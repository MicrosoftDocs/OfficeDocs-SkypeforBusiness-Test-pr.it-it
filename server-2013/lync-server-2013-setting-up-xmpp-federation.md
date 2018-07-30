---
title: 'Lync Server 2013: Configurazione della federazione di XMPP'
TOCTitle: Configurazione della federazione di XMPP
ms:assetid: 5fda6cb7-8d4d-495d-90c7-601f1036e085
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204939(v=OCS.15)
ms:contentKeyID: 49300726
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione della federazione di XMPP in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-12-03_

Per distribuire il proxy XMPP nel server perimetrale, è necessario configurare il server perimetrale per la federazione XMPP. A tale scopo, eseguire le operazioni seguenti.

## Configurazione della federazione di XMPP

1.  Accedere al computer in cui è installata la Distribuzione guidata di Lync Server come membro del gruppo Domain Admins e del gruppo RTCUniversalServerAdmins.

2.  Nel Front End Server aprire la Distribuzione guidata di Lync Server. Fare clic su Installa o aggiorna il sistema Lync Server e quindi su Installazione o rimozione componenti di Lync Server. Fare clic su Riesegui.

3.  In Installazione componenti di Lync Server fare clic su Avanti. Nella schermata di riepilogo verranno visualizzate le azioni in esecuzione. Al termine della distribuzione, fare clic su Visualizza log per visualizzare i file di log disponibili. Fare clic su Fine per completare la distribuzione.

4.  Nel server perimetrale aprire la Distribuzione guidata di Lync Server. Fare clic su Installa o aggiorna il sistema Lync Server e quindi su Installazione o rimozione componenti di Lync Server. Fare clic su Riesegui.

5.  In Installazione componenti di Lync Server fare clic su Avanti. Nella schermata di riepilogo verranno visualizzate le azioni in esecuzione. Al termine della distribuzione, fare clic su Visualizza log per visualizzare i file di log disponibili. Fare clic su Fine per completare la distribuzione.

6.  Nel server perimetrale fare clic su Riesegui nella Distribuzione guidata accanto a Passaggio 3: Richiesta, installazione o assegnazione dei certificati.
    
    > [!tip]  
    > Se si distribuisce il server perimetrale per la prima volta, sarà disponibile il pulsante Esegui anziché Riesegui.

7.  Nella pagina Attività certificato disponibili fare clic su Crea una nuova richiesta di certificato.

8.  Nella pagina Richiesta di certificato fare clic su Certificato perimetro esterno.

9.  Nella pagina Richieste immediate o ritardate selezionare la casella di controllo Prepara la richiesta per l'invio posticipato.

10. Nella pagina File richiesta di certificato digitare il percorso completo e il nome del file in cui si desidera salvare la richiesta, ad esempio c:\\cert\_perimetro\_esterno.cer.

11. Nella pagina Specifica modello di certificato alternativo, per utilizzare un modello diverso dal modello Web Server predefinito selezionare la casella di controllo Utilizza modello di certificato alternativo per l'autorità di certificazione selezionata.

12. Nella pagina Impostazioni nome e sicurezza eseguire le operazioni seguenti:
    
    1.  In Nome descrittivo digitare un nome visualizzato per il certificato.
    
    2.  In Lunghezza bit specificare la lunghezza in bit (di solito, l'impostazione predefinita 2048).
    
    3.  Verificare che la casella di controllo Contrassegna come esportabile la chiave di certificato privata sia selezionata.

13. Nella pagina Informazioni sull'organizzazione digitare il nome per l'organizzazione e l'unità organizzativa, ad esempio una divisione o un reparto.

14. Nella pagina Dati geografici specificare le informazioni sulla località.

15. Nella pagina Nome soggetto/Nomi soggetto alternativi verranno visualizzate le informazioni compilate automaticamente dalla procedura guidata. Se sono necessari ulteriori nomi alternativi soggetto, specificarli nei prossimi due passaggi.

16. Nella pagina Impostazione del dominio SIP su nomi alternativi soggetto (SAN) selezionare la casella di controllo del dominio per aggiungere una voce sip.\<dominiosip\> all'elenco dei nomi alternativi del soggetto.

17. Nella pagina Configura nomi alternativi soggetto aggiuntivi specificare eventuali nomi alternativi soggetto aggiuntivi richiesti.
    
    > [!tip]  
    > Se è installato il proxy XMPP, per impostazione predefinita le voci SAN vengono popolate con il nome di dominio, ad esempio contoso.com. Se sono necessarie ulteriori voci, aggiungerle in questo passaggio.

18. Nella pagina Riepilogo richiesta esaminare le informazioni sul certificato da utilizzare per generare la richiesta.

19. Dopo l'esecuzione del comando, è possibile scegliere Visualizza Log oppure fare clic su Avanti per continuare.

20. Nella pagina File richiesta di certificato è possibile visualizzare il file di richiesta di firma del certificato (CSR) generato facendo clic su Visualizza oppure uscire dalla Configurazione guidata certificati facendo clic su Fine.

21. Copiare il file di richiesta e inviarlo all'autorità di certificazione pubblica.

22. Dopo aver ricevuto, importato e assegnato il certificato pubblico, è necessario arrestare e riavviare i servizi del server perimetrale. A tale scopo, digitare quanto segue nella console di gestione di Lync Server:
    
    ```
    Stop-CsWindowsService
    ```
    ```
    Start-CsWindowsService
    ```

23. Per configurare DNS per la federazione XMPP, aggiungere il record SRV seguente al DNS esterno:\_xmpp-server.\_tcp.\<nome dominio\> Il record SRV risolverà l'FQDN dell'Access Edge del server perimetrale con un valore di porta 5269. È inoltre necessario configurare un record host 'A' (ad esempio, xmpp.contoso.com) che punta all'indirizzo IP del server Access Edge.
    
    > [!IMPORTANT]  
    > Se esistono pool di server perimetrali in più siti, è consigliabile aggiungere più record SRV per la federazione XMPP. Aggiungere un record SRV per ogni pool di server perimetrali nell'organizzazione e assegnare una diversa priorità a ognuno di questi record SRV. Quando tutti i pool di server perimetrali sono in esecuzione, le richieste XMPP verranno tutte gestite dal pool di server perimetrali prioritario, ma se tale pool di server perimetrali diventa inattivo sarà necessario aggiungere un nuovo record SRV per ripristinare la funzionalità di federazione XMPP.

24. Configurare nuovi criteri di accesso esterno per abilitare tutti gli utenti. A tale scopo, aprire Lync Server Management Shell nel Front End Server e digitare:
    
    ```
    New-CsExternalAccessPolicy -Identity <name of policy to create.  If site scope, prepend with 'site:'> -EnableFederationAcces $true -EnablePublicCloudAccess $true
    ```
    ```
    New-CsExternalAccessPolicy -Identity FedPic -EnableFederationAcces $true -EnablePublicCloudAccess $true
    ```
    ```
    Get-CsUser | Grant-CsExternalAccessPolicy -PolicyName FedPic
    ```
    Abilitare l'accesso XMPP per gli utenti esterni digitando:
    
    ```
    Set-CsExternalAccessPolicy -Identity <name of the policy being used> EnableXmppAccess $true
    ```
    ```
    Set-CsExternalAccessPolicy -Identity FedPic -EnableXmppAccess $true
    ```

25. Nel server perimetrale in cui è distribuito il proxy XMPP aprire un prompt dei comandi o un' interfaccia della riga di comando Windows PowerShell™ e digitare il comando seguente:
    
    ```
    Netstat -ano | findstr 5269
    ```
    ```
    Netstat -ano | findstr 23456
    ```
    
    Il comando **netstat -ano** è un comando per le statistiche di rete, i parametri **-ano** richiedono che il comando netstat visualizzi tutte le connessioni e le porte di attesa, che l'indirizzo e le porte vengano visualizzati in forma numerica e che l'ID del processo proprietario venga associato a ogni connessione. Il carattere **|** definisce una pipe per il comando successivo, **findstr**, ovvero "find string" (trova stringa). I numeri 5269 e 23456 passati a findstr come parametro indicano al comando di cercare le stringhe 5269 e 23456 nell'output di netstat. Se la configurazione di XMPP è corretta, il risultato dei comandi dovrebbe essere l'ascolto e l'attivazione delle connessioni sia sull'interfaccia esterna (porta 5269) che interna (porta 23456) del server perimetrale.
    
    Se i comandi non restituiscono porte attivate o in attesa per 5269 e 23456, controllare quanto segue:

## Risoluzione dei problemi relativi alla federazione XMPP

1.  Per stabilire se il proxy XMPP è in esecuzione, eseguire le operazioni seguenti:

2.  Accedere al server perimetrale che esegue il servizio proxy XMPP con un account membro del gruppo degli amministratori locali.

3.  Fare clic sul pulsante **Start** , scegliere **Tutti i programmi** , **Strumenti di amministrazione** e quindi **Servizi** .

4.  In Servizi individuare il servizio Lync Server XMPP Translating Gateway Proxy. Questo servizio dovrebbe essere in stato **Avviato** . In caso contrario, fare clic sull'icona **Avvia** sulla barra degli strumenti. L'icona ha la forma di una freccia verde rivolta a destra.

5.  Verificare che lo stato del servizio sia diventato **Avviato** . Se l'avvio è stato completato correttamente, chiudere **Servizi** e continuare.
    
    Se il servizio non è stato avviato, da Strumenti di amministrazione aprire Visualizzatore eventi e controllare gli errori e gli avvisi nella parte **Lync Server** in **Registri applicazioni e servizi** .

6.  Quando il sevizio **Lync Server XMPP Translating Gateway** è in esecuzione, ricontrollare i comandi netstat utilizzati in precedenza. Se non vengono indicate sessioni stabilite o in attesa, controllare e assicurarsi che la route di federazione XMPP sia configurata in modo corretto in Generatore di topologie

7.  Accedere al computer in cui è installato Generatore di topologie come membro del gruppo Domain Admins e del gruppo RTCUniversalServerAdmins.

8.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

9.  In Generatore di topologie selezionare il sito per la route di federazione XMPP e verificare che in **Assegnazione route federazione sito** per **Federazione XMPP** sia indicato il server perimetrale o il pool di server perimetrali come assegnazione di route di federazione XMPP selezionata.
    
    Se l'assegnazione della route non è corretta o non è impostata, fare clic con il pulsante destro del mouse sul sito e scegliere **Modifica proprietà** . Selezionare la casella di controllo Federazione XMPP e quindi selezionare il server perimetrale o pool di server perimetrali corretto.

10. Pubblicare la topologia. Per informazioni dettagliate, vedere [Pubblicare la topologia in Lync Server 2013](lync-server-2013-publish-your-topology.md).
    
    > [!tip]  
    > Sebbene non sia richiesto e in genere non occorra, potrebbe risultare necessario riavviare il server perimetrali

11. Tramite il processo netstat utilizzato in precedenza, verificare che il server perimetrale sia ora in attesa o abbia stabilito sessioni sulle porte 5269 e 23456.

12. Se ancora non vengono visualizzate le sessioni previste, controllare nel Visualizzatore eventi per individuare le possibili cause del problema di comunicazione.

## Vedere anche

#### Attività

[Esempio di configurazione XMPP in Lync Server 2013 - federazione di XMPP con Google Talk](lync-server-2013-example-xmpp-configuration-–-xmpp-federation-with-google-talk.md)  

#### Ulteriori risorse

[Gestire i partner federati XMPP per l'organizzazione in Lync Server 2013](lync-server-2013-manage-xmpp-federated-partners-for-your-organization.md)

