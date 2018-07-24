---
title: Configurazione del supporto per l'individuazione automatica
TOCTitle: Configurazione del supporto per l'individuazione automatica
ms:assetid: 3a266456-69a0-4539-ba99-d388b83799a8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945622(v=OCS.15)
ms:contentKeyID: 52062130
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione del supporto per l'individuazione automatica

 

_**Ultima modifica dell'argomento:** 2013-01-21_

Il **servizio di individuazione automatica** dei servizi Web di Lync Server è stato introdotto per la prima volta nell'aggiornamento cumulativo di Lync Server 2010: novembre 2011. L'aggiornamento è stato accompagnato dalla prima versione dei client Lync Mobile. Il servizio di individuazione automatica ha esposto i servizi Mobility, noti come servizi Mcx.

Il servizio di individuazione automatica è utilizzato come una posizione unica per tutti i client per richiedere informazioni sui servizi e sulle funzionalità disponibili e su come contattare i servizi (tramite un nome di dominio completo o un riferimento URL Web). Il servizio di individuazione automatica espone un numero di funzionalità e ogni client esegue richieste in base alle funzionalità che può utilizzare. Un client desktop di Lync 2013 utilizzerà ad esempio il servizio di individuazione automatica per stabilire i servizi Web esterni, ma non utilizzerà i servizi Mobility (Mcx). Per definire nel modo corretto e abilitare i client per l'utilizzo delle funzionalità disponibili, è necessario definire gli scenari che consentono a un client di trovare e utilizzare le voci dell'individuazione automatica. Per utilizzare tale servizio nella propria distribuzione è necessario che un proxy inverso pubblichi i servizi Web di Lync Server, che i record DNS siano configurati per risolvere le query DNS per il servizio di individuazione automatica di Lync Server e i servizi Web di Lync Server e che i servizi certificato siano configurati nel modo corretto per lo scenario specificato.

> [!tip]  
> Per informazioni tecniche sulle funzioni degli elementi nella richiesta/risposta dell'individuazione automatica, vedere <a href="lync-server-2013-understanding-autodiscover.md">Informazioni sull'individuazione automatica</a>.

Le informazioni e le tabelle seguenti definiscono, per scenario, le configurazioni necessarie da implementare per fornire l'utilizzo completo del servizio di individuazione automatica. Negli argomenti seguenti sono incluse informazioni specifiche per Microsoft Lync Server 2013. Per informazioni su come pianificare i servizi Mobility per Lync Server 2010, vedere <http://go.microsoft.com/fwlink/?linkid=275113>. Per distribuire i servizi Mobility per Lync Server 2010, vedere <http://go.microsoft.com/fwlink/?linkid=275114>

## Argomenti della sezione

  - [Configurazione di DNS per l'individuazione automatica](lync-server-2013-configuring-dns-for-autodiscover.md)

  - [Configurazione dei certificati per l'individuazione automatica](lync-server-2013-configuring-certificates-for-autodiscover.md)

  - [Configurazione di un proxy inverso per l'individuazione automatica](lync-server-2013-configuring-a-reverse-proxy-for-autodiscover.md)

  - [Configurazione dell'individuazione automatica per le distribuzioni ibride](lync-server-2013-configuring-autodiscover-for-hybrid-deployments.md)

