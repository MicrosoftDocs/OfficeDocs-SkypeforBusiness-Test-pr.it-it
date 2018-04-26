---
title: 'Lync Server 2013: Concessione di autorizzazioni'
TOCTitle: Concessione di autorizzazioni
ms:assetid: d1c9ea66-bd07-480e-99a0-011108f97e42
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398901(v=OCS.15)
ms:contentKeyID: 49302060
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Concessione di autorizzazioni in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-15_

Per la configurazione, è possibile concedere autorizzazioni al gruppo universale RTCUniversalServerAdmins per un'unità organizzativa di Active Directory specifica, consentendo ai membri del gruppo RTCUniversalServerAdmins in tale unità organizzativa di installare Lync Server 2013 nel dominio specificato. Le autorizzazioni che è possibile concedere per un'unità organizzativa sono le seguenti:

  - Read

  - Write

  - ReadSPN

  - WriteSPN

Per l'amministrazione, è possibile aggiungere autorizzazioni alle unità organizzative specificate in modo che i membri dei gruppi universali RTC creati durante la preparazione della foresta possano accedere alle unità organizzative anche se non sono membri del gruppo Domain Admins. Le autorizzazioni aggiunte all'unità organizzativa specificata sono identiche a quelle aggiunte dal cmdlet **Enable-CsAdDomain** ai contenitori di unità organizzative di computer e utenti.

## Contenuto della sezione

  - [Concessione di autorizzazioni di installazione in Lync Server 2013](lync-server-2013-granting-setup-permissions.md)

  - [Concessioni di autorizzazioni per unità organizzative in Lync Server 2013](lync-server-2013-granting-organizational-unit-permissions.md)

