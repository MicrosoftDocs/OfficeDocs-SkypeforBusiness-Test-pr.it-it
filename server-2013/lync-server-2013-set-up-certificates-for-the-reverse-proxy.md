---
title: 'Lync Server 2013: Configurare i certificati per il proxy inverso'
TOCTitle: Configurare i certificati per il proxy inverso
ms:assetid: c03a08ec-a67b-4f11-b0d7-6677461beaaa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412938(v=OCS.15)
ms:contentKeyID: 49301849
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare i certificati per il proxy inverso in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-08_

Ogni server proxy inverso richiede un certificato per server Web server che deve essere utilizzato dal servizio di attesa. Questo certificato deve essere emesso da un'Autorità di certificazione (CA) pubblica.

Per i dettagli relativi ai requisiti di questo e altri certificati, vedere [Requisiti dei certificati per l'accesso utente esterno in Lync Server 2013](lync-server-2013-certificate-requirements-for-external-user-access.md).

## Per impostare un certificato dei servizi Web per il proxy inverso

  - È necessario avere già configurato il proxy inverso, inclusa l'installazione del certificato dei servizi Web. Se queste operazioni non sono state eseguite prima della distribuzione dei server perimetrali, utilizzare le procedure in [Configurare server proxy inversi per Lync Server 2013](lync-server-2013-setting-up-reverse-proxy-servers.md) per creare la richiesta e installare il certificato dei servizi Web, quindi creare ogni regola di pubblicazione Web e configurarla per l'utilizzo del certificato.

