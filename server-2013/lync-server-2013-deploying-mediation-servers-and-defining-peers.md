---
title: 'Lync Server 2013: Distribuzione di Mediation Server e definizione di peer'
TOCTitle: Distribuzione di Mediation Server e definizione di peer
ms:assetid: a684f1da-6671-4011-adf6-2db49e2528e2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412780(v=OCS.15)
ms:contentKeyID: 49301560
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuzione di Mediation Server e definizione di peer in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

Il carico di lavoro di VoIP aziendale, le conferenze telefoniche con accesso esterno e le applicazioni di VoIP aziendale avanzate ( applicazione Response Group, applicazione Parcheggio di chiamata, controllo di ammissione di chiamata e così via), sono disponibili nei pool Front End. Con Lync Server 2013, la funzionalità del Mediation Server è incorporata nel Front End Server. Non è più necessario un Mediation Server autonomo separato. I pool Front End possono comunicare direttamente con i gateway supportati (un gateway PSTN o un sistema I-PBX), eliminando la necessità di un Mediation Server che funga da intermediario.

L'unica eccezione è rappresentata dalla configurazione di un trunk SIP per la connessione a un Session Border Controller per un provider di servizi di telefonia Internet (ITSP). Per connettere l'infrastruttura di VoIP aziendale al provider di trunk SIP, deve essere distribuito un Mediation Server separato.

La connessione tra Lync Server (il componente Mediation Server in un pool Front End o un Mediation Server autonomo) e un gateway è definita come un'associazione logica nota come *trunk* . Negli argomenti di questa sezione viene illustrato come definire un trunk e come distribuire un Mediation Server autonomo se si effettua la connessione a un trunk SIP.

## Argomenti della sezione

  - [Definire un Mediation Server in Generatore di topologie in Lync Server 2013](lync-server-2013-define-a-mediation-server-in-topology-builder.md)

  - [Definire un gateway in Generatore di topologie in Lync Server 2013](lync-server-2013-define-a-gateway-in-topology-builder.md)

  - [Installare i file per Mediation Server in Lync Server 2013](lync-server-2013-install-the-files-for-mediation-server.md)

  - [Definire ulteriori trunk in Generatore di topologie in Lync Server 2013](lync-server-2013-define-additional-trunks-in-topology-builder.md)

## Sezioni correlate

[Configurazione di conferenze telefoniche con accesso esterno in Lync Server 2013](lync-server-2013-configuring-dial-in-conferencing.md)

