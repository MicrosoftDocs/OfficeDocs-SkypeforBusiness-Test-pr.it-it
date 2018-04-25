---
title: 'Lync Server 2013: Creare record DNS per server proxy inversi'
TOCTitle: Creare record DNS per server proxy inversi
ms:assetid: b3513339-e49b-4665-80f1-b5a1c81a0e2e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429719(v=OCS.15)
ms:contentKeyID: 49301712
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare record DNS per server proxy inversi in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-03-29_

Creare record A DNS esterni che puntino all'interfaccia esterna pubblica di Microsoft Internet Security and Acceleration (ISA) Server 2006 SP1, Forefront Threat Management Gateway 2010 oppure al modulo Application Request Routing di Internet Information Services, come descritto in [Configurare DNS per il supporto dei componenti perimetrali in Lync Server 2013](lync-server-2013-configure-dns-for-edge-support.md). Sono necessari record DNS per gli FQDN dei servizi Web esterni per ogni pool, il Server Director (o il pool di server Director) e ogni URL semplice.

Per la risoluzione dei client nel proxy inverso, è almeno necessario creare i record DNS seguenti:

  - Uno o più record host (A) che definiscano i servizi Web esterni pubblicati per i Director e i pool di Server Director (ad esempio, **webdirext.contoso.com** )

  - Uno o più record host (A) che definiscano i servizi Web esterni pubblicati per i servizi Web esterni ospitati in uno qualsiasi dei pool Front End e dei ruoli server Standard Edition (ad esempio, **webext.contoso.com** )

  - Record host (A) per gli URL semplici (ad esempio, **dialin.contoso.com** e **meet.contoso.com** )

  - Un record host (A) per il record esterno di individuazione di Lync, con puntatore all'individuazione automatica per tutte le app Web, tra cui Lync Web App, l'applicazione di pianificazione e l'applicazione per dispositivi mobili (ad esempio, **lyncdiscover.contoso.com** )

  - Record host (A) per l'URL di Server Office Web Apps (ad esempio, **officewebapp01.contoso.com** )

Per informazioni dettagliate, vedere [Riepilogo di DNS - proxy inverso in Lync Server 2013](lync-server-2013-dns-summary-reverse-proxy.md).

