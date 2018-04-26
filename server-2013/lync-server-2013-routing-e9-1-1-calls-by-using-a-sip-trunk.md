---
title: 'Lync Server 2013: Routing delle chiamate di emergenza tramite un trunk SIP'
TOCTitle: Routing delle chiamate di emergenza tramite un trunk SIP
ms:assetid: 157753c3-fe74-4e2c-81da-ee06911d4cc2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204701(v=OCS.15)
ms:contentKeyID: 49299782
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Routing delle chiamate di emergenza tramite un trunk SIP in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-29_

L'utilizzo di un trunk SIP per la connessione a un provider di servizi E9-1-1 qualificato rappresenta uno dei modi disponibili per la distribuzione del servizio E9-1-1. Per informazioni dettagliate sull'utilizzo di un gateway ELIN per la connessione a un provider di servizi E9-1-1 basati su PSTN (Public Switched Telephone Network), vedere [Routing delle chiamate di emergenza tramite un gateway ELIN in Lync Server 2013](lync-server-2013-routing-e9-1-1-calls-by-using-an-elin-gateway.md).

Il diagramma seguente illustra il routing di una chiamata di emergenza da Lync Server al punto PSAP (Public Safety Answering Point) quando si utilizza un trunk SIP e un provider di servizi E9-1-1 qualificato.

**Routing delle chiamate E9-1-1 tramite un trunk SIP**

![Routing delle chiamate di emergenza da Lync Server a PSAP](images/JJ204701.0637a9d4-2ca7-438a-8ed0-19090a4b992d(OCS.15).jpg "Routing delle chiamate di emergenza da Lync Server a PSAP")

All'inserimento di una chiamata di emergenza da un client Lync Server compatibile:

1.  A Lync Server viene inviata una richiesta SIP INVITE contenente la posizione, il numero di callback del chiamante e (facoltativo) l'URL di notifica nonché il numero di callback per le conferenze.

2.  Lync Server individua il numero di emergenza corrispondente e instrada la chiamata (in base al valore **Utilizzo PSTN** definito nei criteri di percorso applicabili) a un Mediation Server, quindi su un trunk SIP da tale server al provider di servizi E9-1-1.

3.  Il provider di servizi E9-1-1 instrada la chiamata di emergenza al punto PSAP corretto in base alla posizione fornita. Quando il client include una posizione ERL (Emergency Response Location) convalidata con la chiamata di emergenza, il provider instrada automaticamente la chiamata al punto PSAP appropriato. Se la posizione è stata inserita manualmente dall'utente, il centro ECRC (Emergency Call Response Center) verifica la precisione della posizione con il chiamante prima di instradare la chiamata di emergenza al punto PSAP.

4.  Se sono stati configurati criteri di percorso per le notifiche, a uno o più responsabili della sicurezza dell'organizzazione viene inviato un messaggio istantaneo di notifica dell'emergenza speciale di Lync. Questo messaggio viene sempre visualizzato sullo schermo dei responsabili della sicurezza come popup e contiene nome del chiamante, numero telefonico, ora e posizione. Il personale di sicurezza ha così la possibilità di rispondere rapidamente al chiamante tramite un messaggio istantaneo o una chiamata vocale.

5.  Se sono stati configurati criteri di percorso per il servizio di conferenza e il provider di servizi E9-1-1 lo supporta, un desk di sicurezza interno viene invitato a partecipare in conferenza alla chiamata con audio unidirezionale o bidirezionale.

6.  In caso di interruzione prematura della chiamata, il punto PSAP utilizza il numero di callback per contattare direttamente il chiamante.

