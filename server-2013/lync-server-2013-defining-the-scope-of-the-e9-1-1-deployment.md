---
title: "Lync Server 2013: Definizione dell'ambito della distribuzione di E9-1-1"
TOCTitle: Definizione dell'ambito della distribuzione di E9-1-1
ms:assetid: 2c572dfd-e901-471d-b5a0-18bc8d1d5328
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425775(v=OCS.15)
ms:contentKeyID: 49300032
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definizione dell'ambito della distribuzione di E9-1-1 in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-06-06_

Prima di configurare Microsoft Lync Server 2013 per il servizio di chiamate di emergenza E9-1-1, è necessario pianificare la distribuzione di tale servizio. Di seguito sono riportati alcuni aspetti di cui tenere conto:

  - **Politica aziendale e vincoli di tipo legale dell'organizzazione per il servizio E9-1-1**  
    Le disposizioni legali del servizio E9-1-1 per i PBX (denominati sistemi telefonici multilinea, o MLTS, nella terminologia relativa a E9-1-1) variano a seconda delle località. È consigliabile rivolgersi al team dell'ufficio legale per conoscere i vincoli eventualmente applicati alla distribuzione di Lync Server nella propria area geografica.

<!-- end list -->

  - **Aree dell'organizzazione che devono essere abilitate per il servizio E9-1-1**  
    È possibile abilitare il servizio E9-1-1 per l'intera organizzazione o solo per località selezionate. È ad esempio possibile applicare requisiti E9-1-1 diversi per gli uffici di stati diversi oppure escludere le sedi al di fuori degli Stati Uniti.

<!-- end list -->

  - **Modalità di distribuzione del servizio E9-1-1 nei siti di succursale**  
    La resilienza vocale è un concetto importante di cui tenere conto quando si distribuisce il servizio E9-1-1 in un sito di succursale. Se sono stati centralizzati i trunk SIP del servizio E-9-1-1 e si verifica un problema nella rete WAN, è possibile che i client che eseguono l'accesso non riescano a ottenere una posizione da servizio Informazioni percorso o a connettersi al provider di servizi di emergenza. In Lync Server sono disponibili diverse strategie per la gestione della resilienza vocale nelle succursali, tra cui la creazione di reti di dati resilienti, la distribuzione di un trunk SIP in ogni succursale o lo spostamento delle chiamate di emergenza nel gateway locale durante eventuali problemi di rete. Per informazioni dettagliate, vedere [Pianificazione della resilienza vocale del sito di succursale in Lync Server 2013](lync-server-2013-planning-for-branch-site-voice-resiliency.md).

<!-- end list -->

  - **Possibilità di abilitare il servizio E9-1-1 per gli utenti che lavorano all'esterno della rete**  
    L'acquisizione automatica della posizione è disponibile solo per i client all'interno della rete aziendale. L'organizzazione deve pertanto decidere se supportare le chiamate E9-1-1 effettuate da client Lync non locali, ad esempio se consentire agli utenti di effettuare chiamate di emergenza quando lavorano dalla propria abitazione o dalla sede di un cliente. Se è posizionato all'esterno di una rete aziendale, un client può essere configurato per richiedere la posizione a un utente. Poiché tuttavia queste posizioni fornite dagli utenti non possono essere precedentemente convalidate a fronte dello stradario generale, il dispatcher del provider di servizi di emergenza dovrà verificare la validità della posizione verbalmente con il chiamante prima di instradare la chiamata al centro di raccolta delle chiamate di emergenza (PSAP, Public Safety Answering Point).
    

    > [!NOTE]
    > I client Lync di utenti che si connettono alla rete aziendale tramite VPN possono raccogliere le informazioni sugli indirizzi IP interni, ma poiché questi indirizzi non possono essere usati per identificare la posizione effettiva dell'utente, è necessario escludere le subnet VPN dal servizio Informazioni percorso.



<!-- end list -->

  - **Possibilità di fornire il routing delle chiamate di emergenza per siti al di fuori degli Stati Uniti**  
    È possibile offrire il routing delle chiamate di emergenza per aree dell'azienda non servite dal provider di servizi di emergenza, ad esempio sedi internazionali. A tale scopo, creare un nuovo sito e quindi assegnare i criteri vocali ai siti che fanno riferimento a un utilizzo PSTN che instrada le chiamate tramite il gateway PSTN locale.

