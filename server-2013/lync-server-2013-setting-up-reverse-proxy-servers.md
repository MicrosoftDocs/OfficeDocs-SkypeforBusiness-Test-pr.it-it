---
title: 'Lync Server 2013: Configurare server proxy inversi'
TOCTitle: Configurare server proxy inversi
ms:assetid: 00bc138a-243f-4389-bfa5-9c62fcc95132
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398069(v=OCS.15)
ms:contentKeyID: 49299481
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare server proxy inversi per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-05-08_

Per le distribuzioni di Edge Server di Microsoft Lync Server 2013, è necessario che nella rete perimetrale sia presente un proxy inverso HTTPS in modo che i client esterni possano accedere ai servizi Web di Lync Server 2013 (denominati *componenti Web* in Office Communications Server) nel director e nel pool principale dell'utente. Di seguito sono riportate alcune funzionalità che richiedono l'accesso esterno tramite un proxy inverso:

  - Consentire agli utenti esterni di scaricare il contenuto delle riunioni.

  - Consentire agli utenti esterni di espandere i gruppi di distribuzione.

  - Consentire agli utenti remoti di scaricare file dal servizio Rubrica.

  - Accedere al client Lync Web App.

  - Accedere alla pagina Web Impostazioni conferenza telefonica con accesso esterno.

  - Consentire ai dispositivi esterni di connettersi al servizio Web di aggiornamento dispositivi e ottenere gli aggiornamenti.

  - Consentire alle applicazioni mobili di individuare automaticamente e utilizzare gli URL per dispositivi mobili (MCX) da Internet.

  - Consentire al client di Lync 2013, all' app Windows Store Lync e al client mobile di Lync 2013 di individuare gli URL di Lync Discover (individuazione automatica) e utilizzare l'API Web Unified Communications.

È consigliabile configurare il proxy inverso HTTP per pubblicare tutti i servizi Web in tutti i pool. Se si pubblica https:// *FQDNesterno* /\*, vengono pubblicate tutte le directory virtuali IIS per un pool. È necessaria una regola di pubblicazione per ogni server Standard Edition, per ogni pool Front End, nonché per ogni Server Director o pool di server Director presente nell'organizzazione.

È inoltre necessario pubblicare gli URL semplici. Se l'organizzazione dispone di un Server Director o di un pool di server Director, il proxy inverso HTTP resterà in attesa delle richieste HTTP/HTTPS relative agli URL semplici e le invierà tramite proxy alla directory virtuale dei servizi Web esterni nel Server Director o nel pool di server Director. Se non è stato distribuito un Server Director, sarà necessario designare un pool per la gestione delle richieste dirette agli URL semplici. Se non si tratta del pool principale dell'utente, le richieste verranno reindirizzate ai servizi Web nel pool principale. Gli URL semplici possono essere gestiti da una regola di pubblicazione Web dedicata oppure possono essere aggiunti i ai nomi pubblici della regola di pubblicazione Web per il Server Director. È inoltre necessario pubblicare l'URL del servizio di individuazione automatica esterno.

È possibile utilizzare Microsoft Forefront Threat Management Gateway 2010, Microsoft Internet Security and Acceleration (ISA) Server 2006 SP1 o Internet Information Server 7.0, 7.5 o 8.0 con Application Request Routing (IIS ARR) come proxy inverso. Nei passaggi dettagliati di questa sezione viene descritto come configurare Forefront Threat Management Gateway 2010, in quanto i passaggi per configurare ISA Server 2006 sono praticamente identici. Vengono inoltre fornite istruzioni per IIS ARR. Se si utilizza un altro proxy inverso, consultare la documentazione relativa a tale prodotto e controllare le caratteristiche che corrispondono ai requisiti definiti qui.

