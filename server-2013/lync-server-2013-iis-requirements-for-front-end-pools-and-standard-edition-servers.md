---
title: 'Lync Server 2013: Requisiti di IIS per pool Front End e server Standard Edition'
TOCTitle: Requisiti di IIS per pool Front End e server Standard Edition
ms:assetid: e8a6c7ac-b6d5-4c7e-abe9-d8ea5eedbc62
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399038(v=OCS.15)
ms:contentKeyID: 49302312
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti di IIS per pool Front End e server Standard Edition in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per i server Standard Edition, i Front End Server e i Director, il programma di installazione di Lync Server 2013 crea directory virtuali in Internet Information Services (IIS) per gli scopi seguenti:

  - Consentire agli utenti di scaricare file dal servizio Rubrica

  - Consentire ai client di ottenere aggiornamenti

  - Abilitare le conferenze

  - Consentire agli utenti di scaricare il contenuto delle riunioni

  - Consentire agli utenti di espandere i gruppi di distribuzione

  - Abilitare le conferenze telefoniche

  - Abilitare le funzionalità di Response Group

Inoltre, l'aggiornamento cumulativo di novembre 2011 del programma di installazione di Lync Server 2010 crea directory virtuali in IIS per gli scopi seguenti:

  - In Front End Server o server Standard Edition, supportare la funzionalità di mobilità, ad esempio messaggistica istantanea e presenza, in dispositivi mobili

  - In Front End Server o server Standard Edition e in Director, consentire ai dispositivi mobili di rilevare automaticamente le risorse per la mobilità


> [!NOTE]
> Se si distribuiscono dispositivi mobili, è consigliabile utilizzare IIS 7.5. Il programma di installazione del servizio per dispositivi mobili Lync Server imposta alcuni contrassegni di ASP.NET per migliorare le prestazioni. IIS 7.5 viene installato per impostazione predefinita in Windows Server 2008 R2 e il programma di installazione del servizio per dispositivi mobili modifica automaticamente le impostazioni di ASP.NET. Se si utilizza IIS 7.0 in Windows Server 2008, è necessario modificare manualmente queste impostazioni.



Per Lync Server, è necessario installare i moduli IIS seguenti:

> [!IMPORTANT]  
> Se l'organizzazione richiede che IIS e tutti i servizi Web vengano posizionati in un'unità diversa da quella di sistema, è possibile cambiare il percorso di installazione dei file di Lync Server nella finestra di dialogo del programma di installazione. Se i file del programma di installazione, incluso OCSCore.msi, vengono installati in questo percorso, anche gli altri file di Lync Server verranno distribuiti in questa unità. Per informazioni dettagliate su come spostare la directory INETPUB distribuita da Server Manager di Windows durante l'installazione di IIS, vedere <a href="http://go.microsoft.com/fwlink/p/?linkid=216888">http://go.microsoft.com/fwlink/p/?linkId=216888</a>.

  - Contenuto statico

  - Documento predefinito

  - Errori HTTP

  - ASP.NET

  - Estendibilità .NET

  - Estensioni ISAPI (Internet Server API)

  - Filtri ISAPI

  - Registrazione HTTP

  - Strumenti di registrazione

  - Funzionalità di traccia

  - Autenticazione di Windows

  - Filtro richieste

  - Compressione contenuto statico

  - Compressione contenuto dinamico

  - Console di gestione IIS

  - Strumenti e script di gestione IIS

  - Autenticazione anonima (installata per impostazione predefinita insieme a IIS)

  - Autenticazione mapping certificati client

Nella tabella seguente vengono elencati gli URI delle directory virtuali per l'accesso interno e le risorse del file system a cui si riferiscono.

