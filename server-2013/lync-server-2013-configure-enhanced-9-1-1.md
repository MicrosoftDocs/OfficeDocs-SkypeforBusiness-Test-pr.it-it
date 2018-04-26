---
title: 'Lync Server 2013: Configurare i servizi di emergenza avanzati'
TOCTitle: Configurare i servizi di emergenza avanzati
ms:assetid: 5967de00-c8b9-4923-86da-6ad3369a4cad
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398390(v=OCS.15)
ms:contentKeyID: 49300667
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare i servizi di emergenza avanzati in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-24_

Enhanced 9-1-1 (E9-1-1) è una funzionalità di notifica per chiamate di emergenza che associa il numero di telefono del chiamante a una via o a un numero civico. Con tali informazioni, l'operatore del servizio di salute pubblica e sicurezza nazionale (PSAP) è in grado di erogare immediatamente servizi di emergenza nei confronti del chiamante in difficoltà.

Per supportare E9-1-1, il Lync Server 2013 deve essere in grado di associare correttamente una posizione a un client e di assicurarsi che tali informazioni vengano usate per instradare la chiamata di emergenza al centro di raccolta delle chiamate di emergenza (PSAP, Public Safety Answering Point) più vicino.

Per informazioni dettagliate sulla pianificazione della distribuzione del servizio E9-1-1, vedere [Pianificazione per i servizi di emergenza (E9-1-1) in Lync Server 2013](lync-server-2013-planning-for-emergency-services-e9-1-1.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync Server 2013 supporta E9-1-1 solo all'interno degli Stati Uniti. Per distribuire il servizio E9-1-1, è necessario configurare una connessione SIP a un provider del servizio E9-1-1 qualificato o distribuire un gateway ELIN (Emergency Location Identification Number) a un provider del servizio E9-1-1 basato su PSTN (Public Switched Telephone). Per informazioni dettagliate, vedere <a href="lync-server-2013-enhanced-9-1-1-e9-1-1-and-mediation-server.md">Servizi di emergenza avanzati e Mediation Server in Lync Server 2013</a>. Per informazioni dettagliate sulla configurazione di connessioni trunk, vedere <a href="lync-server-2013-configure-a-trunk-with-media-bypass.md">Configurare un trunk con bypass multimediale in Lync Server 2013</a>.</td>
</tr>
</tbody>
</table>


## Argomenti della sezione

  - [Configurare una route vocale E9-1-1 in Lync Server 2013](lync-server-2013-configure-an-e9-1-1-voice-route.md)

  - [Creare criteri percorso in Lync Server 2013](lync-server-2013-create-location-policies.md)

  - [Configurare le informazioni del sito per E9-1-1 in Lync Server 2013](lync-server-2013-configure-site-information-for-e9-1-1.md)

  - [Configurare il database delle posizioni in Lync Server 2013](lync-server-2013-configure-the-location-database.md)

  - [Configurare le caratteristiche avanzate del servizio chiamate di emergenza (E9-1-1) in Lync Server 2013](lync-server-2013-configure-advanced-e9-1-1-features.md)

