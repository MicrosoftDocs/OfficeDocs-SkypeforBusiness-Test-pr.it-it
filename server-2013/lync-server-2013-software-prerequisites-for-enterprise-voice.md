---
title: 'Lync Server 2013: Prerequisiti software per VoIP aziendale'
TOCTitle: Prerequisiti software per VoIP aziendale
ms:assetid: 41172119-9631-46c7-9d9f-386d951c650b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425916(v=OCS.15)
ms:contentKeyID: 49300324
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Prerequisiti software per VoIP aziendale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-03_

Verificare che l'infrastruttura in cui si intende distribuire VoIP aziendale soddisfi i prerequisiti software seguenti:

  - Lync Server 2013 Standard Edition o Enterprise Edition è installato e funzionante nella rete.

  - Distribuzione e utilizzo di tutti i server perimetrali nella rete perimetrale, inclusi i server perimetrali che eseguono il servizio Access Edge, il servizio A/V Edge, il servizio Web Conferencing Edge e un proxy inverso.

  - Microsoft Exchange Server 2007 Service Pack 3 (SP3), Microsoft Exchange Server 2010 o Microsoft Exchange Server 2013 per l'integrazione di messaggistica unificata di Exchange con Lync Server e per fornire notifiche e informazioni del log chiamate avanzate agli endpoint Lync.

  - Uno o più utenti sono stati creati e abilitati per Lync Server.

  - Distribuzione di client e dispositivi Lync.

  - Installazione di Generatore di topologie in un server della rete.

## Passaggi successivi: verificare i prerequisiti della sicurezza e della configurazione

Dopo aver verificato i prerequisiti software per VoIP aziendale, è possibile utilizzare la documentazione per continuare la preparazione per la distribuzione di VoIP aziendale:

1.  Verificare la sicurezza, la configurazione utente e i prerequisiti hardware, come descritto in [Prerequisiti di configurazione e sicurezza per VoIP aziendale in Lync Server 2013](lync-server-2013-security-and-configuration-prerequisites-for-enterprise-voice.md).

2.  Installare il Mediation Server, come descritto in [Installare i file per Mediation Server in Lync Server 2013](lync-server-2013-install-the-files-for-mediation-server.md), ma *solo* se si desidera distribuire un Mediation Server autonomo o un pool, poiché i Mediation Server vengono installati nell'ambito del processo di distribuzione del pool Front End o del server Standard Edition quando sono collocati.

3.  Configurare le connessioni trunk per fornire la connettività PSTN per gli utenti, come descritto in [Configurazione di trunk in Lync Server 2013](lync-server-2013-configuring-trunks.md).

