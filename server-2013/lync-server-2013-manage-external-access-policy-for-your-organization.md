---
title: "Lync Server 2013: Gestire i criteri di accesso esterno per l'organizzazione"
TOCTitle: Gestire i criteri di accesso esterno per l'organizzazione
ms:assetid: 5571811e-34c8-443a-b94c-1ab5d4275581
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520995(v=OCS.15)
ms:contentKeyID: 49300564
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestire i criteri di accesso esterno per l'organizzazione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-10-07_

Dopo avere distribuito uno o più server perimetrali, è necessario abilitare i tipi di accesso esterno da supportare per l'organizzazione.

Per impostazione predefinita, non vi sono criteri configurati per supportare l'accesso utente esterno, inclusi l'accesso utente remoto e federato, anche se il supporto dell'accesso utente esterno è già stato abilitato per l'organizzazione. Per controllare l'uso dell'accesso utente esterno, è necessario configurare uno o più criteri, specificando il tipo di accesso utente esterno supportato per ogni criterio. Per la creazione e la configurazione sono disponibili gli ambiti di criteri seguenti. Per impostazione predefinita, i criteri globali possono essere creati ma non possono essere eliminati.

  - **Criteri globali** I criteri globali vengono creati quando si distribuiscono i server perimetrali. Per impostazione predefinita, nei criteri globali non è abilitata alcuna opzione di accesso utente esterno. Per supportare l'accesso utente esterno a livello globale, è possibile configurare i criteri globali per supportare uno o più tipi di opzioni di accesso utente esterno. I criteri globali si applicano a tutti gli utenti dell'organizzazione, ma i criteri sito e utente hanno la precedenza sui criteri globali. Se si eliminano i criteri globali, questi non vengono rimossi, ma ne vengono reimpostati i valori predefiniti.

  - **Criteri sito** È possibile creare e configurare uno o più criteri sito per limitare il supporto per l'accesso utente esterno a siti specifici. La configurazione dei criteri sito ha la precedenza sui criteri globali, ma solo per il sito specifico a cui i criteri si riferiscono. Se, ad esempio, si abilita l'accesso utente remoto nei criteri globali, è possibile specificare criteri sito tramite cui viene disabilitato l'accesso utente remoto per un sito specifico. Per impostazione predefinita, i criteri sito vengono applicati a tutti gli utenti del sito, ma è possibile assegnare criteri utente a un utente per sostituire l'impostazione dei criteri sito.

  - **Criteri utente** È possibile creare e configurare uno o più criteri utente per limitare il supporto per l'accesso utente remoto a utenti specifici. La configurazione dei criteri utente ha la precedenza sui criteri globali e sui criteri sito, ma solo per gli utenti specifici a cui sono assegnati i criteri utente. Se, ad esempio, si abilita l'accesso utente remoto nei criteri globali e nei criteri sito, è possibile specificare criteri utente tramite cui viene disabilitato l'accesso utente remoto e quindi assegnare tali criteri a utenti specifici. Se si creano criteri utente, è necessario applicarli a uno o più utenti affinché diventino attivi.

> [!IMPORTANT]  
> Le impostazioni criteri di Lync Server applicate a un determinato livello di criteri possono sostituire le impostazioni applicate a un altro livello di criteri. La precedenza dei criteri di Lync Server è la seguente: i criteri utente (maggiore influenza) sostituiscono i criteri sito e i criteri sito sostituiscono i criteri globali (minore influenza). Ciò significa che maggiore è la prossimità dell'impostazione criteri all'oggetto su cui influiscono i criteri, maggiore è l'influenza su tale oggetto.

Queste opzioni includono i tipi di accesso esterno seguenti:

  - **Abilita comunicazioni con utenti federati**    Abilitare questa opzione se si desidera supportare l'accesso utente ai domini dei partner federati. Questa impostazione consente agli utenti di comunicare con altri domini federati SIP e con provider ospitati come Microsoft Office 365. Se si seleziona questa opzione, è possibile selezionare l'opzione che consente la comunicazione con i domini federati XMPP.
    
    Dopo aver selezionato **Abilita comunicazioni con utenti federati** è possibile selezionare, se si vuole, **Abilita le comunicazioni con gli utenti federati XMPP** . La federazione XMPP è una federazione con organizzazioni che usano il protocollo XMPP (eXtensible Messaging and Presence Protocol).
    

    > [!NOTE]
    > Se si abilita la federazione XMPP, è necessario anche selezionare la distribuzione della <STRONG>Federazione XMPP</STRONG> nella sezione di configurazione dei pool di server perimetrali del Generatore di topologie. Una configurazione che abilita la federazione XMPP distribuisce un proxy XMPP nel server perimetrale e un gateway XMPP nel Front End Server.



  - **Abilita comunicazioni con utenti remoti**    Abilitare questa opzione se si vuole consentire la connessione a Lync Server via Internet agli utenti dell'organizzazione che si trovano all'esterno del firewall, come telelavoratori e utenti in viaggio.

  - **Abilita comunicazioni con utenti pubblici**    Abilitare questa opzione se si vuole consentire agli utenti interni di comunicare con i contatti dei provider di messaggistica istantanea pubblici, ad esempio quelli forniti da Windows Live, Yahoo\! e America Online (AOL).
    
    > [!IMPORTANT]  
    > <ul>    
