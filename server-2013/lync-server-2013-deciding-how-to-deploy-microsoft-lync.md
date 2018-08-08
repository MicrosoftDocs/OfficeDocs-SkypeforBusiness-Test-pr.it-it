---
title: "Lync Server 2013: Determina la modalità di distribuzione di Microsoft Lync"
TOCTitle: Determinazione della modalità di distribuzione di Microsoft Lync
ms:assetid: 6ca677d3-745d-4935-8f05-19274a8bccf2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204979(v=OCS.15)
ms:contentKeyID: 49300897
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Determinazione della modalità di distribuzione di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-03_

Quando si esegue la pianificazione per Lync, la prima decisione importante riguarda le modalità di distribuzione di Microsoft Lync: come Lync Server 2013 locale o Skype for Business online con Microsoft Office 365 nel cloud.

  - **Lync Server 2013 locale** : questa scelta garantisce l'intero insieme di funzionalità di Lync e offre la massima flessibilità nella configurazione, personalizzazione ed esecuzione della distribuzione. Tutti i server sono installati localmente e mantenuti presso l'organizzazione. La distribuzione locale garantisce l'intero insieme di funzionalità di Lync Server.

  - **Skype for Business online nel cloud :** Skype for Business online è concepito per quelle organizzazioni che desiderano ottenere i vantaggi di costo e agilità derivanti da messaggistica istantanea, presenza e riunioni su cloud, senza sacrificare le funzionalità di classe business di Lync Server. Con Skype for Business online, Microsoft distribuisce e mantiene l'infrastruttura server necessaria, e gestisce manutenzione, patch e upgrade su base continua. Alcune caratteristiche disponibili nella distribuzione locale non sono disponibili in Skype for Business online.

Il tipo di distribuzione più adatto per un'azienda dipende dal tipo di workload che si ha bisogno di distribuire, nonché dalla posizione geografica e dallo stato dell'attività dell'organizzazione.

## Lync Server

Una distribuzione locale di Lync Server rappresenta la soluzione ideale nei seguenti casi:

  - **Funzionalità VoIP aziendale complete**   Se si ha intenzione di distribuire una soluzione VoIP aziendale completa a sostituzione di una soluzione PBX o un altro tipo di soluzione che si serve di funzionalità di chiamata avanzate, è necessaria una distribuzione locale di Lync Server. La distribuzione locale supporta un tipo di connettività diretta con i sistemi e trunk PBX, e funzionalità telefoniche avanzate come gruppi di risposta e parcheggio di chiamata. Lync Online attualmente non supporta queste funzionalità.

  - **Controlli della qualità multimediale**   Se si desidera ottenere l'insieme completo di funzionalità per il controllo della qualità multimediale, tra cui le funzioni di Controllo di ammissione di chiamata (CAC) e Quality of Service (QoS), si ha bisogno di una distribuzione locale .

  - **Chat permanente**   Se si ha bisogno di distribuire la chat permanente all'interno della propria organizzazione, è necessario optare per una distribuzione locale.

  - **Applicazioni server di terze parti**   Solo le distribuzioni locali sono in grado di funzionare con applicazioni sicure di terze parti che utilizzano Microsoft Unified Communications Managed API (UCMA).

  - **Compagnie multinazionali e multiregionali che necessitano di supporto**   Se si dispone di data center in più Paesi o regioni e si ha bisogno di server da distribuire e gestire su base regionale, una distribuzione locale rappresenta la soluzione migliore, poiché garantisce questo tipo di funzionalità per la gestione regionale.

  - **Controllo completo di criteri, rapporti e upgrade**   Con la distribuzione locale di Lync Server si ottiene l'accesso all'insieme completo di criteri per server e client, rapporti di monitoraggio e altri rapporti, nonché impostazione dei tempi degli upgrade. Lync Online garantisce un sottoinsieme di impostazioni e rapporti per i criteri, nonché una funzionale, seppur limitata, finestra per l'accettazione degli upgrade.

## Lync Online

Se nessuno dei precedenti rappresenta un fattore di importanza critica per la propria organizzazione, è possibile scegliere Lync Online, che offre una distribuzione e una gestibilità semplificate. Lync Online offre un insieme solido di caratteristiche per la messaggistica istantanea, la presenza e le conferenze, e consente la trasmissione video e audio tramite protocollo IP tra gli utenti dell'organizzazione.

