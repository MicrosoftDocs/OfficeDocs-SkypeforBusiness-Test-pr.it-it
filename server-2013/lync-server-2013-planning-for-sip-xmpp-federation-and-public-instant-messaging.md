---
title: Pianificazione per SIP, federazione XMPP e messaggistica istantanea pubblica in Lync Server 2013
TOCTitle: Pianificazione per SIP, federazione XMPP e messaggistica istantanea pubblica in Lync Server 2013
ms:assetid: 3b234d92-b9ff-4b1d-910e-084c6f17e751
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204825(v=OCS.15)
ms:contentKeyID: 49300260
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione per SIP, federazione XMPP e messaggistica istantanea pubblica in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-10-28_

È possibile configurare i server perimetrali in modo da consentire agli utenti interni ed esterni di accedere ai contatti di organizzazioni o servizi partner. Le federazioni, ovvero questi accordi tra partner, possono rendere disponibile qualsiasi contatto dell'organizzazione alla federazione partner e viceversa:

  - Messaggistica istantanea e presenza

  - Collaborazione e servizi di conferenza, ad esempio Web Conferencing

  - Conferenze audio, video o entrambe

In alcuni casi la comunicazione, ad esempio la messaggistica istantanea e la presenza tra Microsoft Lync Server 2013 e un contatto XMPP (Extensible Messaging and Presence Protocol) è solo di tipo peer-to-peer, ovvero supporta solo l'utente e il contatto del partner federato. In altri casi, come tra Lync Server, Lync Server 2010 e una federazione di Lync Server 2013, è possibile invitare più partecipanti a partecipare alla conversazione.

## Federazione di Lync Server e Office Communications Server

La federazione tra Microsoft Lync Server 2013, Lync Server 2010 e Office Communications Server supporta le comunicazioni peer-to-peer e tra più parti. È possibile effettuare l'escalation delle conversazioni peer-to-peer a conversazioni tra più parti, consentendo l'esecuzione di riunioni ad hoc. Le riunioni, che possono essere conferenze Web o conferenze audio/video, possono essere pianificate in modo da includere contatti all'interno dell'organizzazione e contatti del partner con cui si attua la federazione.

La federazione è stata introdotta per la prima volta in Microsoft Office Live Communications Server 2005, in cui è supportato un tipo di federazione, la federazione diretta, che richiede la conoscenza del dominio SIP (Session Initiation Protocol) del partner della federazione e il nome di dominio completo del server perimetrale del partner. In Live Communications Server 2005 con SP1 sono stati introdotti ulteriori tipi di federazione, che richiedono tutti la pubblicazione di record SRV DNS da parte del partner federato per poterne individuare il server perimetrale. La terminologia utilizzata in tale versione è la seguente:

  - *Federazione avanzata aperta*: viene accettato qualsiasi nome di dominio SIP e viene utilizzato il record SRV DNS per individuare il server perimetrale del partner.

  - *Federazione avanzata*: il nome di dominio SIP del partner viene configurato come partner della federazione dell'organizzazione e viene utilizzato il record SRV DNS per individuare il server perimetrale del partner.

  - *Federazione diretta*: vengono configurati il nome di dominio SIP del partner e il nome di dominio completo del server perimetrale del partner.

  - *Elenco dei server consentiti*: viene accettato qualsiasi dominio e viene utilizzato il record SRV DNS per individuare il server perimetrale di un provider di hosting o di un provider di connettività per messaggistica istantanea pubblica.

In Microsoft Office Communications Server 2007 è stata introdotto un sistema di denominazione aggiornato per i tipi di federazione per definire in modo ottimale ogni tipo di federazione effettivamente eseguito:

  - La federazione avanzata aperta è stata denominata *dominio partner individuato*.

  - La federazione avanzata è stata denominata *dominio partner consentito*.

  - La federazione diretta è stata denominata *server partner consentito*.

  - L'elenco dei server consentiti è stato denominato *provider di hosting* e *provider di servizi di messaggistica istantanea pubblica*.

In Microsoft Lync Server 2010 è stata introdotta una definizione più circoscritta del provider di hosting in conformità con Microsoft Lync Online 2010 e Microsoft Office 365 soggetta allo stesso elenco di membri consentiti definito dal tipo di federazione dominio partner consentito.

