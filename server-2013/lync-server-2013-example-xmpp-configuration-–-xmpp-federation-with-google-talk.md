---
title: 'Lync Server 2013: Esempio di configurazione XMPP - federazione di XMPP con Google Talk'
TOCTitle: Esempio di configurazione XMPP - federazione di XMPP con Google Talk
ms:assetid: 360a2f7b-015b-4e93-ac67-0f609c21f1a2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204807(v=OCS.15)
ms:contentKeyID: 49300164
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Esempio di configurazione XMPP in Lync Server 2013 - federazione di XMPP con Google Talk

 

_**Ultima modifica dell'argomento:** 2014-04-22_

Una configurazione di esempio per la distribuzione del proxy XMPP definisce una federazione con Google Talk.

## Esempio di configurazione XMPP - federazione di XMPP con Google Talk

1.  Nel Front End Server aprire la Distribuzione guidata di Lync Server. Fare clic su **Installa** o su **Aggiorna il sistema Lync Server** , quindi su **Installazione** o su **Rimozione componenti di Lync Server** . Fare clic su **Riesegui** .

2.  In **Installazione componenti di Lync Server** fare clic su **Avanti** . Nella schermata di riepilogo verranno visualizzate le azioni in esecuzione. Al termine della distribuzione, fare clic su **Visualizza log** per visualizzare i file di log disponibili. Fare clic su **Fine** per completare la distribuzione.

3.  Nel server perimetrale aprire la Distribuzione guidata di Lync Server. Fare clic su **Installa** o su **Aggiorna il sistema Lync Server**, quindi su **Installazione** o su **Rimozione componenti di Lync Server**. Fare clic su **Riesegui**.

4.  Aggiungere Google Talk come partner XMPP consentito. Google Talk attualmente supporta solo connessioni TCP senza crittografia per la federazione XMPP server-server e solo Server Dialback per la verifica dell'identità (vedere <http://xmpp.org/extensions/xep-0220.html>).
    
        New-CsXmppAllowedPartner gmail.com -TlsNegotiation NotSupported -SaslNegotiation NotSupported -EnableKeepAlive $false -SupportDialbackNegotiation $true

5.  Per abilitare la federazione perimetrale, digitare:
    
        Set-CsAccessEdgeConfiguration -AllowFederatedUsers $true

6.  In **Installazione componenti di Lync Server** fare clic su **Avanti** . Nella schermata di riepilogo verranno visualizzate le azioni in esecuzione. Al termine della distribuzione, fare clic su **Visualizza log** per visualizzare i file di log disponibili. Fare clic su **Fine** per completare la distribuzione.

7.  Nell' server perimetrale, nella Distribuzione guidata di Lync Server, accanto a **Passaggio 3: Richiesta, installazione o assegnazione dei certificati** , fare clic su **Riesegui** .
    
    > [!TIP]  
    > Se si distribuisce il server perimetrale per la prima volta, sarà disponibile il pulsante Esegui anziché Riesegui.


8.  Nella pagina **Attività certificato disponibili** fare clic su **Crea una nuova richiesta di certificato** .

9.  Nella pagina **Richiesta di certificato** fare clic su **Certificato perimetro esterno** .

10. Nella pagina **Richieste immediate o ritardate** selezionare la casella di controllo **Prepara la richiesta per l'invio posticipato** .

11. Nella pagina **File richiesta di certificato** digitare il percorso completo e il nome del file in cui si desidera salvare la richiesta, ad esempio c:\\cert\_perimetro\_esterno.cer.

12. Nella pagina **Specifica modello di certificato alternativo** , per utilizzare un modello diverso dal modello Web Server predefinito selezionare la casella di controllo **Utilizza modello di certificato alternativo per l'autorità di certificazione selezionata** .

13. Nella pagina **Impostazioni nome e sicurezza** eseguire le operazioni seguenti:
    
    1.  In **Nome descrittivo** digitare un nome visualizzato per il certificato.
    
    2.  In **Lunghezza bit** specificare la lunghezza in bit (di solito, l'impostazione predefinita **2048** ).
    
    3.  Verificare che la casella di controllo **Contrassegna come esportabile la chiave di certificato privata** sia selezionata.

14. Nella pagina **Informazioni sull'organizzazione** digitare il nome per l'organizzazione e l'unità organizzativa, ad esempio una divisione o un reparto.

15. Nella pagina **Dati geografici** specificare le informazioni sulla posizione.

16. Nella pagina **Nome soggetto / Nomi soggetto alternativi** verranno visualizzate le informazioni compilate automaticamente dalla procedura guidata. Se sono necessari ulteriori nomi alternativi soggetto, specificarli nei due passaggi successivi

17. Nella pagina **Impostazione del dominio SIP su nomi soggetto alternativi (SAN)** selezionare la casella di controllo del dominio per aggiungere una voce sip. *\<dominiosip\>* all'elenco dei nomi alternativi soggetto.

18. Nella pagina **Configura nomi alternativi soggetto aggiuntivi** specificare eventuali nomi alternativi del soggetto aggiuntivi necessari.
    
    > [!TIP]  
    > Se è installato il proxy XMPP, per impostazione predefinita le voci SAN vengono popolate con il nome di dominio, ad esempio contoso.com. Se sono necessarie ulteriori voci, aggiungerle in questo passaggio.


19. Nella pagina **Riepilogo richiesta** esaminare le informazioni sul certificato da utilizzare per generare la richiesta.

20. Al termine dell'esecuzione dei comandi è possibile fare clic su **Visualizza log** o su **Avanti** per continuare.

21. Nella pagina **File richiesta di certificato** è possibile visualizzare il file di richiesta di firma del certificato (CSR) generato facendo clic su **Visualizza** oppure uscire dalla Configurazione guidata certificati facendo clic su **Fine** .

22. Copiare il file di richiesta e inviarlo all'autorità di certificazione pubblica.

23. Dopo aver ricevuto, importato e assegnato il certificato pubblico, è necessario arrestare e riavviare i servizi del server perimetrale. Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.. In Lync Server Management Shell digitare:
    
    ```
    Stop-CsWindowsService
    ```
    ```
    Start-CsWindowsService
    ```

24. Per configurare DNS per la federazione XMPP, aggiungere il record SRV seguente al DNS esterno:\_xmpp-server.\_tcp. *\<nome dominio\>* . Il record SRV risolverà l'FQDN dell'Access Edge del server perimetrale con un valore di porta 5269.

25. Configurare un nuovo criterio di accesso esterno per abilitare tutti gli utenti aprendo Lync Server Management Shell in un Front End Server e digitando:
    
        New-CsExternalAccessPolicy -Identity FedPic -EnableFederationAccess $true -EnablePublicCloudAccess $true
        Get-CsUser | Grant-CsExternalAccessPolicy -PolicyName FedPic

