---
title: Istruzioni di configurazione speciali per le transazioni sintetiche
TOCTitle: Istruzioni di configurazione speciali per le transazioni sintetiche
ms:assetid: 694cbe05-5dba-4035-a01c-c87ebfb0478b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688080(v=OCS.15)
ms:contentKeyID: 49887593
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Istruzioni di configurazione speciali per le transazioni sintetiche

 

_**Ultima modifica dell'argomento:** 2013-01-22_

La maggior parte delle transazioni sintetiche può essere eseguita su un nodo Watcher così com'è, ovvero non appena la transazione sintetica viene aggiunta alle impostazioni di configurazione del nodo Watcher, questo può iniziare a utilizzarla durante l'esecuzione di test. Ciò non è vero, tuttavia, per tutte le transazioni sintetiche. Nelle sezioni seguenti vengono descritte le eccezioni, ovvero le transazioni sintetiche con istruzioni speciali per la configurazione.

## Transazioni sintetiche per conferenze dati

Se il computer del nodo Watcher si trova all'esterno della rete perimetrale, probabilmente non sarà possibile eseguire la transazione sintetica per le conferenze dati se non dopo aver disabilitato le impostazioni proxy di Internet Explorer per l'account Servizio di rete. Per disabilitare le impostazioni proxy per questo servizio, eseguire la procedura seguente:

1.  Nel computer del nodo Watcher, fare clic sul pulsante **Start**, scegliere **Tutti i programmi** e **Accessori**, fare clic con il pulsante destro del mouse su **Prompt dei comandi** e quindi scegliere **Esegui come amministratore**.

2.  Nella finestra della console digitare il comando seguente, quindi premere INVIO.
    
        bitsadmin /util /SetIEProxy NetworkService NO_PROXY

Nella finestra di comando verrà visualizzato il messaggio seguente:

    BITSAdmin is deprecated and is not guaranteed to be available in future versions of Windows. Administration tools for the BITS service are now provided by BITS PowerShell cmdlets.
    
    Internet proxy settings for account NetworkService set to NO_PROXY. 
    (connection = default)

Questo messaggio indica che sono state disabilitate le impostazioni proxy di Internet Explorer per l'account Servizio di rete.

## Transazioni sintetiche per la messaggistica unificata di Exchange.

La transazione sintetica per Messaggistica unificata di Exchange verifica che gli utenti di prova possano connettersi agli account della segreteria telefonica in Exchange. È necessario configurare tali utenti di prova con account per la segreteria telefonia prima che possano utilizzare i test di messaggistica unificata di Exchange.

## Transazioni sintetiche per Chat persistente

Per utilizzare la transazione sintetica per Chat persistente, gli amministratori devono prima creare un canale e concedere agli utenti di prova le autorizzazioni per il suo utilizzo. È possibile utilizzare il cmdlet [Test-CsPersistentChatMessage](test-cspersistentchatmessage.md) per configurare correttamente questi utenti di prova:

    $cred1 = Get-Credential "litwareinc\kenmyer"
    $cred2 = Get-Credential "litwareinc\pilar"
    
    Test-CsPersistentChatMessage -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress sip:kenmyer@litwareinc.com -SenderCredential $cred1 -ReceiverSipAddress sip:pilar@litwareinc.com -ReceiverCredential $cred2 -TestUser1SipAddress sip:kenmyer@litwareinc.com -TestUser2SipAddress sip:pilar@litwareinc.com -Setup $True

Questa attività di configurazione deve essere eseguita dall'interno dell'organizzazione:

  - Se l'attività viene eseguita da un computer non server, l'utente che esegue il cmdlet deve essere membro del ruolo PersistentChatAdministrators per il controllo di accesso basato sui ruoli (RBAC).

  - Se l'attività viene eseguita dal server stesso, l'utente che esegue il cmdlet deve essere un membro del gruppo RTCUniversalServerAdmins.