> [!important]  
> Internet Information Server Application Request Routing (IIS ARR) è un prodotto completamente testato e supportato per l'implementazione di un proxy inverso per Lync Server 2010 e Lync Server 2013. Nel novembre del 2012 Microsoft ha sospeso la vendita delle licenze di ForeFront Threat Management Gateway 2010 o TMG, che rimane comunque un prodotto completamente supportato e viene ancora venduto nei dispositivi di terze parti. Il supporto per il proxy inverso viene inoltre fornito con numerosi firewall e dispositivi per il bilanciamento del carico hardware. Se si utilizzano tali firewall o dispositivi per il bilanciamento del carico hardware, chiedere al fornitore le istruzioni specifiche su come configurare questi prodotti per il supporto del proxy inverso per Lync Server. È inoltre possibile che determinate terze parti abbiano fornito a Microsoft la documentazione per i propri prodotti. Per le soluzioni di terze parti, i fornitori stessi forniscono in genere il supporto necessario. Per un elenco di terze parti attive nel fornire soluzioni, vedere la <a href="http://go.microsoft.com/fwlink/?linkid=268730">pagina delle infrastrutture qualificate per Microsoft Lync</a>.

Gli argomenti e le procedure seguenti utilizzano Forefront Threat Management Gateway 2010 e IIS ARR come base per le procedure di distribuzione e configurazione.

  - [Configurare i nomi di dominio completi (FQDN) delle Web farm per Lync Server 2013](lync-server-2013-configure-web-farm-fqdns.md)

  - [Configurare le schede di rete in Lync Server 2013](lync-server-2013-configure-network-adapters.md)

  - [Richiedere e configurare un certificato per il proxy inverso HTTP in Lync Server 2013](lync-server-2013-request-and-configure-a-certificate-for-your-reverse-http-proxy.md)

  - [Configurare le regole di pubblicazione Web per un singolo pool interno in Lync Server 2013](lync-server-2013-configure-web-publishing-rules-for-a-single-internal-pool.md)

  - [Verificare o configurare l'autenticazione e la certificazione nelle directory virtuali IIS in Lync Server 2013](lync-server-2013-verify-or-configure-authentication-and-certification-on-iis-virtual-directories.md)

  - [Creare record DNS per server proxy inversi in Lync Server 2013](lync-server-2013-create-dns-records-for-reverse-proxy-servers.md)

  - [Verificare l'accesso tramite il proxy inverso in Lync Server 2013](lync-server-2013-verify-access-through-your-reverse-proxy.md)

## Operazioni preliminari

Per una distribuzione corretta di Forefront Threat Management Gateway 2010 come proxy inverso, è necessario impostare e configurare un server utilizzando i prerequisiti e i requisiti hardware definiti nella documentazione di Forefront Threat Management Gateway 2010. Per configurare correttamente l'hardware e installare Forefront Threat Management Gateway 2010 sul server prima di continuare, vedere gli argomenti seguenti.

  -   
    [Forefront Threat Management Gateway (TMG) 2010](http://go.microsoft.com/fwlink/?linkid=291292)

  -   
    [Specifiche hardware di Forefront TMG 2010](http://go.microsoft.com/fwlink/?linkid=291293)

Per una distribuzione corretta di IIS ARR come proxy inverso, è necessario configurare l'hardware e i prerequisiti software come illustrato negli argomenti seguenti.

  -   
    Per installare IIS in Windows Server 2008 o Windows Server 2008 R2, consultare le istruzioni sull' [installazione di IIS 7 in Windows Server 2008 o Windows Server 2008 R2](http://go.microsoft.com/fwlink/?linkid=291296)

  -   
    Per installare IIS in Windows Server 2012, consultare le istruzioni sull' [installazione di IIS 8 in Windows Server 2012](http://go.microsoft.com/fwlink/?linkid=291297)

  -   
    Per installare IIS in Windows Server 2012 R2, vedere [Installazione di IIS 8.5 in Windows Server 2012 R2](http://go.microsoft.com/fwlink/?linkid=330687)

  -   
    Per scaricare l'estensione di Application Request Routing per IIS, seguire le istruzioni della [pagina per il download di Application Request Routing v2.5](http://go.microsoft.com/fwlink/?linkid=291298)

  -   
    Per installare ARR, seguire le istruzioni della [pagina sull'installazione di Application Request Routing Version 2](http://go.microsoft.com/fwlink/?linkid=291299)
    

    > [!NOTE]
    > Le istruzioni attualmente disponibili sono per ARR 2.0. I passaggi da eseguire per l'installazione dell'estensione sono uguali per entrambe le versioni.


