---
title: 'Lync Server 2013: Configurazione di IIS'
TOCTitle: Configurazione di IIS
ms:assetid: b458babf-bf64-43f0-8a8e-612f5096b63c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412871(v=OCS.15)
ms:contentKeyID: 49301720
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di IIS in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per eseguire questa procedura, è necessario aver eseguito l'accesso al server almeno come amministratore locale e utente di dominio.

Prima di poter configurare e installare il Front End Server per Lync Server 2013, Standard Edition o il primo Front End Server in un pool, è necessario installare e configurare il ruolo del server e i servizi Web per Internet Information Services (IIS).

> [!IMPORTANT]  
> Se l'organizzazione richiede di posizionare IIS e tutti i servizi Web in un'unità diversa dall'unità di sistema, è possibile modificare il percorso di installazione per i file di Lync Server 2013 nella finestra di dialogo del programma di installazione durante l'installazione iniziale degli strumenti di amministrazione di Lync Server 2013, che vengono installati prima di IIS. Se si installano i file del programma di installazione in questo percorso, incluso OCSCore.msi, anche il resto dei file di Lync Server 2013 verrà distribuito in questa unità. Per informazioni dettagliate, vedere <a href="lync-server-2013-install-lync-server-administrative-tools.md">Installare gli strumenti di amministrazione di Lync Server 2013</a>. Per informazioni dettagliate su come spostare la directory INETPUB distribuita da Server Manager di Windows durante l'installazione di IIS, vedere la pagina Web all'indirizzo <a href="http://go.microsoft.com/fwlink/?linkid=216888" class="uri">http://go.microsoft.com/fwlink/?linkid=216888</a>.

Nella tabella seguente vengono indicati i servizi ruolo di IIS 7.5 necessari.

### Servizi ruolo di IIS 7.5

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Intestazione ruolo</th>
<th>Servizio ruolo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Funzionalità HTTP comuni installate</p></td>
<td><p>Contenuto statico</p></td>
</tr>
<tr class="even">
<td><p>Funzionalità HTTP comuni installate</p></td>
<td><p>Documento predefinito</p></td>
</tr>
<tr class="odd">
<td><p>Funzionalità HTTP comuni installate</p></td>
<td><p>Errori HTTP</p></td>
</tr>
<tr class="even">
<td><p>Sviluppo applicazioni</p></td>
<td><p>ASP.NET</p>
<p>Windows Server 2012 richiede anche ASP.NET4.5</p></td>
</tr>
<tr class="odd">
<td><p>Sviluppo applicazioni</p></td>
<td><p>Estendibilità .NET</p></td>
</tr>
<tr class="even">
<td><p>Sviluppo applicazioni</p></td>
<td><p>Estensioni ISAPI (Internet Server API)</p></td>
</tr>
<tr class="odd">
<td><p>Sviluppo applicazioni</p></td>
<td><p>Filtri ISAPI</p></td>
</tr>
<tr class="even">
<td><p>Integrità e diagnostica</p></td>
<td><p>Registrazione HTTP</p></td>
</tr>
<tr class="odd">
<td><p>Integrità e diagnostica</p></td>
<td><p>Strumenti di registrazione</p></td>
</tr>
<tr class="even">
<td><p>Integrità e diagnostica</p></td>
<td><p>Funzionalità di traccia</p></td>
</tr>
<tr class="odd">
<td><p>Sicurezza</p></td>
<td><p>Autenticazione anonima (installata e abilitata per impostazione predefinita)</p></td>
</tr>
<tr class="even">
<td><p>Sicurezza</p></td>
<td><p>Autenticazione di Windows</p></td>
</tr>
<tr class="odd">
<td><p>Sicurezza</p></td>
<td><p>Autenticazione mapping certificati client</p></td>
</tr>
<tr class="even">
<td><p>Sicurezza</p></td>
<td><p>Filtro richieste</p></td>
</tr>
<tr class="odd">
<td><p>Prestazioni</p></td>
<td><p>Compressione contenuto statico</p>
<p>Compressione contenuto dinamico</p></td>
</tr>
<tr class="even">
<td><p>Strumenti di gestione</p></td>
<td><p>Console di gestione IIS</p></td>
</tr>
<tr class="odd">
<td><p>Strumenti di gestione</p></td>
<td><p>Strumenti e script di gestione IIS</p></td>
</tr>
</tbody>
</table>


