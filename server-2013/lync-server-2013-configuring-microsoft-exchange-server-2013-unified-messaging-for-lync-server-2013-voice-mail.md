---
title: Configurazione della messaggistica unificata di Microsoft Exchange Server 2013 per la segreteria telefonica di Microsoft Lync Server 2013
TOCTitle: Configurazione della messaggistica unificata di Microsoft Exchange Server 2013 per la segreteria telefonica di Microsoft Lync Server 2013
ms:assetid: 1be9c4f4-fd8e-4d64-9798-f8737b12e2ab
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ687983(v=OCS.15)
ms:contentKeyID: 49887466
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione della messaggistica unificata di Microsoft Exchange Server 2013 per la segreteria telefonica di Microsoft Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-04_

Microsoft Lync Server 2013 consente di archiviare i messaggi della segreteria telefonica in Microsoft Exchange Server 2013; tali messaggi verranno quindi visualizzati come messaggi di posta elettronica nelle caselle Posta in arrivo degli utenti. Questa funzionalità era anche presente nelle edizioni 2010 di Lync Server e Exchange. Il processo di configurazione di questa messaggistica unificata, tuttavia, è stato semplificato nelle edizioni 2013 grazie all'introduzione del componente Router chiamate di messaggistica unificata, che viene installato nel server Accesso client di Exchange 2013. Tutte le chiamate alla messaggistica unificata di Exchange (ad esempio una segreteria telefonica) vengono prima indirizzate tramite il router chiamate, quindi reindirizzate al server Cassette postali appropriato.

Se è già stata configurata l'autenticazione da server a server tra Lync Server 2013 e Exchange 2013, è possibile configurare la messaggistica unificata. A tale scopo, creare e assegnare innanzitutto un nuovo dial plan di messaggistica unificata nel server Exchange. Ad esempio, questi due comandi (eseguiti da Exchange Management Shell) configurano un nuovo dial plan a tre cifre per Exchange:

    New-UMDialPlan -Name "RedmondDialPlan" -VoIPSecurity "Secured" -NumberOfDigitsInExtension 3 -URIType "SipName" -CountryOrRegionCode 1
    Set-UMDialPlan "RedmondDialPlan" -ConfiguredInCountryOrRegionGroups "Anywhere,*,*,*" -AllowedInCountryOrRegionGroups "Anywhere"

Nel primo comando dell'esempio, il parametro VoIPSecurity e il valore del parametro "Secured" indicano che il canale di segnale è crittografato tramite Transport Layer Security (TLS). Il parametro URIType "SipName" indica che i messaggi verranno inviati e ricevuti tramite il protocollo SIP e il valore 1 per CountryOrRegionCode indica che il dial plan si applica agli Stati Uniti.

Nel secondo comando il valore di parametro passato al parametro ConfiguredInCountryOrRegionGroups specifica quali gruppi nazionali è possibile utilizzare con questo dial plan. Il valore di parametro "Anywhere,\*,\*,\*" imposta quanto segue:

  - Nome gruppo

  - AllowedNumberString (\*, carattere jolly indicante che è consentita qualsiasi stringa numerica)

  - DialNumberString (\*, carattere jolly indicante che è consentito qualsiasi numero composto)

  - TextComment (\*, carattere jolly indicante che è consentito qualsiasi comando di testo)

Dopo aver creato e configurato il nuovo dial plan, è necessario aggiungerlo al server di messaggistica unificata, quindi impostare la modalità di avvio su "Doppio". Entrambe queste attività possono essere eseguite da Exchange Management Shell:

    Set-UmServer -Identity "atl-exchangeum-001.litwareinc.com" -DialPlans "RedmondDialPlan" -UMStartupMode "Dual"

Dopo la configurazione del server di messaggistica unificata, è necessario eseguire il cmdlet Enable-ExchangeCertificate per garantire l'applicazione del certificato di Exchange al servizio di messaggistica unificata:

    Enable-ExchangeCertificate -Server "atl-umserver-001.litwareinc.com" -Thumbprint "EA5A332496CC05DA69B75B66111C0F78A110D22d" -Services "SMTP","IIS","UM"

Dopo avere assegnato correttamente il certificato, è quindi necessario arrestare e riavviare il servizio MsExchangeUM sul server di messaggistica unificata. È necessario arrestare e riavviare il servizio ogni volta che si modifica la modalità di avvio.

Al termine della configurazione del server di messaggistica unificata, è quindi possibile configurare il Router chiamate di messaggistica unificata:

    Set-CsUMCallRouterSettings -Server "atl-exchange-001.litwareinc.com" -UMStartupMode "Dual" -DialPlans "RedmondDialPlan" 
    Enable-ExchangeCertificate -Server "atl-umserver-001.litwareinc.com" -Thumbprint "45BAA32496CC891169B75B9811320F78A1075DDA" -Services "IIS","UMCallRouter"

Dato che la modalità di avvio è stata modificata, è necessario arrestare e riavviare il servizio MsExchangeUMCR nel computer che ospita il router chiamate di messaggistica unificata.

Per completare l'impostazione della messaggistica unificata, è quindi necessario creare criteri di cassetta postale di messaggistica unificata e utilizzare tali criteri per abilitare la messaggistica unificata per gli utenti. È possibile creare criteri di cassetta postale tramite un comando simile al seguente:

    New-UMMailboxPolicy -ID "RedmondMailboxPolicy" -AllowedCountryOrRegionGroups "Anywhere"

È possibile abilitare la messaggistica unificata per un utente tramite un comando simile al seguente:

    Enable-UMMailbox -Extensions 100 -SIPResourceIdentifier "kenmyer@litwareinc.com" -Identity "litwareinc\kenmyer" -UMMailboxPolicy "RedmondMailboxPolicy"

Nel comando precedente, il parametro Extensions rappresenta il numero di interno telefonico dell'utente. In questo esempio l'utente ha l'interno 100.

Dopo averne abilitato la cassetta postale, l'utente kenmyer@litwareinc.com dovrebbe essere in grado di utilizzare la messaggistica unificata di Exchange. Per verificare che l'utente possa connettersi alla messaggistica unificata di Exchange, eseguire il cmdlet [Test-CsExUMConnectivity](https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsExUMConnectivity) da Lync Server Management Shell:

    $credential = Get-Credential "litwareinc\kenmyer"
    
    Test-CsExUMConnectivity -TargetFqdn "atl-cs-001.litwareinc.com" -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $credential

Se è presente un secondo utente per cui è stata abilitata la messaggistica unificata, è possibile utilizzare il cmdlet [Test-CsExUMVoiceMail](test-csexumvoicemail.md) per verificare che possa lasciare un messaggio della segreteria telefonica per il primo utente.

    $credential = Get-Credential "litwareinc\pilar"
    
    Test-CsExUMVoiceMail -TargetFqdn "atl-cs-001.litwareinc.com" -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $credential

