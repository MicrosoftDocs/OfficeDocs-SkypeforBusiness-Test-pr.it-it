---
title: Gestione dell'autenticazione da server a server (Oauth) e applicazioni partner in Lync Server 2013
TOCTitle: Gestione dell'autenticazione da server a server (Oauth) e applicazioni partner in Lync Server 2013
ms:assetid: 38848373-c8c6-4097-bf7f-699fe471348d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204817(v=OCS.15)
ms:contentKeyID: 49300208
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestione dell'autenticazione da server a server (Oauth) e applicazioni partner in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-05-14_

Microsoft Lync Server 2013 deve riuscire a comunicare in modo facile e sicuro con altre applicazioni e prodotti server. È ad esempio possibile configurare Lync Server 2013 in modo che i dati dei contatti e/o o i dati di archiviazione vengano archiviati in Microsoft Exchange Server 2013. Questa operazione può tuttavia essere eseguita solo se Lync Server e Exchange riescono a comunicare tra loro in modo sicuro. Analogamente, è possibile pianificare una conferenza Lync Server da Microsoft SharePoint Server. Anche questa operazione può tuttavia essere eseguita solo se i due server (SharePoint e Lync Server) sono reciprocamente attendibili. Sebbene sia possibile usare un solo meccanismo di autenticazione per la comunicazione tra Lync ed Exchange e un meccanismo separato per la comunicazione tra Lync e SharePoint, è preferibile usare un approccio più efficiente, ovvero un metodo standardizzato per tutte le operazioni di autorizzazione e autenticazione server-server.

L'approccio di Lync Server 2013 consiste nell'uso di un unico metodo standardizzato per l'autenticazione server-server. Per la release 2013, Lync Server 2013 e altri prodotti Microsoft Server, inclusi Exchange 2013 e Microsoft SharePoint Server, supportano il protocollo OAuth (Open Authorization) per l'autorizzazione e l'autenticazione server-server. Con OAuth, un protocollo di autorizzazione standard usato da diversi siti Web principali, le password e le credenziali utente non vengono trasferite da un computer all'altro. L'autorizzazione e l'autenticazione si basano, invece, sullo scambio di token di sicurezza che garantiscono l'accesso a un insieme di risorse per un periodo di tempo specifico.

L'autenticazione OAuth coinvolge generalmente tre parti: un server di autorizzazione singolo e le due aree che devono comunicare tra loro. È possibile anche effettuare l'autenticazione server-server senza usare un server di autorizzazione. Questa procedura verrà descritta più avanti in questo documento. I token di sicurezza vengono rilasciati dal server di autorizzazione (noto anche come server del token di sicurezza) per le due aree che devono comunicare tra loro. Tali token verificano che le comunicazioni che hanno origine da un'area siano attendibili per l'altra area. Ad esempio il server di autorizzazione potrebbe rilasciare token che verificano che gli utenti di un'area specifica di Lync Server 2013 riescano ad accedere a un'area specifica di Exchange 2013 e viceversa.


> [!NOTE]
> Un'area non è altro che un contenitore di sicurezza. Per impostazione predefinita, Lync Server 2013 usa come area OAuth il dominio SIP predefinito dell'utente.



Lync Server 2013 supporta tre scenari di autenticazione server-server. Con Lync Server 2013 è possibile:

  - Configurare l'autenticazione server-server tra un'installazione locale di Lync Server 2013 e un'installazione locale di Exchange 2013 e/o Microsoft SharePoint Server.

  - Configurare l'autenticazione server-server tra una coppia di componenti di Office 365 (ad esempio tra Microsoft Exchange e Microsoft Lync Server o tra Microsoft Lync Server e Microsoft SharePoint).

  - Configurare l'autenticazione server-server in un ambiente cross-premise, ovvero l'autenticazione server-server tra un server locale e un componente di Office 365.

Si osservi come attualmente solo Exchange 2013, SharePoint Server e Lync Server 2013 supportano l'autenticazione server-server. Se non è in esecuzione uno di questi server, non sarà possibile eseguire l'implementazione completa dell'autenticazione OAuth.

Andrebbe inoltre sottolineato che non è necessario usare l'autenticazione server-server: questo tipo di autenticazione non è richiesto per la distribuzione di Lync Server 2013. Se non è necessario che Lync Server 2013 comunichi con altri server (come Exchange 2013), l'autenticazione server-server non è necessaria.

Tale autenticazione è invece richiesta se si vuole usare alcune nuove funzionalità di Lync Server, come l'"archivio contatti unificato". Con questa funzionalità, le informazioni sui contatti di Lync Server 2013 vengono archiviate in Exchange 2013 anziché in Lync Server. Ciò consente agli utenti di tenere un unico gruppo di contatti cui possono facilmente accedere da Lync, Microsoft Outlook o Microsoft Outlook Web Access. Dal momento che l'archivio contatti unificato richiede la condivisione di informazioni tra Lync Server 2013 e Exchange 2013, è necessario usare l'autenticazione server-server per distribuire la funzionalità. Questa autenticazione è richiesta anche se si decide di usare l'archiviazione di Exchange, in cui le trascrizioni delle sessioni di messaggistica istantanea vengono salvate come messaggi di posta elettronica di Exchange 2013 anziché come record di database singoli.

Per consentire alla versione di Office 365 di Lync Server di comunicare con la rispettiva controparte Exchange, Lync Server 2013 deve prima ottenere un token di sicurezza dal server di autorizzazione. Lync Server usa quindi questo token per identificare se stesso in Exchange. La versione di Office 365 di Exchange deve seguire la stessa procedura per comunicare con Lync Server 2013.

Per l'autenticazione server-server in locale tra due server Microsoft, non è invece necessario usare un server di token di terze parti. I prodotti server come Lync Server 2013 e Exchange 2013 sono dotati di un server di token incorporato che può essere usato per l'autenticazione con altri server Microsoft (come il server di SharePoint) che supportano l'autenticazione server-server. Ad esempio, Lync Server 2013 può autonomamente emettere e firmare un token di sicurezza e usarlo per comunicare con Exchange 2013. In un caso del genere non è necessario un server di token di terze parti.

Per poter configurare l'autenticazione server-server per un'implementazione in locale di Lync Server 2013, è necessario eseguire due operazioni:

  - Assegnare un certificato all'autorità emittente di token incorporata di Lync Server.

  - Configurare come "applicazione partner" il server con cui comunicherà Lync Server 2013. Ad esempio, per consentire la comunicazione tra Lync Server 2013 e Exchange 2013, è necessario configurare Exchange come applicazione partner.


> [!NOTE]
> Per "applicazione partner " si intende qualsiasi applicazione con cui Lync Server 2013 può scambiare direttamente i token di sicurezza senza dover ricorrere a un server di token di sicurezza di terze parti.



Si noti che OAuth è una parte essenziale del prodotto e non può essere disabilitata o rimossa.

## Vedere anche

#### Concetti

[Assegnazione di un certificato di autenticazione da server a server a Microsoft Lync Server 2013](lync-server-2013-assigning-a-server-to-server-authentication-certificate-to-lync-server-2013.md)  
[Configurazione di Microsoft Lync Server 2013 in un ambiente cross-premise](lync-server-2013-configuring-lync-server-in-a-cross-premises-environment.md)

