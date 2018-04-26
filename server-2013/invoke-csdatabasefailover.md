---
title: Invoke-CsDatabaseFailover
TOCTitle: Invoke-CsDatabaseFailover
ms:assetid: 24b73e8e-948c-4e9c-bf4e-04ec0a229ffa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204744(v=OCS.15)
ms:contentKeyID: 49299944
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Invoke-CsDatabaseFailover

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Richiama il processo di failover di un database di Lync Server 2013 nel relativo database mirror. Al termine del failover, il database mirror diventa il database principale e gestisce tutte le nuove richieste per il database. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Invoke-CsDatabaseFailover -DatabaseType <Application | Archiving | Monitoring | User | Provision | CentralAdmin | Lyss | Registrar | Edge | PersistentChat | PersistentChatCompliance | CentralMgmt> -NewPrincipal <Primary | Mirror> -PoolFqdn <Fqdn> [-Confirm [<SwitchParameter>]] [-ExcludeDatabaseList <String[]>] [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 richiama il failover per il database User contenuto nel pool atl-cs-001.litwareinc.com. Il comando determina il failover del database User su un database mirror precedentemente assegnato.

    Invoke-CsDatabaseFailover -PoolFqdn atl-cs-001.litwareinc.com -DatabaseType "User" -NewPrincipal "Mirror"

## Esempio 2

Nell'esempio 2 viene eseguito il failover di tutti i database del pool atl-cs-001.litwareinc.com, ad eccezione dei database LcsCDR e LcsLog. Questi database vengono esclusi dal failover utilizzando il parametro ExcludeDatabaseList.

    Invoke-CsDatabaseFailover -PoolFqdn atl-cs-001.litwareinc.com -ExcludeDatabase -NewPrincipal "Mirror" -ExcludeDatabaseList "LcsCDR", "LcsLog"

## Descrizione dettagliata

Il cmdlet **Invoke-CsDatabaseFailover** consente agli amministratori di eseguire il "failover" di uno o più database di Lync Server 2013. Si supponga ad esempio di dover temporaneamente disconnettere il database primario, magari per effettuare un aggiornamento hardware. In tal caso è possibile utilizzare il cmdlet **Invoke-CsDatabaseFailover** per eseguire il failover dal database primario al database mirror. Quando si esegue questa operazione, tutte le richieste per il database in questione vengono instradate al database mirror. Successivamente, al termine dell'aggiornamento hardware, è possibile utilizzare lo stesso cmdlet per eseguire il failback nel database primario.

Si noti che i comandi in cui viene utilizzato il cmdlet **Invoke-CsDatabaseFailover** avranno esito negativo se non sono stati configurati un database primario e un database mirror per il database in questione.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Invoke-CsDatabaseFailover"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Invoke-CsDatabaseFailover** non sono disponibili nel Pannello di controllo di Lync Server.

## Parametri


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Obbligatorio</th>
<th>Tipo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DatabaseType</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.DatabaseNameType</p></td>
<td><p>Tipo di database di cui viene eseguito il failover. I valori validi sono:</p>
<p>Application</p>
<p>Archiving</p>
<p>CentralAdmin</p>
<p>CentralMgmt</p>
<p>Cls</p>
<p>Edge</p>
<p>Lyss</p>
<p>Monitoring</p>
<p>PersistentChat</p>
<p>PersistentChatCompliance</p>
<p>Provision</p>
<p>Registrar</p>
<p>User</p></td>
</tr>
<tr class="even">
<td><p><em>NewPrincipal</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.MirrorRole</p></td>
<td><p>Specifica se il failover verrà eseguito nel database primario o nel database mirror. I valori validi sono:</p>
<p>Mirror</p>
<p>Primary</p></td>
</tr>
<tr class="odd">
<td><p><em>PoolFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del pool contenente il database di cui eseguire il failover.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExcludeDatabaseList</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String[]</p></td>
<td><p>Elenco di database di cui non deve essere eseguito il failover, ad esempio:</p>
<p>-ExcludeDatabaseList &quot;LcsCDR&quot;</p>
<p>Per specificare più database di cui non deve essere eseguito il failover, separare i relativi nomi con le virgole:</p>
<p>-ExcludeDatabaseList &quot;LcsCDR&quot;, &quot;LcsLog&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando. Se il database corrente non è accessibile, verrà utilizzato inoltre il parametro Force.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera le informazioni sulla topologia dalla replica locale dell'archivio di gestione centrale anziché direttamente dall'archivio di gestione centrale.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet, ad esempio: -Report &quot;C:\Logs\DatabaseFailover.html&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Invoke-CsDatabaseFailover** non accetta input inviato tramite pipe.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Get-CsDatabaseMirrorState](get-csdatabasemirrorstate.md)  
[Install-CsMirrorDatabase](install-csmirrordatabase.md)