Nel sistema operativo Windows Server 2008 R2 SP1 x64 è possibile utilizzare Windows PowerShell 2.0. È prima necessario importare il modulo ServerManager e quindi installare il ruolo e i servizi ruolo di IIS 7.5.

    Import-Module ServerManager

    Add-WindowsFeature Web-Server, Web-Static-Content, Web-Default-Doc, Web-Scripting-Tools, Web-Windows-Auth, Web-Asp-Net, Web-Log-Libraries, Web-Http-Tracing, Web-Stat-Compression, Web-Dyn-Compression, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Http-Errors, Web-Http-Logging, Web-Net-Ext, Web-Client-Auth, Web-Filtering, Web-Mgmt-Console


> [!NOTE]
> L'autenticazione anonima viene installata per impostazione predefinita con il ruolo del server IIS. È possibile gestire l'autenticazione anonima dopo l'installazione di IIS. Per istruzioni dettagliate, vedere "Abilitare l'autenticazione anonima (IIS 7)" all'indirizzo <A class=uri href="http://go.microsoft.com/fwlink/?linkid=203935">http://go.microsoft.com/fwlink/?linkid=203935</A>.



Nella tabella seguente vengono indicati i servizi ruolo di IIS 8.0 e IIS 8.5 necessari per Windows Server 2012 e Windows Server 2012 R2.


> [!NOTE]
> Per Windows Server 2012 e Windows Server 2012 R2, il cmdlet Add-WindowsFeature è stato sostituito dal cmdlet Install-WindowsFeature. Per informazioni dettagliate, vedere <A href="http://go.microsoft.com/fwlink/p/?linkid=392274">Install-WindowsFeature</A>.



### Servizi ruolo di IIS 8.0 e IIS 8.5

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Intestazione ruolo</th>
<th>Servizio ruolo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Server Web (IIS)</p></td>
<td><p>Server Web</p></td>
</tr>
<tr class="even">
<td><p>Funzionalità HTTP comuni</p></td>
<td><p>Documento predefinito</p></td>
</tr>
<tr class="odd">
<td><p>Funzionalità HTTP comuni</p></td>
<td><p>Esplorazione directory</p></td>
</tr>
<tr class="even">
<td><p>Funzionalità HTTP comuni</p></td>
<td><p>Errori HTTP</p></td>
</tr>
<tr class="odd">
<td><p>Funzionalità HTTP comuni</p></td>
<td><p>Contenuto statico</p></td>
</tr>
<tr class="even">
<td><p>Funzionalità HTTP comuni</p></td>
<td><p>Reindirizzamento HTTP</p></td>
</tr>
<tr class="odd">
<td><p>Integrità e diagnostica</p></td>
<td><p>Registrazione HTTP</p></td>
</tr>
<tr class="even">
<td><p>Integrità e diagnostica</p></td>
<td><p>Strumenti di registrazione</p></td>
</tr>
<tr class="odd">
<td><p>Integrità e diagnostica</p></td>
<td><p>Monitor richieste</p></td>
</tr>
<tr class="even">
<td><p>Integrità e diagnostica</p></td>
<td><p>Funzionalità di traccia</p></td>
</tr>
<tr class="odd">
<td><p>Sicurezza</p></td>
<td><p>Filtro richieste</p></td>
</tr>
<tr class="even">
<td><p>Sicurezza</p></td>
<td><p>Autenticazione di base</p></td>
</tr>
<tr class="odd">
<td><p>Sicurezza</p></td>
<td><p>Autenticazione mapping certificati client</p></td>
</tr>
<tr class="even">
<td><p>Sicurezza</p></td>
<td><p>Autenticazione di Windows</p></td>
</tr>
<tr class="odd">
<td><p>Sviluppo applicazioni</p></td>
<td><p>Estendibilità .Net 3,5</p></td>
</tr>
<tr class="even">
<td><p>Sviluppo applicazioni</p></td>
<td><p>Estendibilità .Net 4.5</p></td>
</tr>
<tr class="odd">
<td><p>Sviluppo applicazioni</p></td>
<td><p>ASP.Net 3,5</p></td>
</tr>
<tr class="even">
<td><p>Sviluppo applicazioni</p></td>
<td><p>ASP.Net 4.5</p></td>
</tr>
<tr class="odd">
<td><p>Sviluppo applicazioni</p></td>
<td><p>Estensioni ISAPI</p></td>
</tr>
<tr class="even">
<td><p>Sviluppo applicazioni</p></td>
<td><p>Filtri ISAPI</p></td>
</tr>
<tr class="odd">
<td><p>Sviluppo applicazioni</p></td>
<td><p>Server-Side Include</p></td>
</tr>
<tr class="even">
<td><p>Strumenti di gestione</p></td>
<td><p>Console di gestione IIS</p></td>
</tr>
<tr class="odd">
<td><p>Strumenti di gestione</p></td>
<td><p>Compatibilità con la metabase di IIS 6</p></td>
</tr>
<tr class="even">
<td><p>Strumenti di gestione</p></td>
<td><p>Strumenti e script di gestione IIS</p></td>
</tr>
<tr class="odd">
<td><p>Funzionalità di .Net Framework 3,5</p></td>
<td><p>.Net Framework 3.5</p></td>
</tr>
<tr class="even">
<td><p>Funzionalità di .Net Framework 4.5</p></td>
<td><p>.Net Framework 4.5</p></td>
</tr>
<tr class="odd">
<td><p>Funzionalità di .Net Framework 4.5</p></td>
<td><p>ASP.Net 4.5</p></td>
</tr>
<tr class="even">
<td><p>Funzionalità di .Net Framework 4.5</p></td>
<td><p>Attivazione di HTTP</p></td>
</tr>
<tr class="odd">
<td><p>Funzionalità di .Net Framework 4.5</p></td>
<td><p>Condivisione di porta TCP</p></td>
</tr>
<tr class="even">
<td><p>Servizio trasferimento intelligente in background</p></td>
<td><p>Estensioni del server IIS</p></td>
</tr>
<tr class="odd">
<td><p>Servizi di riconoscimento della grafia</p></td>
<td><p>Servizi di riconoscimento della grafia</p></td>
</tr>
<tr class="even">
<td><p>Media Foundation</p></td>
<td><p>Media Foundation</p></td>
</tr>
<tr class="odd">
<td><p>Infrastruttura e interfacce utente</p></td>
<td><p>Infrastruttura e strumenti di gestione grafica</p></td>
</tr>
<tr class="even">
<td><p>Infrastruttura e interfacce utente</p></td>
<td><p>Esperienza desktop</p></td>
</tr>
<tr class="odd">
<td><p>Infrastruttura e interfacce utente</p></td>
<td><p>Shell grafica server</p></td>
</tr>
<tr class="even">
<td><p>Windows Identity Foundation 3.5</p></td>
<td><p>Windows Identity Foundation 3.5</p></td>
</tr>
<tr class="odd">
<td><p>Servizio Attivazione processo Windows</p></td>
<td><p>Modello di processo</p></td>
</tr>
<tr class="even">
<td><p>Servizio Attivazione processo Windows</p></td>
<td><p>API di configurazione</p></td>
</tr>
</tbody>
</table>


