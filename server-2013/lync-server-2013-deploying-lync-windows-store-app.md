---
title: Distribuzione dell'app Lync di Windows Store
TOCTitle: Distribuzione dell'app Lync di Windows Store
ms:assetid: 9e00aaf4-15f9-4356-9ed7-5a58a2bfa043
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ822971(v=OCS.15)
ms:contentKeyID: 52062256
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuzione dell'app Lync di Windows Store

 

_**Ultima modifica dell'argomento:** 2013-12-03_

Prima di rendere l'app Windows Store Lync disponibile agli utenti, è necessario verificare che la distribuzione soddisfi i [Requisiti dell'app Lync di Windows Store](lync-server-2013-lync-windows-store-app-requirements.md). Per informazioni dettagliate sulla configurazione di Lync Server 2013 per il supporto dell'app Windows Store Lync, vedere l'articolo del blog NextHop relativo alla funzionalità di individuazione automatica di Lync Server e all'app Lync di Windows Store all'indirizzo [http://go.microsoft.com/fwlink/?LinkId=271966](http://go.microsoft.com/fwlink/?linkid=271966). Dopo aver configurato correttamente l'ambiente server, è possibile indicare agli utenti di scaricare l'app Lync da Windows Store cercando "Lync."

## Abilitazione dell'autenticazione a più fattori per l'app Windows Store Lync

Negli Aggiornamenti cumulativi per Lync Server 2013: giugno 2013 è stato aggiunto il supporto dell'autenticazione a più fattori per i clienti dell'app Windows Store Lync. Oltre al nome e alla password utente, è perciò possibile richiedere ulteriori metodi di autenticazione, ad esempio smart card o PIN, per autenticare gli utenti esterni quando eseguono l'accesso alle riunioni di Lync. È possibile abilitare l'autenticazione a più fattori distribuendo il server federativo di Active Directory Federation Service (ADFS) e abilitando l'autenticazione passiva in Lync Server 2013. Dopo la configurazione di ADFS, agli utenti esterni che tentano di partecipare a riunioni di Lync viene visualizzata una pagina Web di autenticazione a più fattori ADFS contenente la richiesta di nome e password utente, con gli eventuali altri metodi di autenticazione configurati.

> [!important]  
> Prima di configurare ADFS per l'autenticazione a più fattori per l'app Windows Store Lync, è importante considerare gli aspetti seguenti:<ul>
> <li><p>È necessario almeno Lync Server 2013 con gli Aggiornamenti cumulativi per Lync Server 2013: giugno 2013. I client desktop Lync 2013 non richiedono gli Aggiornamenti cumulativi per Lync Server 2013: giugno 2013, pertanto potrebbe sembrare che l'autenticazione passiva funzioni perché i client Lync 2013 riescono a eseguire l'autenticazione. In realtà il processo di autenticazione dei clienti dell'app Windows Store Lync non viene completato, senza che venga visualizzata una notifica o un messaggio di errore.</p></li>
> <li><p>Il server deve essere configurato in modo che l'autenticazione passiva sia l'unico tipo di autenticazione offerto.</p></li>
> 
> <li><p>Se si usano dispositivi di bilanciamento del carico hardware, abilitare il salvataggio permanente dei cookie in tali dispositivi, in modo che tutte le richieste provenienti dal client dell'app Windows Store Lync vengano gestite dallo stesso server front-end.</p></li>
> 
> 
> <li><p>Quando si stabilisce una relazione di trust di relying party tra i server ADFS e Lync Server, assegnare ai token una durata tale da coprire la lunghezza massima delle riunioni di Lync. 240 minuti in genere sono una durata sufficiente per i token.</p></li></ul>


**Per configurare l'autenticazione a più fattori**

1.  Installare un ruolo del server federativo ADFS. Per informazioni dettagliate, vedere la guida alla distribuzione di Active Directory Federation Services 2.0 all'indirizzo <http://go.microsoft.com/fwlink/p/?linkid=267511>.

2.  Creare certificati per ADFS. Per altre informazioni, vedere la sezione "Certificati server federativi" dell'argomento Pianificazione e distribuzione di ADFS per l'utilizzo con l'accesso Single Sign-On all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=285376](http://go.microsoft.com/fwlink/p/?linkid=285376).

3.  Dall'interfaccia della riga di comando di Windows PowerShell eseguire il comando seguente:
    
        add-pssnapin Microsoft.Adfs.powershell

4.  Stabilire una relazione eseguendo il comando seguente:
    
        Add-ADFSRelyingPartyTrust -Name ContosoApp -MetadataURL https://lyncpool.contoso.com/passiveauth/federationmetadata/2007-06/federationmetadata.xml

5.  Impostare le regole di relying party seguenti:
    
    ```
    $IssuanceAuthorizationRules = '@RuleTemplate = "AllowAllAuthzRule" => issue(Type = "http://schemas.contoso.com/authorization/claims/permit", Value = "true");'$IssuanceTransformRules = '@RuleTemplate = "PassThroughClaims" @RuleName = "Sid" c:[Type == "http://schemas.contoso.com/ws/2008/06/identity/claims/primarysid"]=> issue(claim = c);'
    ```
    ```
    Set-ADFSRelyingPartyTrust -TargetName ContosoApp -IssuanceAuthorizationRules $IssuanceAuthorizationRules -IssuanceTransformRules $IssuanceTransformRules
    ```
    ```
    Set-CsWebServiceConfiguration -UseWsFedPassiveAuth $true -WsFedPassiveMetadataUri https://dc.contoso.com/federationmetadata/2007-06/federationmetadata.xml
    ```

## Problemi noti che possono impedire l'accesso

## La data e l'ora non sono impostate correttamente nel dispositivo che esegue l'app Windows Store Lync

L'impostazione dell'ora nel dispositivo deve essere sincronizzata con l'impostazione dell'ora nel server. Questo aspetto è particolarmente importante per i dispositivi come Microsoft Surface e altri dispositivi che eseguono Windows RT e non appartengono a un dominio. Per impostare automaticamente l'ora su questi dispositivi da un server di riferimento ora, eseguire il comando seguente da un prompt dei comandi con privilegi elevati sul dispositivo:

    w32tm /resync

## L'app Windows Store Lync non riesce ad accedere al server o ai servizi Lync

L'app Windows Store Lync potrebbe non essere in grado di accedere al server o ai servizi Lync tramite schede di rete, quali i modem USB 4G LTE, che non vengono registrati con Windows 8 come dispositivi fisici. L'app Windows Store Lync potrebbe riscontrare questo problema anche quando le app desktop e i browser riescono invece ad accedere ad altri server e siti Web.

## L'app Lync di Windows Store non è in grado di effettuare l'accesso con Lync Server 2010 e Office Communications Server 2007 R2 Edge Server

Se la topologia è costituita da Lync Server 2010 con Office Communications Server 2007 R2 Edge Server, è necessario eseguire la versione aggiornata di Generatore di topologie disponibile nell'aggiornamento cumulativo per Lync Server 2010: luglio 2013. Le versioni precedenti di Generatore di topologie non creano il mapping a Office Communications Server 2007 Edge Server necessario, impedendo l'accesso ai client dell'app Lync di Windows Store. La procedura da eseguire è la seguente:

1.  Installare l'aggiornamento cumulativo per Lync Server 2010: luglio 2013 nei pool di Lync Server 2010 e nei server Director di Lync Server 2010.

2.  Eseguire i passaggi seguenti per aggiornare la configurazione dell'individuazione automatica di Lync per indicare che il punto di ingresso SIP esterno è l'indirizzo del server perimetrale:
    
    1.  Aprire Lync Server Management Shell.
    
    2.  Eseguire il comando seguente:
        
            Set-CsAutodiscoverConfiguration -ExternalSipClientAccessFqdn <FQDN of server used for external client access> -ExternalSipClientAccessPort 443

## L'app Lync di Windows Store non può eseguire l'accesso a causa di un errore di convalida del nome del certificato

Può verificarsi un problema di accesso per gli utenti di Office 365 che non eseguono la versione più recente di app Windows Store Lync. In genere questo problema si verifica durante l'utilizzo di più domini (ad esempio, quando l'URI SIP è **userA@domainZ.com**, ma il server perimetrale è **sip.domainX.com**). Per correggere il problema, gli utenti devono installare la versione più recente di app Windows Store Lync, che richiede anche Windows 8.1.

