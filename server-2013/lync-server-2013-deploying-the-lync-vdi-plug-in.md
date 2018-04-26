---
title: 'Lync Server 2013: Distribuzione del plug-in VDI di Lync'
TOCTitle: Distribuzione del plug-in VDI di Lync
ms:assetid: 11d3bd5d-6dd3-471c-b842-b072fa197714
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204683(v=OCS.15)
ms:contentKeyID: 49299725
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuzione del plug-in VDI di Lync in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-03_

Il client Lync 2013 supporta l'audio e il video in un ambiente Virtual Desktop Infrastructure (VDI). Un utente può connettere un dispositivo audio o video, ad esempio un auricolare o una videocamera, al computer locale, ad esempio un thin client o computer riconfigurato, ma non può connettersi alla macchina virtuale, accedere al client Lync 2013 in esecuzione sulla macchina virtuale e partecipare a comunicazioni audio e video in tempo reale, anche se il client è in esecuzione in locale.

Il plug-in VDI di Lync è un'applicazione autonoma che viene installata nel computer locale e consente l'utilizzo di dispositivi audio e video locali con il client Lync 2013 in esecuzione sulla macchina virtuale. Il plug-in non richiede che Lync sia installato nel computer locale. Dopo l'accesso al client Lync 2013 in esecuzione sulla macchina virtuale, Lync richiede all'utente di immettere nuovamente le proprie credenziali per stabilire una connessione al plug-in VDI di Lync in esecuzione sul computer locale. Una volta effettuata questa connessione, l'utente può effettuare e ricevere chiamate audio e video.

## Contenuto della sezione

  - [Prerequisiti del plug-in VDI di Lync in Lync Server 2013](lync-server-2013-lync-vdi-plug-in-prerequisites.md)

  - [Preparazione dell'ambiente di Lync Server 2013 per VDI](lync-server-2013-preparing-your-environment-for-vdi.md)

  - [Accesso e utilizzo di Lync 2013 nella macchina virtuale](lync-server-2013-signing-in-and-using-lync-2013-on-the-virtual-machine.md)

  - [Risoluzione dei problemi del plug-in VDI di Lync e Lync Server 2013](lync-server-2013-troubleshooting-the-lync-vdi-plug-in.md)

  - [Tecnologie di virtualizzazione supportate e limitazioni note in Lync Server 2013](lync-server-2013-supported-virtualization-technologies-and-known-limitations.md)

