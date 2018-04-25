---
title: 'Lync Server 2013: Pianificazione del bypass multimediale'
TOCTitle: Pianificazione del bypass multimediale
ms:assetid: 8ac732b6-8538-4d7b-b1a9-2035e419dac2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398703(v=OCS.15)
ms:contentKeyID: 49301246
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione del bypass multimediale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

Il termine bypass multimediale indica la rimozione del Mediation Server dal percorso multimediale in tutti i casi possibili per le chiamate con segnale che attraversa il Mediation Server.

Media Bypass consente di migliorare la qualità vocale riducendo la latenza, le conversioni inutili, la possibilità di perdita di pacchetti e il numero di potenziali punti di errore. Può inoltre essere migliorata la scalabilità, in quanto l'eliminazione dell'elaborazione multimediale per le chiamate ignorate consente di ridurre il carico di Mediation Server. La riduzione del carico favorisce la capacità di Mediation Server di controllare più gateway.

Quando un sito derivato senza Mediation Server è connesso a un sito centrale da uno o più collegamenti WAN con larghezza di banda limitata, Media Bypass consente di ridurre i requisiti di larghezza di banda consentendo il flusso diretto dei contenuti multimediali da un client in un sito derivato al relativo gateway locale, senza che sia necessario il passaggio attraverso il collegamento WAN a un server Mediation Server nel sito centrale e viceversa.

Esonerando Mediation Server dall'elaborazione multimediale, il bypass multimediale può anche consentire una riduzione del numero di Mediation Server necessari in un'infrastruttura VoIP aziendale.

Nella figura seguente sono illustrati i percorsi multimediali e di segnalazione di base in topologie con e senza Media Bypass.

**Percorsi multimediali e di segnalazione con e senza Media Bypass**

![Applicazione del controllo di ammissione di chiamata vocale con bypass multimediale sulle connessioni](images/Gg398529.4d66d529-0912-4de1-abec-266f54272eb3(OCS.15).jpg "Applicazione del controllo di ammissione di chiamata vocale con bypass multimediale sulle connessioni")

In generale, è consigliabile abilitare Media Bypass quando possibile.

## Argomenti della sezione

  - [Panoramica del bypass multimediale in Lync Server 2013](lync-server-2013-overview-of-media-bypass.md)

  - [Modalità di bypass multimediale in Lync Server 2013](lync-server-2013-media-bypass-modes.md)

  - [Bypass multimediale e controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-media-bypass-and-call-admission-control.md)

  - [Requisiti tecnici per il bypass multimediale in Lync Server 2013](lync-server-2013-technical-requirements-for-media-bypass.md)

## Sezioni correlate

[Distribuzione delle funzionalità di VoIP aziendale avanzate in Lync Server 2013](lync-server-2013-deploying-advanced-enterprise-voice-features.md)

## Vedere anche

#### Attività

[Configurare un trunk con bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-with-media-bypass.md)  

#### Concetti

[Opzioni globali di bypass multimediale in Lync Server 2013](lync-server-2013-global-media-bypass-options.md)

