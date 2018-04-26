---
title: 'Lync Server 2013: Componenti VoIP della rete perimetrale'
TOCTitle: Componenti VoIP della rete perimetrale
ms:assetid: 74230008-695d-436a-90b9-9cd060c70f7b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398559(v=OCS.15)
ms:contentKeyID: 49300981
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Componenti VoIP della rete perimetrale per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

I chiamanti esterni che utilizzano client per le comunicazioni unificate per singole chiamate o conferenze telefoniche utilizzano server perimetrale per le comunicazioni vocali con i collaboratori.

In un server perimetrale, il servizio Access Edge fornisce i segnali SIP per le chiamate dagli utenti del Lync esterni al firewall dell'organizzazione. Il servizio A/V Edge consente l'attraversamento del contenuto multimediale in NAT e nei firewall. Un chiamante che utilizza un client per le comunicazioni unificate dall'esterno del firewall aziendale utilizza il servizio A/V Edge per singole chiamate e conferenze telefoniche.

Il servizio di autenticazione A/V si trova nella stessa posizione del servizio A/V Edge e offre servizi di autenticazione per questo servizio. Gli utenti esterni che tentano di connettersi al servizio A/V Edge devono disporre di un token di autenticazione fornito dal servizio di autenticazione A/V prima di poter effettuare le proprie chiamate.