> <li><p>Dal 1 settembre 2012, la licenza di sottoscrizione utenti per la connettività di messaggistica istantanea pubblica di Microsoft Lync (“PIC USL”) non è più disponibile per l'acquisto per i nuovi contratti o quelli in fase di rinnovo. I clienti con licenze attive potranno continuare a eseguire la federazione con Yahoo! Messenger fino alla data di chiusura del servizio. Giugno 2014 è la data di fine servizio annunciata per Yahoo! e AOL. Per informazioni dettagliate, vedere <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Supporto della connettività per messaggistica istantanea pubblica in Lync Server 2013</a>.</p></li>    
> 
> <li><p>La licenza PIC USL è una licenza di sottoscrizione di tipo mensile per utente, richiesta per la federazione di Lync Server o Office Communications Server con Yahoo! Messenger. La capacità di Microsoft di fornire questo servizio dipende dal supporto offerto da Yahoo! e il contratto sottostante è in fase di chiusura.</p></li>    
> 
> 
> <li><p>Oggi più che mai, Lync è un potente strumento per la connessione tra diverse organizzazioni e con utenti di tutto il mondo. La federazione con Windows Live Messenger non richiede ulteriori licenze per utente/dispositivo in aggiunta alla licenza CAL Standard per Lync. La federazione con Skype verrà aggiunta a questo elenco, consentendo agli utenti di Lync di raggiungere centinaia di milioni di persone tramite messaggistica istantanea e comunicazioni vocali.</p></li>    </ul>



> [!NOTE]
> Oltre ad abilitare il supporto dell'accesso a utenti esterni, è inoltre necessario configurare i criteri per controllare l'uso dell'accesso agli utenti esterni nell'organizzazione prima che sia disponibile qualsiasi tipo di accesso esterno per gli utenti. Per informazioni dettagliate sulla creazione, la configurazione e l'applicazione di criteri per l'accesso agli utenti esterni, vedere <A href="lync-server-2013-enable-or-disable-remote-user-access.md">Abilitare o disabilitare l'accesso degli utenti remoti in Lync Server 2013</A>.



**Per visualizzare i criteri di accesso esterno tramite i cmdlet di Windows PowerShell**

  - Per visualizzare i criteri di accesso esterno, è possibile utilizzare Lync Server Management Shell e il cmdlet **Get-CsExternalAccessPolicy**. È possibile eseguire questo cmdlet da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).
    
    Per visualizzare informazioni su tutti i criteri di accesso esterno, digitare il comando seguente in Lync Server Management Shell e quindi premere INVIO:
    
        Get-CsExternalAccessPolicy
    
    Questo comando restituisce informazioni simili alle seguenti:
    
        Identity                          : Global
        Description                       :
        EnableFederationAccess            : False
        EnableXmppAccess                  : False
        EnablePublicCloudAccess           : False
        EnablePublicCloudAudioVideoAccess : False
        EnableOutsideAccess               : False

## Argomenti della sezione

  - [Configurare criteri per controllare l'accesso utente federato in Lync Server 2013](lync-server-2013-configure-policies-to-control-federated-user-access.md)

  - [Configurare criteri per controllare l'accesso utente federato XMPP in Lync Server 2013](lync-server-2013-configure-policies-to-control-xmpp-federated-user-access.md)

  - [Configurare criteri per controllare l'accesso degli utenti remoti in Lync Server 2013](lync-server-2013-configure-policies-to-control-remote-user-access.md)

  - [Configurare criteri per controllare l'accesso degli utenti pubblici in Lync Server 2013](lync-server-2013-configure-policies-to-control-public-user-access.md)

  - [Assegnare criteri di accesso per gli utenti esterni a un utente abilitato per Lync in Lync Server 2013](lync-server-2013-assign-an-external-user-access-policy-to-a-lync-enabled-user.md)

  - [Reimpostazione o eliminazione dei criteri di accesso esterno degli utenti in Lync Server 2013](lync-server-2013-resetting-or-deleting-external-user-access-policies.md)

