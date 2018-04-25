---
title: Prerequisiti per l'integrazione di Microsoft Lync Server 2013 e Microsoft Exchange Server 2013
TOCTitle: Prerequisiti per l'integrazione di Microsoft Lync Server 2013 e Microsoft Exchange Server 2013
ms:assetid: ea22beb9-c02e-47cb-836d-97a556969052
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721919(v=OCS.15)
ms:contentKeyID: 49887800
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Prerequisiti per l'integrazione di Microsoft Lync Server 2013 e Microsoft Exchange Server 2013

 

_**Ultima modifica dell'argomento:** 2014-04-22_

Per poter integrare Microsoft Lync Server 2013 e Microsoft Exchange Server 2013 è necessario prima verificare che tutti prerequisiti siano soddisfatti. Come intuibile, l'integrazione non può avere luogo se Exchange 2013 e Lync Server 2013 non sono completamente installati e funzionanti. Per informazioni dettagliate sull'installazione di Exchange, vedere la documentazione sulla pianificazione e la distribuzione di Exchange 2013 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268539\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268539%26clcid=0x410). Per informazioni dettagliate sull'installazione di Lync Server 2013, vedere la documentazione sulla pianificazione e la distribuzione all'indirizzo [http://go.microsoft.com/fwlink/?linkid=254806\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=254806%26clcid=0x410).

Quando i server sono installati e funzionanti, è necessario assegnare i certificati di autenticazione da server a server sia in Lync Server 2013 che in Exchange 2013. Tali certificati consentono a Lync Server e Exchange di scambiarsi informazioni e comunicare. Quando si installa Exchange 2013, viene creato un certificato autofirmato denominato Microsoft Exchange Server Auth Certificate. Tale certificato, che può essere trovato nell'archivio certificati del computer locale, consente l'autenticazione da server a server in Exchange 2013. Per informazioni dettagliate sull'assegnazione dei certificati in Exchange 2013, vedere "Configurare il flusso di posta e l'accesso client" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268540\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268540%26clcid=0x410).

Per Lync Server 2013 è possibile utilizzare un certificato di Lync Server esistente come certificato per l'autenticazione da server a server. Il certificato predefinito può ad esempio essere utilizzato anche come certificato OAuthTokenIssuer. Lync Server 2013 consente di utilizzare qualsiasi certificato server Web come certificato per l'autenticazione da server a server, a condizione che:

  - Il certificato includa il nome del dominio SIP nel campo Oggetto.

  - Lo stesso certificato sia configurato come certificato OAuthTokenIssuer in tutti i Front End Server.

  - Il certificato abbia una lunghezza di almeno 2048 bit.

Per informazioni dettagliate sui certificati per l'autenticazione da server a server in Microsoft Lync Server 2013, vedere [Assegnazione di un certificato di autenticazione da server a server a Microsoft Lync Server 2013](lync-server-2013-assigning-a-server-to-server-authentication-certificate-to-lync-server-2013.md).

Dopo l'assegnazione dei certificati è necessario configurare il servizio di individuazione automatica in Exchange 2013. In Exchange 2013 il servizio di individuazione automatica configura i profili utente e fornisce l'accesso ai servizi di Exchange quando gli utenti eseguono l'accesso al sistema. Gli utenti forniscono al servizio di individuazione automatica il proprio indirizzo di posta elettronica e la relativa password. A sua volta, il servizio fornisce all'utente informazioni quali:

  - Informazioni di connessione per la connettività sia interna che esterna a Exchange 2013.

  - Posizione del server della cassetta postale dell'utente.

  - URL per caratteristiche Outlook quali le informazioni di libero/occupato, la messaggistica unificata e la rubrica offline.

  - Impostazioni del server Outlook via Internet.

Per poter integrare Lync Server 2013 e Exchange 2013 è necessario prima configurare il servizio di individuazione automatica. Per verificare se il servizio di individuazione automatica è stato configurato, è possibile eseguire il comando seguente da Exchange Management Shell e leggere il valore della proprietà AutoDiscoverServiceInternalUri:

    Get-ClientAccessServer | Select-Object Name, AutoDiscoverServiceInternalUri | Format-List

Se il valore è vuoto, è necessario assegnare un URI al servizio di individuazione automatica. Solitamente l'URI sarà simile a questo:

    https://autodiscover.litwareinc.com/autodiscover/autodiscover.xml

Per assegnare l'URI di individuazione automatica, è possibile eseguire un comando simile a questo:

    Get-ClientAccessServer | Set-ClientAccessServer -AutoDiscoverServiceInternalUri "https://autodiscover.litwareinc.com/autodiscover/autodiscover.xml"

Per informazioni sul servizio di individuazione automatica, vedere "Informazioni sul servizio di individuazione automatica" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268542\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268542%26clcid=0x410).

Dopo la configurazione del servizio di individuazione automatica, è necessario modificare le impostazioni di configurazione OAuth di Lync Server. Questo assicura che Lync Server sappia dove trovare il servizio di individuazione automatica. Per modificare le impostazioni di configurazione OAuth in Lync Server 2013, eseguire il comando seguente in Lync Server Management Shell. Quando si esegue questo comando, assicurarsi di specificare l'URI del servizio di individuazione automatica in esecuzione nel server di Exchange e di utilizzare **autodiscover.svc** per puntare alla posizione del servizio anziché a **autodiscover.xml** (che punta al file XML utilizzato dal servizio):

    Set-CsOAuthConfiguration -Identity global -ExchangeAutodiscoverUrl "https://autodiscover.litwareinc.com/autodiscover/autodiscover.svc


> [!NOTE]
> Il parametro Identity nel comando precedente è facoltativo, perché Lync Server consente un'unica raccolta globale delle impostazioni di configurazione OAuth. Tra le altre cose, questo significa che è possibile configurare l'URL di individuazione automatica utilizzando questo comando leggermente più semplice:<BR>Set-CsOAuthConfiguration–ExchangeAutodiscoverUrl "https://autodiscover.litwareinc.com/autodiscover/autodiscover.svc"<BR>Per chi non avesse familiarità con la tecnologia, OAuth è un protocollo di autorizzazione standard utilizzato da numerosi siti Web di rilievo. Con OAuth, le credenziali e le password degli utenti non vengono passate da un computer all'altro. L'autenticazione e l'autorizzazione sono invece basate sullo scambio di token di sicurezza. Tali token consentono l'accesso a uno specifico set di risorse per un tempo specifico.



Oltre a configurare il servizio di individuazione automatica, è anche necessario creare un record DNS per il servizio che punti al proprio server Exchange. Se ad esempio il servizio di individuazione automatica è collocato in autodiscover.litwareinc.com sarà necessario creare un record DNS per autodiscover.litwareinc.com che si risolva nel nome di dominio qualificato del server Exchange (ad esempio, atl-exchange-001.litwareinc.com).

