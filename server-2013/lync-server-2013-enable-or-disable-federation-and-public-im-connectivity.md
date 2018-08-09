---
title: "Lync Server 2013: Abilita/disabilita federaz. e connettività per i messaggi"
TOCTitle: Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica
ms:assetid: 8ec58f4b-9f6d-47b4-a187-d18a83fe4577
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182549(v=OCS.15)
ms:contentKeyID: 49301292
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-06-24_

Il supporto della federazione è necessario per consentire agli utenti che dispongono di un account con un'organizzazione cliente o partner attendibile, inclusi i domini partner e gli utenti di provider di messaggistica istantanea pubblica supportati, di collaborare con gli utenti all'interno dell'organizzazione. La federazione è anche necessaria per poter utilizzare un provider di servizi di Exchange ospitato in modo da offrire il servizio di segreteria telefonica agli utenti di VoIP aziendale le cui cassette postali si trovano su un servizio di Exchange ospitato quale Microsoft Exchange Online. Dopo aver stabilito una relazione di trust con questi domini esterni, è possibile autorizzare gli utenti di tali domini ad accedere alla distribuzione e partecipare alle comunicazioni di Lync Server. La relazione di trust è denominata federazione e non è correlata a una relazione di trust di Active Directory né dipende da essa.

Per supportare l'accesso da parte degli utenti dei domini federati, è necessario abilitare la federazione. Se si abilita la federazione per la propria organizzazione, è anche necessario specificare se si desidera implementare le opzioni seguenti:

  - **Abilita individuazione dominio partner** . Se si abilita questa opzione, Lync Server utilizza i record DNS (Domain Name System) per provare a individuare i domini non elencati nell'elenco dei domini consentiti, valutando automaticamente il traffico in arrivo dai partner federati individuati e limitando o bloccando tale traffico in base al livello di trust, al volume di traffico e alle impostazioni dell'amministratore. Se non si seleziona questa opzione, l'accesso degli utenti federati viene abilitato solo per gli utenti dei domini inclusi nell'elenco di domini consentiti. Indipendentemente dalla selezione di questa opzione, è possibile specificare se bloccare o consentire singoli domini, nonché limitare l'accesso a server specifici che eseguono il servizio Access Edge nel dominio federato. Per informazioni dettagliate sul controllo dell'accesso da parte dei domini federati, vedere [Configurare il supporto per i domini esterni consentiti in Lync Server 2013](lync-server-2013-configure-support-for-allowed-external-domains.md).

  - **Invia dichiarazione di non responsabilità relativa all'archiviazione ai partner federati** . Questa opzione consente di inviare una dichiarazione ai partner federati per informarli che nella distribuzione è usata l'archiviazione. Se si supporta l'archiviazione delle comunicazioni esterne con i domini partner federati, è necessario abilitare la notifica della dichiarazione di non responsabilità relativa all'archiviazione per avvisare i partner che i loro messaggi vengono archiviati.

Se successivamente si desidera impedire, in modo temporaneo o permanente, l'accesso degli utenti dei domini federati, è possibile disabilitare la federazione per l'organizzazione. Attenersi alla procedura descritta in questa sezione per abilitare o disabilitare l'accesso degli utenti federati per l'organizzazione, nonché per specificare le opzioni di federazione appropriate da supportare per l'organizzazione.