Nel comando precedente è incluso il parametro Setup impostato su True ($True). Se si include il parametro Setup, Test-CsPersistentChatMessage creerà una chat room speciale di Chat persistente e la popolerà con utenti di prova. Ciò consente di assicurarsi che sia effettivamente disponibile una chat room per i test. Si noti che il parametro Setup dovrebbe essere eseguito solo da un Front End Server.

La chat room creata da Test-CsPersistentChatMessage può essere eliminata solo da un amministratore.

## Transazioni sintetiche per chiamate peer-to-peer PSTN

La transazione sintetica [Test-CsPstnPeerToPeerCall](test-cspstnpeertopeercall.md) verifica la possibilità di effettuare e ricevere chiamate tramite la rete PSTN (Public Switched Telephone Network).

Per eseguire questa transazione sintetica, gli amministratori devono configurare:

  - Due utenti di prova (un chiamante e un ricevente) abilitati per VoIP aziendale.

  - Numeri DID (Direct Inward Dialing) per ogni account utente.

  - Criteri vocali e route vocali per consentire alle chiamate al numero del ricevente di raggiungere il gateway PSTN.

  - Un gateway PSTN che accetta le chiamate e un supporto per il routing delle chiamate al pool principale del ricevente in base al numero composto.

## Transazioni sintetiche per l'archivio contatti unificato

La transazione sintetica per l'archivio contatti unificato verifica che Lync Server 2013 sia in grado di recuperare contatti per conto di un utente da Microsoft Exchange Server 2013.

Per utilizzare questa transazione sintetica, devono essere soddisfatte le condizioni seguenti:

  - Configurazione dell'autenticazione tra Lync Server 2013 e Exchange 2013 ([Gestione dell'autenticazione da server a server (Oauth) e applicazioni partner in Lync Server 2013](lync-server-2013-managing-server-to-server-authentication-oauth-and-partner-applications.md)).

  - Gli utenti di prova devono disporre di una cassetta postale di Exchange 2013 valida.

Quando queste condizioni sono soddisfatte, gli amministratori possono eseguire il comando seguente per verificare che l'utente con indirizzo SIP kenmyer@litwareinc.com possa recuperare i contatti personali dall'archivio contatti unificato:

    Test-CsUnifiedContactStore -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:kenmyer@litwareinc.com" -RegistrarPort 5061 -Authentication TrustedServer -Setup

Si noti l'utilizzo del parametro Setup nel comando precedente. Se si include il parametro Setup durante l'esecuzione di Test-CsUnifiedContactStore, i contatti dell'utente specificato (in questo caso, sip:kenmyer@litwareinc.com) verranno spostati nell'archivio contatti unificato. (Naturalmente, i contatti non devono essere spostati se sono già presenti nell'archivio contatti unificato.) Il parametro Setup viene in genere utilizzato una sola volta, ovvero alla prima esecuzione di Test-CsUnifiedContactStore, e dovrebbe essere utilizzato solo con utenti di prova, ovvero con account utente che non si connetteranno mai veramente a Lync Server. Al termine della migrazione dei contatti dell'utente di prova nell'archivio contatti unificato, è possibile verificare che i contatti dell'utente possano essere recuperati, chiamando Test-CsUnifiedContactStore senza il parametro Setup:

    Test-CsUnifiedContactStore -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:kenmyer@litwareinc.com" -RegistrarPort 5061 -Authentication TrustedServer

## Transazioni sintetiche per XMPP

La transazione sintetica per la messaggistica istantanea XMPP (Extensible Messaging and Presence Protocol) richiede la configurazione della funzionalità XMPP in uno o più domini federati.

Per abilitare la transazione sintetica XMPP, è necessario specificare un parametro XmppTestReceiverMailAddress con un account utente come dominio XMPP instradabile. Ad esempio:

    Set-CsWatcherNodeConfiguration -Identity pool0.contoso.com -Tests @{Add="XmppIM"} -XmppTestReceiverMailAddress user1@litwareinc.com

In questo esempio, sarà necessaria una regola di Lync Server 2013 per l'instradamento dei messaggi per litwareinc.com a un gateway XMPP.

