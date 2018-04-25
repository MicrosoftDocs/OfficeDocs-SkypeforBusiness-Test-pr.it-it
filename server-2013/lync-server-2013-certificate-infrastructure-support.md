---
title: "Lync Server 2013: Supporto per l'infrastruttura di certificazione"
TOCTitle: Supporto per l'infrastruttura di certificazione
ms:assetid: 47aa5c95-eb60-4d4b-81d5-7fdaef1a1145
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425950(v=OCS.15)
ms:contentKeyID: 49300417
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supporto per l'infrastruttura di certificazione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-07_

Lync Server 2013 richiede un'infrastruttura a chiave pubblica (PKI) per supportare le connessioni TLS (Transport Layer Security) e MTLS (mutual TLS). Per impostazione predefinita, Lync Server 2013 è configurato per utilizzare TLS per le connessioni client-server. MTLS viene utilizzato per le connessioni tra server.

I certificati MTLS devono essere emessi da Autorità di certificazione (CA) attendibili per Lync Server 2013. Lync Server supporta i certificati emessi dalle Autorità di certificazione seguenti:

  - Certificati emessi da un'autorità di certificazione interna:
    
      - CA del sistema operativo Windows Server 2003
    
      - CA del sistema operativo Windows Server 2008
    
      - CA del sistema operativo Windows Server 2008 R2
    
      - CA del sistema operativo Windows Server 2012
    
      - CA del sistema operativo Windows Server 2012 R2

  - Certificati emessi da un'autorità di certificazione pubblica

La comunicazione con altre applicazioni e server, ad esempio Exchange 2013, richiede un certificato supportato dalle altre applicazioni e prodotti. Per la versione 2013, Lync Server 2013 e altri prodotti server Microsoft, compresi Exchange 2013 e SharePoint Server, supportano il protocollo Open Authorization (OAuth) per l'autenticazione e l'autorizzazione server-server. Per informazioni dettagliate, vedere [Gestione dell'autenticazione da server a server (Oauth) e applicazioni partner in Lync Server 2013](lync-server-2013-managing-server-to-server-authentication-oauth-and-partner-applications.md) nella documentazione relativa alla distribuzione o nella documentazione relativa alle operazioni.

Per le connessioni da client che eseguono il sistema operativo Windows 7, il sistema operativo Windows Server 2008 R2 e il Microsoft Office Communicator 2007 Phone Edition, Lync Server 2013 include il supporto per (ma non richiede) i certificati firmati con la funzione hash crittografico SHA-256. Per supportare l'accesso esterno con SHA-256, il certificato esterno viene emesso da un'Autorità di certificazione pubblica che utilizza SHA-256.

Per informazioni dettagliate sui requisiti dei certificati, vedere [Requisiti dell'infrastruttura dei certificati per Lync Server 2013](lync-server-2013-certificate-infrastructure-requirements.md) nella documentazione relativa alla pianificazione. Per informazioni dettagliate sull'uso dei caratteri jolly con i certificati, vedere [Supporto dei certificati con caratteri jolly in Lync Server 2013](lync-server-2013-wildcard-certificate-support.md) nella documentazione relativa alla supportabilità.

