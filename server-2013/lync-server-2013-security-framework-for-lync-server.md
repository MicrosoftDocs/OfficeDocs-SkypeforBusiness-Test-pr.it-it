---
title: Framework di sicurezza per Lync Server 2013
TOCTitle: Framework di sicurezza per Lync Server 2013
ms:assetid: 01131e28-b38e-40d9-8524-06725b9c6608
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn481316(v=OCS.15)
ms:contentKeyID: 59682878
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Framework di sicurezza per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-08_

In questa sezione viene fornita una panoramica degli elementi fondamentali che costituiscono il framework di sicurezza per Microsoft Lync Server 2013. La comprensione del funzionamento di tali elementi è essenziale per ottimizzare il processo decisionale relativo alla protezione della distribuzione di Lync Server 2013.

Gli elementi sono i seguenti:

  - I Servizi di dominio Active Directory (AD DS) forniscono un unico repository back-end attendibile per gli account utente e le risorse di rete.

  - Controllo degli accessi in base al ruolo (RBAC) consente di delegare attività amministrative mantenendo standard di sicurezza elevati.

  - L'infrastruttura a chiave pubblica (PKI) utilizza i certificati emessi dalle autorità di certificazione attendibili (CA) per autenticare i server e assicurare l'integrità dei dati.

  - TLS (Transport Layer Security), HTTPS (HTTPS over SSL) e MTLS (Mutual TLS) consentono l'autenticazione degli endpoint e la crittografia della messaggistica istantanea. I flussi di condivisione point-to-point di applicazioni, audio e video vengono crittografati tramite SRTP (Secure Real-Time Transport Protocol).

  - Protocolli standard per l'autenticazione utente, dove possibile.

  - Windows PowerShell fornisce caratteristiche di sicurezza abilitate per impostazione predefinita, in modo che gli utenti non possano eseguire script alla leggera o inconsapevolmente.

Questi elementi di sicurezza fondamentali interagiscono per definire utenti, server, connessioni e operazioni attendibili in modo da garantire a Lync Server 2013 una base sicura.

## Argomenti della sezione

Gli argomenti in questa sezione descrivono in che modo ognuno di questi elementi fondamentali funziona per garantire la sicurezza dell'infrastruttura di Lync Server.

  - [Servizi di dominio Active Directory per Lync Server 2013](lync-server-2013-active-directory-domain-services-for-lync-server.md)

  - [Controllo degli accessi in base al ruolo (RBAC) per Lync Server 2013](lync-server-2013-role-based-access-control-rbac.md)

  - [Infrastruttura a chiave pubblica per Lync Server 2013](lync-server-2013-public-key-infrastructure.md)

  - [TLS e MTLS per Lync Server 2013](lync-server-2013-tls-and-mtls.md)

  - [Crittografia per Lync Server 2013](lync-server-2013-encryption.md)

  - [Autenticazione utenti e client per Lync Server 2013](lync-server-2013-user-and-client-authentication.md)

  - [Strumenti di gestione di Windows PowerShell e Lync Server 2013](lync-server-2013-windows-powershell-and-lync-server-management-tools.md)

