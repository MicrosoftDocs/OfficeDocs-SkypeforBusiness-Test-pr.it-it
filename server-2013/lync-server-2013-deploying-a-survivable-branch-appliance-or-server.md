---
title: 'Lync Server 2013: Distribuzione di Survivable Branch Appliance o Survivable Branch Server'
TOCTitle: Distribuzione di Survivable Branch Appliance o Survivable Branch Server
ms:assetid: cb780c14-dc5f-41ba-8092-f20ae905bd16
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398849(v=OCS.15)
ms:contentKeyID: 49301975
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuzione di Survivable Branch Appliance o Survivable Branch Server con Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-12-10_

Per VoIP aziendale resiliente si intende la resilienza dei siti di succursale, ovvero la capacità di fornire un servizio VoIP aziendale continuo agli utenti dei siti di succursale qualora il collegamento al sito centrale non sia più disponibile.

Per i siti di succursale di piccole e medie dimensioni, ovvero con un numero di utenti compreso tra 25 e 1.000, è consigliabile distribuire un Survivable Branch Appliance, che terminerà le chiamate PSTN (Public Switched Telephone Network) utilizzando il proprio gateway PSTN incorporato o un trunk SIP per un provider di servizi telefonici. Un Survivable Branch Appliance è un dispositivo di terze parti che include un blade server che esegue il sistema operativo Windows Server 2008 R2, la funzione di registrazione di Lync Server 2013, il software Mediation Server e un gateway PSTN, tutti in un singolo chassis di appliance.

Per i siti di succursale con un numero di utenti compreso tra 1.000 e 5.000 e senza WAN resiliente, è consigliabile un Survivable Branch Server connesso a un gateway PSTN o un trunk SIP per un provider di servizi telefonici. Un Survivable Branch Server è un computer basato su Windows Server in cui sono installati la funzione di registrazione e il software Mediation Server.


> [!NOTE]
> Per i siti di succursale con più di 5.000 utenti e amministratori di Lync Server dedicati, è consigliabile una distribuzione completa di Lync Server 2013, separata da quella del sito centrale.<BR>Per istruzioni su come scegliere la soluzione di resilienza ottimale per i siti di succursale dell'organizzazione, incluse informazioni sui prerequisiti e considerazioni relative alla pianificazione, vedere <A href="lync-server-2013-branch-site-resiliency-requirements.md">Requisiti di resilienza dei siti di succursale per Lync Server 2013</A> nella documentazione relativa alla pianificazione.



## Argomenti della sezione

  - [Distribuzione di Survivable Branch Appliance o Survivable Branch Server con Lync Server 2013 - Attività presso il sito centrale](lync-server-2013-deploying-a-survivable-branch-appliance-or-server-central-site-tasks.md)

  - [Distribuire un Survivable Branch Appliance o un Survivable Branch Server con Lync Server 2013 - Attività presso il sito di succursale](lync-server-2013-deploy-a-survivable-branch-appliance-or-server-branch-site-task.md)

  - [Configurazione degli utenti per la resilienza dei siti di succursale in Lync Server 2013](lync-server-2013-configuring-users-for-branch-site-resiliency.md)

  - [Ospitare utenti in Survivable Branch Appliance o Survivable Branch Server in Lync Server 2013](lync-server-2013-home-users-on-a-survivable-branch-appliance-or-server.md)

  - [Appendici: Survivable Branch Appliance e Survivable Branch Server in Lync Server 2013](lync-server-2013-appendices-survivable-branch-appliances-and-servers.md)

## Vedere anche

#### Ulteriori risorse

[Distribuzione di Lync Server 2013](lync-server-2013-deploying-lync-server.md)

