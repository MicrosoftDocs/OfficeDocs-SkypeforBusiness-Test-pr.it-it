---
title: 'Lync Server 2013: Collocazione dei server supportata per i componenti perimetrali'
TOCTitle: Collocazione dei server supportata per i componenti perimetrali
ms:assetid: 435c4dd8-36af-4b71-9b88-3ffcf0fc5c65
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425934(v=OCS.15)
ms:contentKeyID: 49300350
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Collocazione dei server supportata per i componenti perimetrali in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-08_

I servizi Access Edge, Web Conferencing Edge, A/V Edge e Proxy XMPP sono collocati nei server perimetrali. I server seguenti forniscono le funzioni necessarie per l'accesso degli utenti esterni e devono essere distribuiti come server dedicati:

  - server perimetrale

  - Server Director (facoltativo)

  - Proxy inverso

> [!important]  
> Il proxy inverso non deve essere destinato esclusivamente a fornire servizi a Lync Server 2013. Ad esempio è possibile offrire servizi per pubblicare i servizi Web di Lync Server e simultaneamente fornire un sito Web pubblicato per un altro sito Web che non dispone di supporto per Lync Server. Se nella rete perimetrale è già presente un server proxy inverso per il supporto di altri servizi è possibile utilizzarlo per Lync Server 2013.
