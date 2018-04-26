---
title: 'Lync Server 2013: Bypass multimediale e Mediation Server'
TOCTitle: Bypass multimediale e Mediation Server
ms:assetid: 8ed35f95-05cd-4b5d-8470-442d2323df71
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398719(v=OCS.15)
ms:contentKeyID: 49301293
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Bypass multimediale e Mediation Server in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

Bypass multimediale è una nuova funzionalità di Lync Server che consente a un amministratore di configurare il routing delle chiamate in modo che venga effettuato direttamente tra l'endpoint dell'utente e il gateway PSTN senza attraversare il Mediation Server. Questa funzionalità consente di migliorare la qualità delle chiamate riducendo la latenza, le operazioni superflue di conversione, il rischio di perdita di pacchetti e il numero di potenziali punti di errore. Nei casi in cui un sito remoto senza Mediation Server viene connesso a un sito centrale tramite uno o più collegamenti WAN con larghezza di banda limitata, la funzionalità Bypass multimediale riduce il requisito di larghezza di banda consentendo il flusso diretto di elementi multimediali da un client di un sito remoto al gateway locale senza dover passare attraverso il collegamento WAN a un Mediation Server nel sito centrale e tornare indietro. Questa riduzione di elaborazione a livello di Mediation Server completa la capacità del Mediation Server di controllare più gateway.

Le funzionalità di bypass multimediale e controllo di ammissione di chiamata (CAC) si escludono a vicenda. Se per una chiamata viene utilizzato il bypass multimediale, il controllo di ammissione di chiamate per tale chiamata non viene eseguito. Il presupposto è che nella chiamata non siano coinvolti link con larghezza di banda limitata.

## Vedere anche

#### Concetti

[Controllo di ammissione di chiamata e Mediation Server in Lync Server 2013](lync-server-2013-call-admission-control-and-mediation-server.md)  

#### Ulteriori risorse

[Pianificazione del bypass multimediale in Lync Server 2013](lync-server-2013-planning-for-media-bypass.md)

