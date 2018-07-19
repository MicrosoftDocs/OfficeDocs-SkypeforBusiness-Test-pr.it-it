---
title: "Lync Server 2013: Requisiti dei certificati per l'accesso utente esterno"
TOCTitle: Requisiti dei certificati per l'accesso utente esterno
ms:assetid: d45b6b10-556f-4b10-b1a7-fb0d0a64a498
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398920(v=OCS.15)
ms:contentKeyID: 49302094
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti dei certificati per l'accesso utente esterno in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-08_

Il software di comunicazioneMicrosoft Lync Server 2013 supporta l'utilizzo di un singolo certificato pubblico per le interfacce esterne dell'Access Edge Server e del Web Conferencing Edge Server, oltre al servizio di autenticazione A/V. L'interfaccia interna perimetrale utilizza in genere un certificato privato emesso da un'autorità di certificazione (CA) interna, ma può anche utilizzare un certificato pubblico, purché provenga da una CA pubblica attendibile. Il proxy inverso della distribuzione utilizza un certificato pubblico e crittografa le comunicazioni dal proxy inverso verso i client e dal proxy inverso verso i server interni mediante HTTP, ovvero Transport Layer Security su HTTP.

Di seguito sono riportati i requisiti dei certificati pubblici utilizzati per le interfacce esterne dell'Access Edge Server e del Web Conferencing Edge Server, nonché per il servizio di autenticazione A/V:

  - Il certificato deve essere emesso da una CA pubblica approvata che supporta il nome alternativo del soggetto. Per informazioni, vedere l'articolo 929395 della Microsoft Knowledge Base, "Partner certificati per le comunicazioni unificate per Exchange Server e per Communications Server", all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=202834](http://go.microsoft.com/fwlink/p/?linkid=202834).

  - Se il certificato verrà utilizzato in un pool di server perimetrali, deve essere creato come esportabile, con lo stesso certificato utilizzato in ogni server perimetrale del pool. Il requisito della chiave privata esportabile è previsto per il servizio di autenticazione A/V, che deve utilizzare la stessa chiave privata in tutti i server perimetrali del pool.

  - Se si desidera ottimizzare il tempo di attività dei servizi audio/video, rivedere i requisiti dei certificati e implementare un certificato del servizio servizio A/V Edge disaccoppiato, ovvero un certificato del servizio A/V Edge separato dagli scopi degli altri certificati perimetrali esterni. Per informazioni dettagliate, vedere [Modifiche introdotte in Lync Server 2013 che incidono sulla pianificazione dei server perimetrali](lync-server-2013-changes-in-lync-server-that-affect-edge-server-planning.md), [Pianificare i certificati dei server perimetrali in Lync Server 2013](lync-server-2013-plan-for-edge-server-certificates.md) e [Gestione temporanea dei certificati AV e OAuth utilizzando -Roll in Set-CsCertificate in Lync Server 2013](lync-server-2013-staging-av-and-oauth-certificates-using-roll-in-https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCertificate).

  - Il nome soggetto del certificato corrisponde al nome di dominio completo (FQDN) dell'interfaccia esterna del servizio Access Edge o al VIP di un dispositivo di bilanciamento del carico hardware, ad esempio access.contoso.com.
    

    > [!NOTE]
    > Per Lync Server 2013, questo requisito non è più necessario, ma è comunque consigliato per la compatibilità con Office Communications Server.



  - L'elenco di nomi alternativi del soggetto contiene i nomi FQDN dei componenti seguenti:
    
      - L'interfaccia esterna del servizio Access Edge o il VIP del dispositivo di bilanciamento del carico hardware, ad esempio access.contoso.com.
        

        > [!NOTE]
        > Anche se il nome del soggetto del certificato è uguale al nome FQDN dell'Access Edge Server, deve contenere anche questo FQDN perché Transport Layer Security (TLS) ignora il nome del soggetto e utilizza le voci dei nomi alternativi del soggetto per la convalida.

    
      - L'interfaccia esterna del Web Conferencing Edge Server o il VIP del dispositivo di bilanciamento del carico hardware, ad esempio webcon.contoso.com.
    
      - Se si utilizza la configurazione automatica dei client o la federazione, includere anche eventuali FQDN di dominio SIP utilizzati all'interno dell'organizzazione, ad esempio sip.contoso.com, sip.fabrikam.com.
    
      - Il servizio A/V Edge non utilizza le voci relative al nome soggetto o al nome alternativo del soggetto.
    

    > [!NOTE]
    > L'ordine dei nomi FQDN nell'elenco di nomi alternativi del soggetto non è importante.



Se si distribuiscono più server perimetrali con bilanciamento del carico in un sito, il certificato del servizio di autenticazione A/V installato in ogni server perimetrale deve provenire dalla stessa CA e deve utilizzare la stessa chiave privata. Si noti che la chiave privata del certificato deve essere esportabile, indipendentemente dal fatto che venga utilizzata in uno o in più server perimetrali. Deve essere esportabile anche se il certificato viene richiesto da qualsiasi altro computer diverso dal server perimetrale. Poiché il servizio di autenticazione A/V non utilizza il nome del soggetto o il nome alternativo del soggetto, è possibile riutilizzare il certificato dell'Access Edge Server, purché vengano soddisfatti i requisiti del nome del soggetto e del nome alternativo del soggetto per l'Access Edge Server e il Web Conferencing Edge Server e la chiave privata del certificato sia esportabile.

I requisiti per il certificato privato (o pubblico) utilizzato per l'interfaccia interna del server perimetrale sono i seguenti:

  - Il certificato può essere emesso da una CA interna o da una CA pubblica approvata.

  - Il nome del soggetto del certificato corrisponde in genere al nome FQDN dell'interfaccia interna perimetrale o al VIP del servizio di bilanciamento del carico hardware, ad esempio lsedge.contoso.com. È tuttavia possibile utilizzare anche un certificato con caratteri jolly.

  - Non è richiesto alcun elenco di nomi alternativi del soggetto.

Il proxy inverso dei servizi di distribuzione richiede:

  - Accesso di utenti esterni al contenuto delle riunioni

  - Accesso di utenti esterni per espandere e visualizzare i membri di gruppi di distribuzione

  - Accesso di utenti esterni a file scaricabili dal servizio Rubrica

  - Accesso di utenti esterni al client Lync Web App

  - Accesso di utenti esterni alla pagina Web Impostazioni conferenza telefonica con accesso esterno

  - Accesso di utenti esterni al servizio Informazioni percorso

  - Accesso di utenti esterni al servizio Aggiornamento dispositivo e recupero di aggiornamenti

Il proxy inverso pubblica gli URL dei componenti Web del server interno. Gli URL di questi componenti sono definiti nel Director, nel Front End Server o nel pool Front End come **servizi Web esterni** in Generatore di topologie.

Le voci con caratteri jolly sono supportate nel campo del nome alternativo del soggetto del certificato assegnato al proxy inverso. Per informazioni dettagliate su come configurare la richiesta di certificato per il proxy inverso, vedere [Richiedere e configurare un certificato per il proxy inverso HTTP in Lync Server 2013](lync-server-2013-request-and-configure-a-certificate-for-your-reverse-http-proxy.md).

## Vedere anche

#### Concetti

[Supporto dei certificati con caratteri jolly in Lync Server 2013](lync-server-2013-wildcard-certificate-support.md)

