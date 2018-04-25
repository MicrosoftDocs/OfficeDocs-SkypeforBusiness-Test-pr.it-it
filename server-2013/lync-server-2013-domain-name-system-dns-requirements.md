---
title: Requisiti di DNS (Domain Name System)
TOCTitle: Requisiti di DNS (Domain Name System)
ms:assetid: 586cf18e-0080-4eb1-aee5-56843277fdfc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398386(v=OCS.15)
ms:contentKeyID: 49300609
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti di DNS (Domain Name System)

 

_**Ultima modifica dell'argomento:** 2012-06-18_

Per distribuire il Lync Server è necessario creare record DNS (Domain Name System) che consentano l'individuazione di client e server e facoltativamente il supporto dell'accesso client automatico, se l'organizzazione desidera supportarlo.

Lync Server utilizza DNS nei modi seguenti:

  - Per individuare i pool o i server interni per le comunicazioni server-server.

  - Per consentire ai client di individuare il pool Front End o server Standard Edition utilizzato per le varie transazioni SIP.

  - Per consentire ai dispositivi per comunicazioni unificate non connessi di individuare il pool Front End o il server Standard Edition che esegue il servizio Web Aggiornamento dispositivi, ottenere gli aggiornamenti e inviare i registri.

  - Per consentire ai server e ai client esterni di connettersi agli server perimetrali o al proxy inverso HTTP per i servizi di messaggistica istantanea o conferenza.

  - Per consentire ai dispositivi per comunicazioni unificate esterni di connettersi al servizio Web Aggiornamento dispositivi tramite gli server perimetrali o il proxy inverso HTTP e ottenere gli aggiornamenti.

  - Per consentire ai client mobili di individuare automaticamente le risorse dei servizi Web senza richiedere agli utenti di immettere manualmente gli URL nelle impostazioni dei dispositivi.

## Argomenti della sezione

  - [Determinare i requisiti di DNS per Lync Server 2013](lync-server-2013-determine-dns-requirements.md)

  - [Requisiti di DNS per pool Front End](lync-server-2013-dns-requirements-for-front-end-pools.md)

  - [Requisiti DNS per server Standard Edition](lync-server-2013-dns-requirements-for-standard-edition-servers.md)

  - [Requisiti DNS per gli URL semplici in Lync Server 2013](lync-server-2013-dns-requirements-for-simple-urls.md)

  - [Requisiti DNS per l'accesso automatico dei client in Lync Server 2013](lync-server-2013-dns-requirements-for-automatic-client-sign-in.md)

  - [Requisiti di DNS per dispositivi mobili](lync-server-2013-dns-requirements-for-mobility.md)

  - [Bilanciamento del carico DNS in Lync Server 2013](lync-server-2013-dns-load-balancing.md)