Abilitando la federazione tra Microsoft Lync Server 2013, Lync Server 2010 e Office Communications Server vengono utilizzati i server perimetrali e i proxy inversi per applicare le regole e i domini partner consentiti che sono stati definiti. Dal punto di vista della pianificazione, la federazione con altri Lync Server e Office Communications Server prevede i requisiti seguenti:

  - Abilitare la federazione in Generatore di topologie. Per informazioni dettagliate, vedere [Configurazione di federazione SIP, federazione XMPP e messaggistica istantanea pubblica in Lync Server 2013](lync-server-2013-configuring-sip-federation-xmpp-federation-and-public-instant-messaging.md) nella documentazione relativa alla distribuzione.

  - Determinare i propri requisiti per l'individuazione del dominio federato:
    
      -   
        Per la configurazione manuale della federazione, è necessario disporre del nome di dominio completo (FQDN) del server perimetrale del partner e del nome di dominio, o nome di dominio online, che viene immesso nel Pannello di controllo di Lync Server, in **Federazione e accesso esterno**, **Domini federati SIP**. Creare nuovi criteri facendo clic su **Nuovo** oppure modificare criteri esistenti facendo clic su **Modifica** in modo da consentire o bloccare i domini in base al nome di dominio completo.
        

        > [!WARNING]
        > La configurazione manuale del server perimetrale di un partner della federazione è soggetta a errore qualora il partner modifichi l'indirizzo IP del server perimetrale.

        

        > [!NOTE]
        > Per specificare un nuovo dominio, in <STRONG>Domini federati SIP</STRONG> impostare il valore per <STRONG>Nome di dominio (o FQDN)</STRONG> per Microsoft Lync Online e Microsoft Office 365. Per Microsoft Lync Server 2013, Lync Server 2010 e Office Communications Server è necessario inoltre specificare un valore per <STRONG>Servizio Access Edge (FQDN)</STRONG>.

    
      -   
        Per la federazione di partner individuati, in cui i partner possono individuare il server perimetrale, creare un record SRV nel DNS esterno, ad esempio \_sipfederationtls.\_tcp.contoso.com, che punta alla porta 5061 e al record (A) host del server perimetrale.
        
        > [!important]  
        > Se si supportano client Microsoft Lync Mobile in Windows Phone o Apple iPhone, iPad o altri dispositivi Apple e si utilizza il servizio notifica Push o il servizio notifica Push, è necessario eseguire la pianificazione di record SRV di tipo _sipfederationtls._tcp. <em>&lt;dominio SIP&gt;</em> per ogni dominio SIP nei client Lync Mobile. In Android e Nokia Symbian Lync Mobile non viene utilizzata la notifica push e non è previsto questo requisito.

  - Configurare criteri di accesso degli utenti esterni per il supporto dei domini federati.

  - Aprire le porte del firewall per il protocollo SIP (Session Initiation Protocol), le conferenze Web e le conferenze audio/video per supportare la federazione o i contatti abilitati. Per informazioni dettagliate, vedere [Determinare i requisiti di porte e firewall A/V esterni per Lync Server 2013](lync-server-2013-determine-external-a-v-firewall-and-port-requirements.md).

Le informazioni seguenti consentono di definire i requisiti di certificati, porte/protocolli e DNS per la federazione con Microsoft Lync Server 2013 e Lync Server 2010.

La pianificazione dei requisiti di certificati, firewall, porte/protocolli e DNS è in genere un processo semplice se sono stati già pianificati e distribuiti server perimetraliMicrosoft Lync Server 2013. Poiché la federazione è una funzionalità aggiuntiva che utilizza il server perimetrale esistente, i requisiti di pianificazione sono normalmente già soddisfatti con la pianificazione e la distribuzione del server perimetrale. È consigliabile utilizzare le tabelle seguenti per verificare che i requisiti vengano soddisfatti e apportare eventuali modifiche a porte/protocolli e DNS in base alle esigenze.

> [!important]  
> Se si dispone di un pool di server perimetrali e si attua la federazione con partner Lync Server 2013 o Lync Server 2010, è possibile utilizzare il bilanciamento del carico DNS o dispositivi di bilanciamento del carico hardware sulle interfacce interne ed esterne dei server perimetrali. Se si attua la federazione con Office Communications Server 2007 oppure Office Communications Server 2007 R2, il bilanciamento del carico hardware garantirà il supporto per il failover in caso di errore di un server perimetrale. Office Communications Server 2007 e Office Communications Server 2007 R2 non supportano il bilanciamento del carico DNS. I server perimetrali partner stabiliranno una comunicazione con il primo server perimetrale del pool che risponderà. In caso di errore del server perimetrale, non verrà eseguito automaticamente il failover.

I requisiti dei certificati in genere vengono soddisfatti mediante la pianificazione di certificati per il server perimetrale selezionato o il piano di server perimetrale in pool.

## Connettività per messaggistica istantanea pubblica

La connettività per messaggistica istantanea pubblica è una classe di federazione, configurata per consentire agli utenti interni ed esterni di Lync Server 2013 di aggiungere contatti dalle origini seguenti:

  - Contatti di Messenger

  - Contatti di Yahoo\!

  - Contatti di AOL (America Online)

