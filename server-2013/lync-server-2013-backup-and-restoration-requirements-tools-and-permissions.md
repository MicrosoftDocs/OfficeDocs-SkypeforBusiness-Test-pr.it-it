---
title: 'Requisiti di backup e ripristino: strumenti e autorizzazioni'
TOCTitle: 'Requisiti di backup e ripristino: strumenti e autorizzazioni'
ms:assetid: 35ec2e33-f33e-4f84-9e64-6550fd78aa52
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh202171(v=OCS.15)
ms:contentKeyID: 52062126
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti di backup e ripristino: strumenti e autorizzazioni

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questo argomento vengono indicati gli strumenti che è possibile utilizzare per il backup e il ripristino di Lync Server 2013, le autorizzazioni necessarie e la possibilità di eseguire i comandi localmente o in remoto. Nello specifico, questo argomento illustra gli strumenti per il backup e il ripristino forniti con Lync Server.

## Backup

Tutti i comandi necessari per il backup di Lync Server possono essere eseguiti tramite script e in remoto. Per eseguire il backup di Lync Server, utilizzare gli strumenti illustrati nella tabella seguente.

### Strumenti per il backup di Lync Server

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Per il backup di questo componente:</th>
<th>Utilizzare questo strumento o cmdlet:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dati di configurazione della topologia (Xds.mdf)</p></td>
<td><p>Export-CsConfiguration</p></td>
</tr>
<tr class="even">
<td><p>Dati del servizio Informazioni percorso (E9-1-1) (Lis.mdf)</p></td>
<td><p>Export-CsLisConfiguration</p></td>
</tr>
<tr class="odd">
<td><p>Dati di configurazione di Response Group (RgsConfig.mdf)</p></td>
<td><p>Export-CsRgsConfiguration</p></td>
</tr>
<tr class="even">
<td><p>Dati utente permanenti (database Rtcxds.mdf)</p>
<p>ID conferenza</p></td>
<td><p>Export-CsUserData</p></td>
</tr>
<tr class="odd">
<td><ul>
<li><p>Database di archiviazione (LcsLog.mdf)</p></li>
<li><p>Database di registrazione dettagli chiamata di monitoraggio (LcsCDR.mdf)</p></li>
<li><p>Database QoE di monitoraggio (QoEMetrics.mdf)</p></li>
</ul></td>
<td><p>Strumento dei database di SQL Server, ad esempio SQL Server Management Studio</p></td>
</tr>
<tr class="even">
<td><p>Database chat persistente (Mgc.mdf)</p></td>
<td><p>Procedure di backup di SQL Server o Export-CsPersistentChatData. Export-CsPersistentChatData esporta i dati chat persistente in un file.</p></td>
</tr>
<tr class="odd">
<td><p>Tutti gli archivi file: archivio file di Lync Server, archivio file di archiviazione</p>

> [!NOTE]
> Non eseguire il backup dei file denominati <STRONG>Meeting.Active</STRONG>. Questi file sono in uso e bloccati mentre è in corso una riunione.


</td>
<td><p>Strumento di gestione del file system standard, ad esempio Robocopy.</p></td>
</tr>
</tbody>
</table>


## Ripristino

Per ripristinare Lync Server, utilizzare gli strumenti descritti nella tabella seguente. Tutti i comandi necessari per ripristinare Lync Server possono essere eseguiti tramite script. Alcuni comandi possono essere eseguiti in remoto, mentre altri devono essere eseguiti localmente, come specificato nella tabella seguente.

### Strumenti per il ripristino di Lync Server

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Per eseguire questa operazione:</th>
<th>Utilizzare questo strumento o cmdlet:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Creare un computer nuovo o pulito</p></td>
<td><ul>
<li><p>Software di installazione del sistema operativo Windows</p></li>
<li><p>Software di installazione di SQL Server</p></li>
<li><p>Snap-in MMC (Microsoft Management Console) Certificati, per ripristinare certificati con una chiave privata esportabile</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Ripristinare dati dell'archivio file</p></td>
<td><p>Strumento di gestione del file system standard, ad esempio Robocopy</p></td>
</tr>
<tr class="odd">
<td><p>Ricreare database vuoti e impostare le autorizzazioni per gli elementi seguenti:</p>
<ul>
<li><p>archivio di gestione centrale</p></li>
<li><p>Server back-end</p></li>
<li><p>Database di monitoraggio</p></li>
<li><p>Database di archiviazione</p></li>
</ul></td>
<td><p>Install-CsDatabase</p></td>
</tr>
<tr class="even">
<td><p>Ripristinare il puntatore di Servizi di dominio Active Directory nell'archivio di gestione centrale</p>