### Directory virtuali per l'accesso interno

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>URI directory virtuale</th>
<th>Riferimento</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Server della Rubrica</p></td>
<td><p>https:// <em>&lt;FQDN interno&gt;</em> /ABS/int/Handler</p></td>
<td><p>Percorso dei file di download del server della Rubrica per gli utenti interni.</p></td>
</tr>
<tr class="even">
<td><p>Servizio di individuazione automatica</p></td>
<td><p>https:// <em>&lt;FQDN interno&gt;</em> /Autodiscover</p></td>
<td><p>Percorso del servizio di individuazione automatica di Lync Server che individua le risorse di mobilità per gli utenti di dispositivi mobili interni.</p></td>
</tr>
<tr class="odd">
<td><p>Aggiornamenti client</p></td>
<td><p>http:// <em>&lt;FQDN interno&gt;</em> /AutoUpdate/Int</p></td>
<td><p>Percorso dei file di aggiornamento per i client interni basati su computer.</p></td>
</tr>
<tr class="even">
<td><p>Conf</p></td>
<td><p>http:// <em>&lt;FQDN interno&gt;</em> /Conf/Int</p></td>
<td><p>Percorso delle risorse per conferenze per utenti interni.</p></td>
</tr>
<tr class="odd">
<td><p>Aggiornamenti per i dispositivi</p></td>
<td><p>http:// <em>&lt;FQDN interno&gt;</em> /DeviceUpdateFiles_Int</p></td>
<td><p>Percorso dei file di aggiornamento per i dispositivi interni per comunicazioni unificate.</p></td>
</tr>
<tr class="even">
<td><p>Riunione</p></td>
<td><p>http:// <em>&lt;FQDN interno&gt;</em> /etc/place/null</p></td>
<td><p>Percorso del contenuto della riunione per utenti interni.</p></td>
</tr>
<tr class="odd">
<td><p>Servizio per dispositivi mobili</p></td>
<td><p>https:// <em>&lt;FQDN interno&gt;</em> /Mcx</p></td>
<td><p>Percorso delle risorse del servizio per dispositivi mobili per utenti interni.</p></td>
</tr>
<tr class="even">
<td><p>Servizio di espansione gruppo e query Web della Rubrica</p></td>
<td><p>http:// <em>&lt;FQDN interno&gt;</em> /GroupExpansion/int/service.asmx</p></td>
<td><p>Percorso del servizio Web che consente l'espansione gruppo per utenti interni. Inoltre, percorso del servizio di query Web della Rubrica che fornisce informazioni sugli elenchi di indirizzi globali ai client Lync MobileMicrosoft Lync 2010 Mobile interni.</p></td>
</tr>
<tr class="odd">
<td><p>Phone Conferencing</p></td>
<td><p>http:// <em>&lt;FQDN interno&gt;</em> /PhoneConferencing/Int</p></td>
<td><p>Percorso dei dati relativi alle conferenze telefoniche per utenti interni.</p></td>
</tr>
<tr class="even">
<td><p>Aggiornamenti per i dispositivi</p></td>
<td><p>http:// <em>&lt;FQDN interno&gt;</em> /RequestHandler</p></td>
<td><p>Percorso del gestore richieste del servizio Web di aggiornamento dispositivi che consente ai dispositivi per comunicazioni unificate interni di caricare log e verificare la presenza di aggiornamenti.</p></td>
</tr>
<tr class="odd">
<td><p>applicazione Response Group</p></td>
<td><p>http:// <em>&lt;FQDN interno&gt;</em> /RgsConfig</p>
<p>http:// <em>&lt;FQDN interno&gt;</em> /RgsClients</p></td>
<td><p>Percorso dello strumento di configurazione di Response Group.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Per pool Front End in una configurazione consolidata, è necessario distribuire IIS prima di poter aggiungere server al pool.


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398321.security(OCS.15).gif" title="security" alt="security" />SicurezzaNota:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>È necessario utilizzare lo snap-in di amminsitrazione di IIS per assegnare il certificato utilizzato dal server del componente Web IIS.</td>
</tr>
</tbody>
</table>