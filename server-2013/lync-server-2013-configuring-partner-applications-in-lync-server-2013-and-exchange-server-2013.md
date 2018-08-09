---
title: "Lync Server 2013: Config. applicaz. partner in MS LS 2013 e MS Exchange Server 2013"
TOCTitle: "Lync Server 2013: Config. applicaz. partner in MS LS 2013 e MS Exchange Server 2013"
ms:assetid: 9c3a3054-6201-433f-b128-4c49d3341370
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688151(v=OCS.15)
ms:contentKeyID: 49887675
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione delle applicazioni partner in Microsoft Lync Server 2013 e Microsoft Exchange Server 2013

 

_**Ultima modifica dell'argomento:** 2014-11-05_

L'autenticazione da server a server coinvolge in genere tre entità: i due server che devono comunicare tra loro e un server token di sicurezza di terze parti. Se due server (ad esempio server A e server B) devono comunicare, entrambi iniziano in genere contattando un server di token e ottenendo un token di sicurezza considerato attendibile da entrambi. Il server A presenta quindi il token di sicurezza al server B (e viceversa) a garanzia di autenticità e attendibilità.

Questa è tuttavia una regola generale. Lync Server 2013, Microsoft Exchange Server 2013 e Microsoft SharePoint Server 2013 non hanno necessità di usare un server di token di terze parti per comunicare tra loro in quanto questi prodotti server possono creare token di sicurezza reciprocamente accettabili senza bisogno di un server di token distinto. Questa funzionalità è disponibile solo in Lync Server 2013, Exchange 2013 e SharePoint Server 2013. Se è necessario configurare l'autenticazione da server a server con altri server, inclusi altri prodotti server Microsoft, occorre avvalersi di un server di token di terze parti.

Allo scopo di configurare l'autenticazione da server a server tra Lync Server e Exchange, è necessario eseguire due operazioni: 1) è necessario assegnare i certificati appropriati a ogni server; ed 2) è necessario configurare ogni server come applicazione partner dell'altro server, ovvero occorre configurare Lync Server 2013 come applicazione partner per Exchange 2013 e Exchange 2013 come applicazione partner per Lync Server 2013.

## Configurazione di Lync Server 2013 come applicazione partner per Exchange 2013

Il modo più semplice per configurare Lync Server 2013 come applicazione partner di Exchange 2013 consiste nell'eseguire lo script Configure-EnterprisePartnerApplication.ps1, uno script Windows PowerShell fornito con Exchange 2013. Per eseguire questo script, è necessario specificare l'URL per il documento dei metadati di autenticazione di Lync Server; si tratta in genere del nome di dominio completo del pool SharePoint seguito dal suffisso /metadata/json/1. Ad esempio:

    https://atl-cs-001.litwareinc.com/metadata/json/1

Per configurare Lync Server come applicazione partner, aprire la shell di gestione di Exchange ed eseguire un comando analogo a questo (presupponendo che Exchange sia stato installato sull'unità C: e che usi il percorso di cartella predefinito):

    "C:\Program Files\Microsoft\Exchange Server\V15\Scripts\Configure-EnterprisePartnerApplication.ps1 -AuthMetaDataUrl 'https://atl-cs-001.litwareinc.com/metadata/json/1' -ApplicationType Lync"

Dopo aver configurato l'applicazione partner è consigliabile arrestare e riavviare Internet Information Services (IIS) nei server delle cassette postali di Exchange e nei server di accesso client. È possibile riavviare IIS mediante un comando analogo a questo, che riavvia il servizio nel computer atl-exchange-001:

    iisreset atl-exchange-001

Questo comando può essere eseguito dall'interno della shell di gestione di Exchange oppure da qualsiasi altra finestra di comando eseguita con privilegi di amministratore.

## Configurazione di Exchange 2013 come applicazione partner per Lync Server 2013

Dopo aver configurato Lync Server 2013 come applicazione partner per Exchange 2013, è quindi necessario configurare Exchange come applicazione partner per Lync Server. A tale scopo, è possibile usare la Lync Server Management Shell e specificare il documento dei metadati di autenticazione per Exchange; si tratta in genere dell'URI del servizio Autodiscover di Exchange seguito dal suffisso /metadata/json/1. Ad esempio:

    https://autodiscover.litwareinc.com/autodiscover/metadata/json/1

In Lync Server, le applicazioni partner vengono configurate mediante il cmdlet [New-CsPartnerApplication](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsPartnerApplication). Oltre a specificare l'URI dei metadati è anche necessario impostare il livello di trust dell'applicazione impostandolo su Completo; ciò consente a Exchange di rappresentare se stesso e qualsiasi utente autorizzato nell'area di autenticazione. Ad esempio:

    New-CsPartnerApplication -Identity Exchange -ApplicationTrustLevel Full -MetadataUrl "https://autodiscover.litwareinc.com/autodiscover/metadata/json/1"

In alternativa, è possibile creare un'applicazione partner copiando e modificato il codice dello script disponibile nella documentazione di autenticazione da server a server di Lync Server 2013. Vedere l'articolo [Gestione dell'autenticazione da server a server (Oauth) e applicazioni partner in Lync Server 2013](lync-server-2013-managing-server-to-server-authentication-oauth-and-partner-applications.md) per ulteriori informazioni.

Se le applicazioni partner sono state configurate correttamente per Lync Server e Exchange, significa che è stata configurata anche l'autenticazione da server a server tra i due prodotti. Lync Server 2013 include un cmdlet di Windows PowerShell, [Test-CsExStorageConnectivity](https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsExStorageConnectivity), che consente di verificare che l'autenticazione da server a server sia stata correttamente configurata e che il servizio di archiviazione di Lync Server possa connettersi a Exchange 2013. Il cmdlet esegue questa operazione connettendosi alla cassetta postale di un utente di Exchange 2013, scrivendo un elemento nella cartella della cronologia delle conversazioni per l'utente in questione e quindi, eventualmente, eliminando l'elemento.

Per testare l'integrazione di Lync Server 2013 e Exchange 2013, eseguire un comando analogo a questo da Lync Server Management Shell:

    Test-CsExStorageConnectivity -SipUri "sip:kenmyer@litwareinc.com"

Nel comando precedente, SipUri rappresenta l'indirizzo SIP di un utente con un account in Exchange 2013; il comando ha esito negativo se l'account utente non è valido.

Se il test viene superato e viene stabilita la connessione, è quindi possibile procedere alla configurazione delle caratteristiche facoltative quali l'integrazione dell'archiviazione e l'archivio contatti unificato.

