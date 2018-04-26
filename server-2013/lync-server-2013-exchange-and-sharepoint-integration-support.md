---
title: "Lync Server 2013: Supporto per l'integrazione di Exchange Server e SharePoint"
TOCTitle: Supporto per l'integrazione di Exchange Server e SharePoint
ms:assetid: 72bf8aa5-55b1-4851-8a59-c96bf85d215a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205005(v=OCS.15)
ms:contentKeyID: 49300960
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supporto per l'integrazione di Exchange Server e SharePoint in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-09-29_

Lync Server 2013 e Lync 2013 sono in grado di comunicare in maniera sicura e senza problemi con altre applicazioni e prodotti server, tra cui Office 2013, Exchange 2013 e SharePoint, se integrati. L'integrazione di Lync Server 2013 e Office fornisce agli utenti l'accesso contestuale alle funzionalità di messaggistica istantanea, presenza avanzata, telefonia e conferenza di Lync. Gli utenti di Office possono accedere alle caratteristiche di Lync dal client di messaggistica e collaborazione Outlook 2013 e da altre applicazioni di Office, oppure da una pagina di Microsoft SharePoint Server 2010. Possono inoltre visualizzare una registrazione delle conversazioni di Lync nella cartella Cronologia conversazioni di Outlook. Se integrato con Exchange 2013 o Exchange Online, Lync Server 2013 supporta anche:

  - Archivio unificato per i contatti, che consente agli utenti di archiviare tutte le informazioni dei contatti in Exchange 2013 o Exchange Online, in modo da renderle disponibili a livello globale in Lync 2013, Exchange, Outlook e Outlook Web App.

  - Cronologia delle conversazioni e delle conferenze Web, archiviata nelle cartelle utente di Exchange.

  - I contenuti archiviati di Lync, ad esempio i contenuti relativi a riunioni e messaggistica istantanea, possono essere archiviati nello spazio di archiviazione di Exchange.


> [!NOTE]
> Lync Server 2013 consente l'integrazione con le versioni precedenti di Microsoft Exchange Server e SharePoint. Tuttavia, in queste versioni non sono supportate tutte le funzionalità, ad esempio l'integrazione dell'archiviazione con Microsoft Exchange.<BR>Se si migrano gli utenti a Exchange 2013, è possibile utilizzare sia l'archiviazione di Exchange che l'archiviazione provvisoria di Lync Server mentre si completa la migrazione. L'utilizzo permanente dell'archiviazione di entrambi Exchange e Lync Server non è supportata.



L'integrazione di Lync Server 2013 con Exchange 2013 e SharePoint Server richiede l'autenticazione server-to-server tra i server che eseguono Lync Server 2013, Microsoft Exchange Server e SharePoint Server. Lync Server 2013 supporta il protocollo OAuth (Open Authorization) per l'autenticazione e l'autorizzazione server-to-server. Per l'autenticazione server-to-server locale tra due server Microsoft, non è necessario utilizzare un server token di terze parti. Lync Server 2013, Exchange 2013 e SharePoint sono dotati di un server token integrato, utilizzabile a scopo di autenticazione reciproca. Ad esempio, Lync Server 2013 può emettere e firmare un token di sicurezza autonomamente, e utilizzarlo per la comunicazione con Exchange 2013. In questo caso, non è necessario utilizzare un server token di terze parti.

Lync Server 2013 supporta i due scenari di autenticazione server-to-server. Questi includono la configurazione dell'autenticazione server-to-server tra:

  - Un'installazione locale di Lync Server 2013 e un'installazione locale di Exchange 2013 e/o SharePoint Server.

  - Una coppia di componenti di Office (ad esempio, tra Microsoft Exchange 365 e Microsoft Lync Server 365, o tra Microsoft Lync Server 365 e Microsoft SharePoint 365).


> [!NOTE]
> L'autenticazione server-to-server tra un server locale e un componente locale di Office 365 non è supportata in questa versione di Lync Server 2013. Tra le altre cose, ciò significa che non è possibile configurare l'autenticazione server-to-server tra un'installazione locale di Lync Server 2013 e Microsoft Exchange 365.



Per informazioni dettagliate sulla configurazione server-to-server, vedere [Gestione dell'autenticazione da server a server (Oauth) e applicazioni partner in Lync Server 2013](lync-server-2013-managing-server-to-server-authentication-oauth-and-partner-applications.md) nella documentazione relativa alla distribuzione oppure la documentazione relativa alle operazioni.

