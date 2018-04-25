---
title: 'Lync Server 2013: Abilitazione di Office Web Apps Server e Lync Server 2013'
TOCTitle: Abilitazione di Office Web Apps Server e Lync Server 2013
ms:assetid: 3370ab55-9949-4f32-b88b-5cffed6aaad8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204792(v=OCS.15)
ms:contentKeyID: 49300118
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione dell'integrazione con Office Web Apps Server e Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-02-05_

Lync Server 2013 usa Server Office Web Apps per gestire le presentazioni di PowerPoint. Per informazioni sui vantaggi di questo approccio, vedere [Panoramica di Web Conferencing in Lync Server 2013](lync-server-2013-web-conferencing-overview.md).

Per poter usufruire di queste nuove funzionalità, gli amministratori devono installare Server Office Web Apps e configurare Lync Server 2013 per comunicare con Server Office Web Apps. In questa documentazione sono contenute informazioni su come configurare Lync Server 2013 per l'uso con Server Office Web Apps. Non sono invece disponibili informazioni su come installare Server Office Web Apps. Tali informazioni sono reperibili nel sito Web relativo alla distribuzione delle Microsoft Office Web Apps all'indirizzo [http://go.microsoft.com/fwlink/?linkid=257525\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=257525%26clcid=0x410). La guida include informazioni complete sui prerequisiti per Server Office Web Apps. Tenere presente che Server Office Web Apps deve essere installato in un computer autonomo che non esegue Lync Server, Microsoft SQL Server o qualsiasi altra applicazione server. Nel computer deve essere installata una versione di Microsoft Office. I computer usati per l'esecuzione di Server Office Web Apps devono inoltre disporre di un set specifico di componenti software installati, incluso .NET Framework 4.5 e Windows PowerShell 3.0. Questi requisiti, insieme alle informazioni sulla configurazione dei certificati e di Internet Information Services (IIS), sono descritti in modo dettagliato nel sito Web relativo alla distribuzione di Microsoft Office Web Apps all'indirizzo [http://go.microsoft.com/fwlink/?linkid=257525\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=257525%26clcid=0x410).

Questo documento illustra i seguenti argomenti:

  - [Configurazione di Lync Server 2013 per l'utilizzo con Office Web Apps Server](lync-server-2013-configuring-lync-server-2013-to-work-with-office-web-apps-server.md)

  - [Pubblicazione di Office Web Apps Server in Lync Server 2013 tramite un server proxy inverso](lync-server-2013-publishing-office-web-apps-server-using-a-reverse-proxy-server.md)

  - [Convalida della configurazione di Office Web Apps Server in Lync Server 2013](lync-server-2013-validating-the-configuration-of-office-web-apps-server.md)

  - [Configurazione dei client di Lync Server 2013 per l'utilizzo con Office Web Apps Server](lync-server-2013-configuring-clients-for-use-with-office-web-apps-server.md)