In Windows Server 2012 e Windows Server 2012 R2 è possibile utilizzare Windows PowerShell 3.0 per installare i requisiti di IIS. Utilizzando il modulo ServerManager in Windows PowerShell 3.0, digitare:

    Import-Module ServerManager

    Add-WindowsFeature Web-Server, Web-Static-Content, Web-Default-Doc, Web-Http-Errors, Web-Asp-Net, Web-Net-Ext, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Http-Logging, Web-Log-Libraries, Web-Request-Monitor, Web-Http-Tracing, Web-Basic-Auth, Web-Windows-Auth, Web-Client-Auth, Web-Filtering, Web-Stat-Compression, Web-Dyn-Compression, NET-Framework-45-Core, NET-WCF-HTTP-Activation45, Web-Asp-Net45, Web-Mgmt-Tools, Web-Scripting-Tools, Web-Mgmt-Console, Web-Mgmt-Compat, Windows-Identity-Foundation, Server-Media-Foundation, BITS -Source D:\sources\sxs

> [!IMPORTANT]  
> Il parametro -Source è una novità di Windows Server 2012 e definisce il percorso in cui è disponibile il supporto di origine di Windows Server 2012. Il supporto può essere definito come un'unità DVD (ad esempio, D:\Sources\Sxs) o come una condivisione di rete in cui sono stati copiati i file del supporto (ad esempio, \\fileserver\windows2012\sources\Sxs).

## Vedere anche

#### Concetti

[Requisiti di IIS per pool Front End e server Standard Edition in Lync Server 2013](lync-server-2013-iis-requirements-for-front-end-pools-and-standard-edition-servers.md)