> [!NOTE]
> Se a un certo punto si perde il punto di connessione del servizio, è possibile eseguire di nuovo questo cmdlet.


</td>
<td><p>Set-CsConfigurationStoreLocation</p></td>
</tr>
<tr class="odd">
<td><p>Importare la topologia, i criteri e le impostazioni di configurazione nell'archivio di gestione centrale (Xds.mdf)</p></td>
<td><p>Import-CsConfiguration</p></td>
</tr>
<tr class="even">
<td><p>Pubblicare e abilitare la topologia</p></td>
<td><p>Generatore di topologie</p>
<p>- oppure -</p>
<p>Publish-CsTopology e Enable-CsTopology</p></td>
</tr>
<tr class="odd">
<td><p>Abilitare l'ultima topologia pubblicata</p></td>
<td><p>Enable-CsTopology</p></td>
</tr>
<tr class="even">
<td><p>Reinstallare i componenti di Lync Server</p></td>
<td><p>Programma di installazione di Lync Server</p>

> [!NOTE]
> Contenuto nella cartella di installazione di Lync Server o sul supporto del prodotto in \setup\amd64\Setup.exe.


</td></tr>
<tr class="odd">
<td><p>Ripristinare i dati di Informazioni percorso (E9-1-1) (Lis.mdf)</p></td>
<td><p>Import-CsLisConfiguration</p></td>
</tr>
<tr class="even">
<td><p>Ripristinare i dati utente permanenti (Rtcxds.mdf)</p></td>
<td><p>Import-CsUserData</p></td>
</tr>
<tr class="odd">
<td><p>Ripristinare i dati di configurazione di Response Group (RgsConfig.mdf)</p></td>
<td><p>Import-CsRgsConfiguration</p>

> [!NOTE]
> Se la configurazione viene ripristinata in un nuovo pool senza dati Response Group nel database, utilizzare l'opzione -OverwriteOwner. Utilizzare questa opzione anche se i dati in corso di ripristino si trovano in un pool con lo stesso nome di dominio completo (FQDN). In caso contrario, l'importazione non verrà completata a causa degli oggetti contatto nei Response Group già esistenti in Active Directory.


</td></tr>
<tr class="even">
<td><p>Ripristinare i database seguenti:</p>
<ul>
<li><p>Database di archiviazione (LcsLog.mdf)</p></li>
<li><p>Database di monitoraggio: database di registrazione dettagli chiamata (LcsCDR.mdf) e database QoE (QoEMetrics.mdf)</p></li>
</ul></td>
<td><p>Strumenti di gestione dei database di SQL Server</p></td>
</tr>
<tr class="odd">
<td><p>Database chat persistente (Mgs.mdf)</p></td>
<td><p>Procedure di ripristino di SQL Server o Import-CsPersistentChatData. È possibile utilizzare Import-CsPersistentChatData con un file creato da Export-CsPersistentChatData e i dati verranno importati nel database chat persistente.</p></td>
</tr>
</tbody>
</table>


## Autorizzazioni necessarie

Gli utenti devono essere membri del gruppo **RTCUniversalServerAdmins** per eseguire tutti i comandi descritti in questo argomento. La maggior parte dei comandi di backup e ripristino non supporta il controllo di accesso basato sui ruoli (RBAC). Due eccezioni sono rappresentate dai cmdlet chat persistente Export-CsPersistentChatData e Import-CsPersistentChatData, che devono essere eseguiti da un utente membro del gruppo CsPersistentChatAdministrator. Per eseguire la Distribuzione guidata di Lync Server, un utente deve inoltre essere membro del gruppo Administrators locale.

