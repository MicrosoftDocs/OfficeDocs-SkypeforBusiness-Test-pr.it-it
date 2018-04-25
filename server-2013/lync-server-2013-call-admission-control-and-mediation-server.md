---
title: 'Lync Server 2013: Controllo di ammissione di chiamata e Mediation Server'
TOCTitle: Controllo di ammissione di chiamata e Mediation Server
ms:assetid: 76faccdc-67d0-4c8b-8e47-1e23c93b02c6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398585(v=OCS.15)
ms:contentKeyID: 49301026
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Controllo di ammissione di chiamata e Mediation Server in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

Il servizio Controllo di ammissione di chiamata (CAC), introdotto in Lync Server 2010, gestisce lo stabilimento della sessione in tempo reale basandosi sulla larghezza di banda disponibile, per evitare agli utenti di sperimentare chiamate di scarsa qualità quando le reti sono congestionate. Per supportare questa funzionalità, Mediation Server, che fornisce la traduzione dei segnali e del contenuto multimediale tra l'infrastruttura VoIP di VoIP aziendale e un gateway o un provider di trunking SIP, è responsabile della gestione della larghezza di banda per le proprie interazioni sul lato di Lync Server e sul lato del gateway. Nel controllo di ammissione di chiamata, l'entità di terminazione di una chiamata deve gestire la prenotazione della larghezza di banda. I peer gateway (gateway PSTN, IP-PBX, SBC) con cui interagisce Mediation Server sul lato del gateway non supportano il controllo di ammissione di chiamata di Lync Server 2013. Di conseguenza, Mediation Server deve gestire le interazioni relative alla larghezza di banda per conto del proprio peer gateway. Laddove possibile, Mediation Server riserverà la larghezza di banda in anticipo. In caso contrario, ad esempio se la località dell'endpoint multimediale finale sul lato del gateway non è nota per una chiamata in uscita al peer gateway, la larghezza di banda viene riservata al momento dell'esecuzione della chiamata. Questo comportamento può causare una richiesta eccessiva di larghezza di banda, ma è l'unico modo per impedire squilli falsi..

Il bypass multimediale e la prenotazione della larghezza di banda si escludono a vicenda. Se per una chiamata viene utilizzato il bypass multimediale, non è possibile effettuare il controllo di ammissione di chiamata per la chiamata. Il concetto alla base di questo comportamento è che non vi sono collegamenti con larghezza di banda limitata interessati dalla chiamata. Se per una chiamata specifica che interessa Mediation Server viene utilizzato il controllo di ammissione di chiamata, la chiamata non può utilizzare il bypass multimediale.

Per informazioni dettagliate sul bypass multimediale o il controllo di ammissione di chiamata, vedere [Pianificazione del bypass multimediale in Lync Server 2013](lync-server-2013-planning-for-media-bypass.md) o [Pianificazione del servizio Controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-planning-for-call-admission-control.md) nella documentazione relativa alla pianificazione.