> [!NOTE]
> L'abilitazione della federazione per l'organizzazione consente di specificare solo che i server che eseguono il servizio Access Edge supportano il routing ai domini federati. Gli utenti dei domini federati non possono partecipare alle conferenze o alla messaggistica istantanea all'interno dell'organizzazione finché non si procede anche alla configurazione di almeno un criterio per il supporto dell'accesso degli utenti federati. Gli utenti dei provider di servizi di messaggistica istantanea pubblica non possono partecipare alle conferenze o alla messaggistica istantanea nell'organizzazione finché non si procede anche alla configurazione di almeno un criterio per il supporto della connettività di messaggistica istantanea pubblica. Lync Server non può utilizzare un servizio di Exchange ospitato per fornire servizi di risposta alle chiamate, Outlook Voice Access (inclusa la segreteria telefonica) o servizi con operatori automatici agli utenti le cui cassette postali si trovano su un servizio di Exchange ospitato finché non si procede anche alla configurazione di un criterio per la segreteria telefonica ospitata che fornisca informazioni sul routing. Per informazioni dettagliate sulla configurazione dei criteri per le comunicazioni con gli utenti dei domini federati in altre organizzazioni, vedere <A href="lync-server-2013-manage-sip-federated-domains-for-your-organization.md">Gestire i domini federati SIP per l'organizzazione in Lync Server 2013</A> nella documentazione sulle operazioni. Se, inoltre, si desidera supportare le comunicazioni con gli utenti dei provider di servizi di messaggistica istantanea, è necessario configurare i criteri per il relativo supporto nonché configurare il supporto per i singoli provider di servizi desiderati. Per informazioni dettagliate, vedere <A href="lync-server-2013-manage-sip-federated-providers-for-your-organization.md">Gestire i provider federati SIP per l'organizzazione in Lync Server 2013</A> nella documentazione relativa alle operazioni. Per informazioni dettagliate sulla creazione di un criterio per la segreteria telefonica ospitata, vedere <A href="lync-server-2013-manage-hosted-voice-mail-policies.md">Gestire i criteri di segreteria telefonica ospitata in Lync Server 2013</A> nella documentazione relativa alla distribuzione.



## Per abilitare o disabilitare l'accesso degli utenti federati per l'organizzazione

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Accesso utente esterno** e quindi su **Configurazione Access Edge** .

4.  Nella pagina **Configurazione Access Edge** fare clic su **Globale** , fare clic su **Modifica** e quindi su **Mostra dettagli** .

5.  In **Modifica configurazione Access Edge** eseguire una delle operazioni seguenti:
    
      - Per abilitare l'accesso degli utenti federati per l'organizzazione, selezionare la casella di controllo **Abilita comunicazioni con utenti federati** .
    
      - Per disabilitare l'accesso degli utenti federati per l'organizzazione, deselezionare la casella di controllo **Abilita comunicazioni con utenti federati** .

6.  Se è stata selezionata la casella di controllo **Abilita comunicazioni con utenti federati** , eseguire le operazioni seguenti:
    
    1.  Se si desidera supportare l'individuazione automatica dei domini partner, selezionare la casella di controllo **Abilita individuazione dominio partner** .
    
    2.  Se l'organizzazione supporta l'archiviazione delle comunicazioni esterne, selezionare la casella di controllo **Invia dichiarazione di non responsabilità relativa all'archiviazione ai partner federati** .

7.  Fare clic su **Commit** .

Per consentire agli utenti federati di collaborare con gli utenti nella distribuzione di Lync Server 2013, è anche necessario configurare almeno un criterio di accesso esterno per il supporto dell'accesso degli utenti federati. Per informazioni dettagliate, vedere [Configurare criteri per controllare l'accesso utente federato in Lync Server 2013](lync-server-2013-configure-policies-to-control-federated-user-access.md) nella documentazione relativa alla distribuzione o nella documentazione relativa alle operazioni. Per controllare l'accesso per specifici domini federati, vedere [Configurare il supporto per i domini esterni consentiti in Lync Server 2013](lync-server-2013-configure-support-for-allowed-external-domains.md) nella documentazione relativa alla distribuzione o nella documentazione relativa alle operazioni.

## Abilitazione o disabilitazione della federazione e della connettività per la messaggistica istantanea pubblica mediante cmdlet di Windows PowerShell

La federazione e la connettività IM pubblica possono essere gestite anche mediante Windows PowerShell e il cmdlet Set-CsAccessEdgeConfiguration. Questo cmdlet può essere eseguito dalla Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per abilitare la federazione e la connettività per la messaggistica istantanea pubblica

  - Per abilitare la federazione e la connettività IM pubblica, impostare il valore della proprietà **AllowFederatedUsers** su True ($True):
    
        Set-CsAccessEdgeConfiguration -AllowFederatedUsers $True

## Per disabilitare la federazione e la connettività per la messaggistica istantanea pubblica

  - Per disabilitare la federazione e la connettività IM pubblica, impostare il valore della proprietà **AllowFederatedUsers** su False ($False):
    
        Set-CsAccessEdgeConfiguration -AllowFederatedUsers $False

