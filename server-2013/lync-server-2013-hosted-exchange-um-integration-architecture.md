---
title: "Lync Server 2013: Architettura dell'integrazione della messaggistica unificata di Exchange ospitata"
TOCTitle: Architettura dell'integrazione della messaggistica unificata di Exchange ospitata
ms:assetid: 0094d5dc-1836-441c-b6e2-f88e35203a8d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398067(v=OCS.15)
ms:contentKeyID: 49299479
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Architettura dell'integrazione della messaggistica unificata di Exchange ospitata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-25_

L'applicazione di routing di messaggistica unificata di Exchange di Lync Server 2013 supporta l'integrazione con una distribuzione della Messaggistica unificata di Exchange locale, con la messaggistica unificata di Exchange ospitata da un provider di servizi o con una combinazione di entrambe. Nella figura riportata di seguito vengono illustrate tutte e tre queste possibilità.

**Integrazione con una distribuzione della messaggistica unificata di Exchange locale e due provider di Exchange ospitati**

![Distribuzione della messaggistica unificata di Exchange con Lync Server in locale](images/Gg398821.d6498eb9-87ee-40f3-8ecd-852f91546590(OCS.15).jpg "Distribuzione della messaggistica unificata di Exchange con Lync Server in locale")

Sono supportate le modalità seguenti:

  - **Distribuzione locale :** Lync Server 2013 e la messaggistica unificata di Exchange sono entrambi distribuiti in server locali all'interno dell'azienda.

  - **Distribuzione tra ambienti locali :** Lync Server 2013 è distribuito in server locali all'interno dell'azienda e la messaggistica unificata di Exchange è ospitata in una struttura del provider di servizi online, ad esempio un data center di Microsoft Exchange Online.

  - **Distribuzione mista :** la distribuzione di Lync Server 2013 ha alcune cassette postali degli utenti in server Exchange locali all'interno dell'azienda e alcune cassette postali in un data center del servizio di Exchange ospitato.
    

    > [!NOTE]
    > La distribuzione mista può essere utilizzata come soluzione di transizione durante la valutazione e la migrazione in fasi degli utenti nella messaggistica unificata di Exchange ospitata oppure come soluzione definitiva se si sceglie di lasciare in locale i servizi di messaggistica unificata di Exchange di alcuni utenti dopo averne trasferiti altri.



## Spazio di indirizzamento SIP condiviso

Per integrare Lync Server 2013 con una distribuzione della messaggistica unificata di Exchange locale, è necessario concedere a Lync Server 2013 l'autorizzazione per leggere gli oggetti di Servizi di dominio Active Directory della messaggistica unificata di Exchange. Questo approccio tuttavia non funziona per l'integrazione con la messaggistica unificata di Exchange ospitata perché Lync Server 2013 e la messaggistica unificata di Exchange sono installati in foreste separate senza una relazione di trust tra loro.

Per integrare Lync Server 2013 con la messaggistica unificata di Exchange ospitata, è necessario configurare uno *spazio di indirizzamento SIP condiviso* . In questa configurazione lo stesso spazio di indirizzamento di dominio SIP è disponibile sia per Lync Server 2013 che per il provider di servizi di messaggistica unificata di Exchange ospitata.


> [!NOTE]
> L'utilizzo di uno spazio di indirizzamento SIP condiviso è simile all'approccio utilizzato in una configurazione Lync Server 2013 tra ambienti locali, in cui alcuni utenti si trovano nella distribuzione locale e altri in una distribuzione ospitata, ad esempio Lync Online. Il dominio SIP è diviso tra loro. Quando si integra Lync Server 2013 con la messaggistica unificata di Exchange ospitata, ricordarsi di includere il provider di tali servizi nello spazio di indirizzamento SIP condiviso.



Per configurare lo spazio di indirizzamento SIP condiviso per l'integrazione con un provider di servizi di messaggistica unificata di Exchange, sarà necessario configurare il server perimetrale come segue:

1.  Configurare il server perimetrale per la federazione eseguendo il cmdlet **Set-CsAccessEdgeConfiguration** per impostare i parametri seguenti:
    
      - **UseDnsSrvRouting** specifica che i server perimetrali si baseranno su record DNS SRV per l'invio e la ricezione di richieste di federazione.
    
      - **AllowFederatedUsers** specifica se agli utenti interni è consentito comunicare con utenti di domini federati. Questa proprietà determina inoltre se gli utenti interni possono comunicare con gli utenti in uno scenario di dominio diviso.
    
      - **EnablePartnerDiscovery** consente di specificare se Lync Server 2013 utilizzerà i record DNS per tentare di individuare i domini partner non elencati tra i domini consentiti di Active Directory. Se il parametro è False, Lync Server 2013 stabilirà la federazione solo con i domini inclusi nell'elenco dei domini consentiti. Questo parametro è obbligatorio se si utilizza il routing del servizio DNS. Nella maggior parte delle distribuzioni il valore è impostato su False per evitare l'apertura della federazione a tutti i partner.

2.  Replicare l' archivio di gestione centrale nel server perimetrale e verificare la replica. Per informazioni dettagliate, vedere [Esportare la topologia di Lync Server 2013 e copiarla su supporto esterno per l'installazione perimetrale](lync-server-2013-export-your-topology-and-copy-it-to-external-media-for-edge-installation.md) nella documentazione relativa alla distribuzione.

3.  Configurare un *provider di hosting* nel server perimetrale eseguendo il cmdlet **New-CsHostingProvider** per impostare i parametri seguenti:
    
      - **Identity** consente di specificare un identificatore come valore stringa univoco per il provider di hosting da creare, ad esempio **Messaggistica unificata Exchange ospitata** .
    
      - **Enabled** consente di indicare se la connessione di rete tra il dominio dell'organizzazione e il provider di hosting è abilitata. Deve essere impostato su **True** .
    
      - **EnabledSharedAddressSpace** consente di indicare se il provider di hosting verrà utilizzato in uno scenario con spazio di indirizzamento SIP condiviso. Deve essere impostato su **True** .
    
      - **HostsOCSUsers** consente di indicare se il provider di hosting viene utilizzato per ospitare account di Lync Server 2013. Deve essere impostato su **False** .
    
      - **ProxyFQDN** consente di specificare il nome di dominio completo (FQDN) del server proxy utilizzato dal provider di hosting, ad esempio **serverproxy.fabrikam.com** . Per avere tali informazioni, rivolgersi al provider di hosting. Questo valore non può essere modificato. Se il provider di hosting cambia server proxy, sarà necessario eliminare e quindi ricreare la voce per il provider.
    
      - **IsLocal** consente di indicare se il server proxy utilizzato dal provider di hosting è contenuto all'interno della topologia di Lync Server 2013. Deve essere impostato su **False**.