> [!important]  
> <ul>
> <li><p>Dal 1 settembre 2012, la licenza di sottoscrizione utente per Connettività per messaggistica istantanea pubblica di Microsoft Lync (&quot;PIC USL&quot;) non è più disponibile per l'acquisto per i nuovi contratti o quelli in fase di rinnovo. I clienti con licenze attive potranno continuare a eseguire la federazione con Yahoo! Messenger fino alla data di chiusura del servizio (la data esatta non è ancora stata definita, ma non sarà anteriore a giugno 2013).</p></li>
> 
> <li><p>La licenza PIC USL è una licenza di sottoscrizione di tipo mensile per utente, richiesta per la federazione di Lync Server o Office Communications Server con Yahoo! Messenger. La possibilità di Microsoft di fornire questo servizio dipende dal supporto offerto da Yahoo! e il contratto sottostante non verrà rinnovato.</p></li>
> 
> 
> <li><p>Oggi più che mai, Lync è un potente strumento per la connessione tra diverse organizzazioni e con utenti in tutto il mondo. La federazione con Windows Live Messenger non richiede ulteriori licenze per utente/dispositivo in aggiunta alla licenza CAL Lync Standard. La federazione con Skype verrà aggiunta a questo elenco per consentire agli utenti di Lync di raggiungere centinaia di milioni di persone tramite messaggistica istantanea e comunicazioni vocali.</p></li></ul>


Per questa classe di federazione è necessario tenere conto delle considerazioni seguenti per la pianificazione:

  - Gli utenti di Windows Live Messenger possono stabilire comunicazioni audio/video peer-to-peer con gli utenti di Lync Server 2013 oltre a conversazioni istantanee. I server perimetrali devono soddisfare requisiti specifici per porte e protocolli. Per informazioni dettagliate, vedere [Determinare i requisiti di porte e firewall A/V esterni per Lync Server 2013](lync-server-2013-determine-external-a-v-firewall-and-port-requirements.md)

  - Per la messaggistica istantanea di Yahoo\! non sono previsti requisiti speciali, a parte quelli in genere utilizzati per la pianificazione e la distribuzione del server perimetrale tipico per la federazione.

  - Per AOL è richiesto che il certificato del server perimetrale assegnato al servizio Access Edge sia configurato per l'utilizzo chiavi avanzato (EKU) del client.

## Federazione di XMPP (Extensible Messaging and Presence Protocol)

Le versioni precedenti di Lync Server e Office Communications Server includono un gateway XMPP (Extensible Messaging and Presence Protocol) che può essere distribuito come ruolo server separato per consentire la federazione con distribuzioni XMPP. In Microsoft Lync Server 2013, la funzionalità XMPP può essere distribuita come funzionalità. La funzionalità XMPP viene installata in due parti: un proxy XMPP che viene eseguito nel server perimetrale e il gateway XMPP che viene eseguito nei Front End Server.

La distribuzione e la configurazione di XMPP sono illustrate in [Distribuzione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-deploying-external-user-access.md). Per pianificare il supporto di XMPP in un'organizzazione, occorre definire le regole delle porte e del protocollo nel firewall, la configurazione dei certificati e l'aggiunta dei record DNS. Negli argomenti seguenti di questa sezione vengono riepilogate le informazioni necessarie per pianificare correttamente la federazione XMPP per la distribuzione.

> [!important]  
> La funzionalità XMPP di Lync Server 2013 è testata e supportata da Microsoft per la federazione di messaggistica istantanea con Google Talk. Per altri sistemi XMPP, contattare il fornitore di terze parti per verificare l'eventuale supporto della federazione con Lync Server 2013 e per indicazioni per la distribuzione o la risoluzione dei problemi.

> [!important]  
> La federazione XMPP non è supportata per gli utenti ospitati in Survivable Branch Appliance. Lo stesso vale per la visualizzazione di informazioni sulla presenza e lo scambio di messaggi istantanei.

Negli argomenti seguenti sono fornite informazioni per la definizione di certificati, porte del firewall e voci DNS per i tipi di scenari di federazione supportati.

  -   
    [Riepilogo dei certificati - SIP, federazione di XMPP e messaggistica istantanea pubblica](lync-server-2013-certificate-summary-sip-xmpp-federation-and-public-instant-messaging.md)

  -   
    [Riepilogo porte: SIP, federazione di XMPP e messaggistica istantanea pubblica](lync-server-2013-port-summary-sip-xmpp-federation-and-public-instant-messaging.md)

  -   
    [Riepilogo DNS: SIP, federazione di XMPP e messaggistica istantanea pubblica](lync-server-2013-dns-summary-sip-xmpp-federation-and-public-instant-messaging.md)

## Vedere anche

#### Attività

[Configurare criteri per controllare l'accesso utente federato in Lync Server 2013](lync-server-2013-configure-policies-to-control-federated-user-access.md)  

#### Concetti

[Scenari per l'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-scenarios-for-external-user-access.md)  
[Determinare i requisiti di porte e firewall A/V esterni per Lync Server 2013](lync-server-2013-determine-external-a-v-firewall-and-port-requirements.md)  
[Determinare i requisiti di DNS per Lync Server 2013](lync-server-2013-determine-dns-requirements.md)  

#### Ulteriori risorse

[Gestire la configurazione Access Edge per l'organizzazione in Lync Server 2013](lync-server-2013-manage-access-edge-configuration-for-your-organization.md)  
[Gestire i domini federati SIP per l'organizzazione in Lync Server 2013](lync-server-2013-manage-sip-federated-domains-for-your-organization.md)  
[Gestire i provider federati SIP per l'organizzazione in Lync Server 2013](lync-server-2013-manage-sip-federated-providers-for-your-organization.md)

