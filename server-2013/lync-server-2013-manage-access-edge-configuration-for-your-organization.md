---
title: "Lync Server 2013: Gestire la configurazione Access Edge per l'organizzazione"
TOCTitle: Gestire la configurazione Access Edge per l'organizzazione
ms:assetid: 0145eb08-984f-4ecd-bf9c-364817619c2a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ552443(v=OCS.15)
ms:contentKeyID: 49299484
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestire la configurazione Access Edge per l'organizzazione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Questa documentazione è preliminare e soggetta a modifiche. Gli argomenti vuoti sono inclusi come segnaposto.

Dopo la distribuzione di uno o più server perimetrali, è necessario abilitare i tipi di dominio esterno o accesso provider, accesso utente remoto e accesso utente anonimo alle conferenze tramite il server perimetrali che verrà supportato per l'organizzazione.

Queste opzioni includono i tipi seguenti di accesso, che possono essere configurati nella pagina **Configurazione Access Edge** :

  - **Abilita federazione e connettività di messaggistica istantanea pubblica** : abilitare questa opzione se si desidera supportare l'accesso utente ai domini partner federati. Questa impostazione è applicabile alla federazione SIP e alla federazione XMPP configurate per gli ambiti globale, sito o utente nella pagina **Criteri di accesso esterno** . Per applicare le impostazioni di federazione, è necessario configurare il supporto per la federazione in entrambe le pagine.
    
    Esistono due opzioni che costituiscono impostazioni facoltative relative al modo in cui i partner federati vengono individuati e indicano se ai contatti verranno inviate le dichiarazioni di non responsabilità di archiviazione, ovvero notifiche che informano i contatti federati con cui si comunica che l'archiviazione è abilitata nella distribuzione e che i dettagli delle comunicazioni verranno archiviati.
    
      - **Abilita individuazione dominio partner** : se si seleziona questa opzione, verrà abilitata l'individuazione automatica dei domini con cui è possibile eseguire la federazione. Lync Server 2013 usa record DNS (Domain Name System) per provare a individuare domini non inclusi nell'elenco di domini consentiti, valutando automaticamente il traffico in arrivo dai partner federati individuati o bloccando quel traffico in base a livello di trust, quantità di traffico e impostazioni dell'amministratore. Se non si seleziona questa opzione, l'accesso degli utenti federati viene abilitato solo per gli utenti dei domini inclusi nell'elenco di domini consentiti. Indipendentemente dalla selezione di questa opzione, è possibile specificare se bloccare o consentire singoli domini, nonché limitare l'accesso a server specifici che eseguono il servizio Access Edge nel dominio federato. Per informazioni dettagliate, vedere [Configurare il supporto per i domini esterni consentiti in Lync Server 2013](lync-server-2013-configure-support-for-allowed-external-domains.md).
    
      - **Invia dichiarazione di non responsabilità relativa all'archiviazione ai partner federati** :se si seleziona questa opzione, verrà abilitato l'invio di un messaggio di dichiarazione di non responsabilità relativa all'archiviazione ai partner federati. Il messaggio comunica ai partner che i dettagli della comunicazione verranno registrati. Se si archiviano comunicazioni esterne con domini partner federati, è consigliabile abilitare la dichiarazione di non responsabilità relativa all'archiviazione per avvisare i partner che i dettagli relativi a messaggi e comunicazioni vengono archiviati dalla distribuzione. Per informazioni dettagliate sull'archiviazione, vedere [Definizione dei requisiti dell'organizzazione per l'archiviazione in Lync Server 2013](lync-server-2013-defining-your-requirements-for-archiving.md).

  - **Abilita accesso remoto utenti** : abilitare questa opzione se si vuole che gli utenti dell'organizzazione situati all'esterno del firewall, ad esempio telelavoratori e utenti in trasferta, possano connettersi a Lync Server. Per informazioni dettagliate, vedere [Abilitare o disabilitare l'accesso degli utenti remoti in Lync Server 2013](lync-server-2013-enable-or-disable-remote-user-access.md).

  - **Abilita accesso utente anonimo per le conferenze** : abilitare questa opzione se si vuole che gli utenti interni invitino utenti anonimi esterni alle conferenze organizzate. Se si abilita questa opzione, si autorizzeranno solo utenti anonimi per le conferenze. Per configurare l'esperienza e le opzioni relative alle conferenze che definiranno come e cosa potranno fare gli utenti con le conferenze e per configurare le opzioni per l'inclusione di utenti anonimi, vedere le informazioni dettagliate disponibili in [Creare o modificare l'esperienza utente di conferenza per un sito o un gruppo di utenti](https://technet.microsoft.com/it-it/library/gg429715\(v=ocs.15\)) e [Guida di riferimento alle impostazioni dei criteri di conferenza di Lync Server 2013](lync-server-2013-conferencing-policy-settings-reference.md).


> [!NOTE]
> Oltre ad abilitare il supporto per l'accesso utenti esterni, è necessario configurare anche criteri per controllare l'uso dell'accesso remoto utenti nell'organizzazione, prima che qualsiasi tipo di accesso utente esterno venga reso disponibile per gli utenti. Per informazioni dettagliate sulla creazione, la configurazione e l'applicazione di criteri per l'accesso utenti esterni, vedere <A href="lync-server-2013-manage-external-access-policy-for-your-organization.md">Gestire i criteri di accesso esterno per l'organizzazione in Lync Server 2013</A>.



**Visualizzazione delle informazioni sulla configurazione di Access Edge tramite i cmdlet di Windows PowerShell**

  - Le informazioni sulla configurazione di Access Edge possono essere visualizzate utilizzando Windows PowerShell e il cmdlet **Get-CsAccessEdgeConfiguration**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).
    
    Per visualizzare informazioni su tutte le impostazioni di configurazione di Access Edge, digitare il comando seguente in Lync Server Management Shell e quindi premere INVIO:
    
        Get-CsAccessEdgeConfiguration
    
    Verranno restituite informazioni simili alle seguenti:
    
        Identity                               : Global
        AllowAnonymousUsers                    : False
        AllowFederatedUsers                    : False
        AllowOutsideUsers                      : True
        BeClearingHouse                        : False
        EnablePartnerDiscovery                 : False
        EnableArchivingDisclaimer              : False
        EnableUserReplicator                   : True
        KeepCrlsUpToDateForPeers               : True
        MarkSourceVerifiableOnOutgoingMessages : True
        OutgoingTlsCountForFederatedPartners   : 4
        DiscoveredPartnerStandardRate          : 20
        EnableDiscoveredPartnerContactsLimit   : True
        MaxContactsPerDiscoveredPartner        : 1000
        DiscoveredPartnerReportPeriodMinutes   : 60
        MaxAcceptedCertificatesStored          : 1000
        MaxRejectedCertificatesStored          : 500
        CertificatesDeletedPercentage          : 20
        RoutingMethod                          : UseDnsSrvRouting

## Argomenti della sezione

  - [Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica in Lync Server 2013](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md)

  - [Abilitare o disabilitare l'individuazione dei partner della federazione in Lync Server 2013](lync-server-2013-enable-or-disable-discovery-of-federation-partners.md)

  - [Abilitare o disabilitare l'invio di una dichiarazione di non responsabilità relativa all'archiviazione ai partner federati in Lync Server 2013](lync-server-2013-enable-or-disable-sending-an-archiving-disclaimer-to-federated-partners.md)

  - [Abilitare o disabilitare l'accesso degli utenti remoti in Lync Server 2013](lync-server-2013-enable-or-disable-remote-user-access.md)

  - [Abilitare o disabilitare l'accesso degli utenti anonimi in Lync Server 2013](lync-server-2013-enable-or-disable-anonymous-user-access.md)

  - [Assegnare i criteri di conferenza per supportare gli utenti anonimi in Lync Server 2013](lync-server-2013-assign-conferencing-policies-to-support-anonymous-users.md)

