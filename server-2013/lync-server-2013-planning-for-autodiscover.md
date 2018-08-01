---
title: Pianificazione dell'individuazione automatica
TOCTitle: Pianificazione dell'individuazione automatica
ms:assetid: 51f1ff94-1d64-4e6d-a878-b86fa07edc2d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945628(v=OCS.15)
ms:contentKeyID: 52062160
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione dell'individuazione automatica

 

_**Ultima modifica dell'argomento:** 2013-02-16_

La funzionalità di individuazione automatica è stata introdotta per Lync Server nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011. Lo scopo principale dell'implementazione iniziale dell'individuazione automatica è di offrire uno strumento per consentire a Lync Mobile di individuare il servizio Mobility (Mcx). Il servizio di individuazione automatica in Lync Server 2013 è ora un servizio utilizzato da tutti i client per individuare i servizi del server e utente. Il servizio di individuazione automatica di Microsoft Lync Server 2013 viene eseguito nei Director e nei Front End Server.

> [!TIP]  
> Per ulteriori dettagli tecnici sul servizio di individuazione automatica e sulle informazioni comunicate ai client, vedere <a href="lync-server-2013-understanding-autodiscover.md">Informazioni sull'individuazione automatica</a>.<br />Le funzionalità per dispositivi mobili sono ancora uno scenario distinto e per i servizi per dispositivi mobili sono ancora richiesti interventi di pianificazione speciali. Per ulteriori dettagli, vedere <a href="lync-server-2013-planning-for-mobility.md">Pianificazione della versione per dispositivi mobili in Lync Server 2013</a>.

Al momento dell'introduzione dell'individuazione automatica in Lync Server 2010, si sono resi necessari alcuni compromessi per poter implementare un servizio che richiedeva potenziali modifiche dei certificati nelle distribuzioni server esistenti. Il servizio di individuazione automatica può essere utilizzato sulla porta TCP 443 per HTTPS o sulla porta TCP 80 per HTTP. Se si decide di utilizzare HTTPS, i certificati nei proxy inversi, nei Director e nei Front End Server devono essere riemessi per adattarli ai record DNS richiesti `lyncdiscover.<dominio>` e `lyncdiscoverinternal.<dominio>`. Se si decide di utilizzare HTTP, la riemissione dei certificati può essere evitata utilizzando record DNS CNAME (o alias) per utilizzare i nomi esistenti nei certificati. L'utilizzo di HTTP non significa che le comunicazioni iniziali non siano crittografate.

Dato che Lync Server 2013 utilizza l'individuazione automatica per tutti i client, lo scenario principale prevede l'utilizzo esclusivo di HTTPS e la creazione dei certificati con lyncdiscover.\<dominio\> come parte della configurazione dei proxy inversi, dei Director e dei Front End Server. Se si implementa l'individuazione automatica in una distribuzione aggiornata da Lync Server 2010, è possibile scegliere di utilizzare HTTP per evitare la riemissione dei certificati. Nelle sezioni seguenti sono disponibili istruzioni per entrambi gli scenari.

> [!IMPORTANT]  
> L'elenco dei nomi alternativi soggetto nei certificati utilizzati dalla regola di pubblicazione dei servizi Web esterni deve contenere una voce <em>lyncdiscover.&lt;dominiosip&gt;</em> per ogni dominio SIP all'interno dell'organizzazione. Per informazioni dettagliate sulle voci dei nomi alternativi soggetto richiesti per Director, Front End Server e proxy inversi, vedere <a href="lync-server-2013-certificate-summary-autodiscover.md">Riepilogo certificato - Individuazione automatica</a>.

## Argomenti della sezione

  - [Riepilogo certificato - Individuazione automatica](lync-server-2013-certificate-summary-autodiscover.md)

  - [Riepilogo porte - Individuazione automatica in Lync Server 2013](lync-server-2013-port-summary-autodiscover.md)

  - [Riepilogo DNS - Individuazione automatica in Lync Server 2013](lync-server-2013-dns-summary-autodiscover.md)

  - [Distribuzione ibrida e dominio diviso - Individuazione automatica](lync-server-2013-hybrid-and-split-domain-autodiscover.md)

