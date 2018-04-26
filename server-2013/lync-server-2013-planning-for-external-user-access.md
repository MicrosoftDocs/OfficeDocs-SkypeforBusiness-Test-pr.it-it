---
title: "Lync Server 2013: Pianificazione dell'accesso degli utenti esterni"
TOCTitle: Pianificazione dell'accesso degli utenti esterni
ms:assetid: ea098933-eff5-461e-aba3-e7f128784dc2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399048(v=OCS.15)
ms:contentKeyID: 49302334
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione dell'accesso degli utenti esterni in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-01-19_

Nella maggior parte delle organizzazioni le comunicazioni coinvolgono servizi e utenti non compresi nella rete interna. Tali servizi e utenti includono dipendenti temporaneamente o permanentemente fuori sede, dipendenti di organizzazioni clienti e partner, persone che utilizzano i servizi di messaggistica istantanea pubblica e potenziali clienti, partner e utenti anonimi che vengono invitati a riunioni e presentazioni. In questa documentazione queste persone vengono indicate come *utenti esterni* .

Con Microsoft Lync Server 2013, gli utenti dell'organizzazione possono utilizzare la messaggistica istantanea e la presenza per comunicare con utenti esterni, oltre che per partecipare a conferenze audio/video (A/V) e conferenze Web con i dipendenti fuori sede e altri tipi di utenti esterni. È inoltre possibile supportare l'accesso esterno da dispositivi mobili e tramite VoIP aziendale. Gli utenti esterni che non sono membri dell'organizzazione possono partecipare a riunioni di Lync Server 2013 come partecipanti anonimi.

Per supportare le comunicazioni attraverso il firewall dell'organizzazione, distribuire il server perimetrale Lync Server 2013 nella rete perimetrale. Il server perimetrale controlla il modo in cui gli utenti possono connettersi alla distribuzione interna di Lync Server 2013 dall'esterno del firewall. Controlla inoltre le comunicazioni con utenti esterni che hanno origine nel firewall.

A seconda di specifici requisiti, è possibile distribuire uno o più server perimetrali in una o più posizioni. In questa sezione vengono descritti gli scenari per l'accesso di utenti esterni a Lync Server 2013 e viene illustrato come pianificare la topologia perimetrale e dei proxy inversi.


> [!NOTE]
> Anche se è necessario un server perimetrale per supportare VoIP aziendale e l'accesso di utenti esterni, questa sezione è incentrata sul supporto per messaggistica istantanea, presenza, conferenze A/V, federazione, conferenze Web e Lync Mobile. Per informazioni dettagliate sul supporto per VoIP aziendale, vedere <A href="lync-server-2013-planning-for-enterprise-voice.md">Pianificazione di VoIP aziendale in Lync Server 2013</A> nella documentazione relativa alla pianificazione.



## Argomenti della sezione

  - [Modifiche introdotte in Lync Server 2013 che incidono sulla pianificazione dei server perimetrali](lync-server-2013-changes-in-lync-server-that-affect-edge-server-planning.md)

  - [Requisiti di sistema per i componenti per l'accesso degli utenti esterni per Lync Server 2013](lync-server-2013-system-requirements-for-external-user-access-components.md)

  - [Panoramica dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-overview-of-external-user-access.md)

  - [Informazioni sull'individuazione automatica](lync-server-2013-understanding-autodiscover.md)

  - [Scelta di una topologia in Lync Server 2013](lync-server-2013-choosing-a-topology.md)

  - [Raccolta dati in Lync Server 2013](lync-server-2013-data-collection.md)

  - [Determinare i requisiti di DNS per Lync Server 2013](lync-server-2013-determine-dns-requirements.md)

  - [Determinare i requisiti di porte e firewall A/V esterni per Lync Server 2013](lync-server-2013-determine-external-a-v-firewall-and-port-requirements.md)

  - [Pianificare i certificati dei server perimetrali in Lync Server 2013](lync-server-2013-plan-for-edge-server-certificates.md)

  - [Scenari per l'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-scenarios-for-external-user-access.md)