## Usare i log dell'app Windows Store Lync per la risoluzione dei problemi

È possibile usare i log generati nel dispositivo per risolvere eventuali problemi. I log vengono archiviati nella cartella seguente:

%LocalAppData%\\Packages\\Microsoft.LyncMX\_8wekyb3d8bbwe\\LocalState\\Tracing

Prima di recuperare i log di un utente, verificare che la registrazione sia attivata e quindi chiedere all'utente di salvare i log in modo che anche tutte le informazioni in memoria vengano salvate su file nel disco rigido.

**Per attivare le registrazione**

1.  Aprire l'app Windows Store Lync nel dispositivo.

2.  Scorrere rapidamente dal lato destro dello schermo. Se si usa un mouse, posizionare il puntatore nell'angolo in alto a destra dello schermo e quindi spostarlo verso il basso.

3.  Selezionare **Impostazioni**, **Opzioni** e quindi attivarel'opzione **Log diagnostici**.

4.  Se l'opzione**Log diagnostici** era disattivata, è necessario riavviare Lync eseguendo una delle operazioni seguenti:
    
      - Riavviare il dispositivo.
    
      - Terminare l'attività di Lync e avviare di nuovo l'app. Per terminare l'attività, aprire Gestione attività Windows, selezionare **Lync** e quindi toccare **Termina attività**. Se Lync non è elencato, toccare **Più dettagli** e cercare Lync in **Processi in background**.

**Per salvare i log**

1.  Aprire l'app Windows Store Lync nel dispositivo.

2.  Provare a effettuare l'accesso.

3.  Scorrere rapidamente dal lato destro dello schermo. Se si usa un mouse, posizionare il puntatore nell'angolo in alto a destra dello schermo e quindi spostarlo verso il basso.

4.  Selezionare **Impostazioni**, **Informazioni su** e quindi **Salva log**.

