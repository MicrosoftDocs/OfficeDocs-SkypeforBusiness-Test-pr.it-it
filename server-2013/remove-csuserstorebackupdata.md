---
title: Remove-CsUserStoreBackupData
TOCTitle: Remove-CsUserStoreBackupData
ms:assetid: 71c8e8ee-61c7-4737-bdac-8cfc80bac126
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205003(v=OCS.15)
ms:contentKeyID: 49300952
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsUserStoreBackupData

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove le informazioni non aggiornate dall'archivio utenti specificato. Per "informazioni non aggiornate" si intendono i dati utente di un pool di registrazione non più associato all'archivio utenti specificato. Si supponga ad esempio che i pool A e B inizialmente fossero associati e che ora tale associazione sia cambiata e interessi i pool A e C. Quando viene eseguito sul pool A, il cmdlet Remove-CsUserStoreBackupData rimuove le informazioni relative agli utenti del pool B. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsUserStoreBackupData -PoolFqdn <Fqdn> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 rimuove le informazioni dell'archivio utenti non aggiornate archiviate dal pool pool atl-cs-001.litwareinc.com e dal relativo pool di backup associato.

    Remove-CsUserStoreBackupData -PoolFqdn "atl-cs-001.litwareinc.com"

## Descrizione dettagliata

Lync Server 2013 consente di associare due pool. Quando si esegue questa operazione, ogni pool mantiene due insiemi di informazioni utente, le informazioni sugli utenti che risiedono nel pool in questione e le informazioni sugli utenti che risiedono nel pool associato. Mantenendo entrambi gli insiemi di informazioni utente, si consente al pool B di registrare e gestire gli utenti del pool A in caso di failover del pool A.

Se successivamente si modifica l'associazione tra questi due pool, i dati utente "extra" non verranno eliminati automaticamente dai due pool. Ad esempio, il pool A continuerà ad archiviare i dati per il pool B. Questi dati tuttavia non verranno più aggiornati e replicati. Il cmdlet **Remove-CsUserStoreBackupData** consente di eliminare dal pool B i dati non più necessari per il pool A.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati personalmente, dal prompt di Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsUserStoreBackupData"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Remove-CsUserStoreBackupData** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>PoolFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del pool in cui devono essere rimosse le informazioni degli utenti &quot;non aggiornate&quot;. Ad esempio:</p>
<p>–PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive cosa accadrebbe eseguendo il comando senza però eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Remove-CsUserStoreBackupData** non accetta input tramite pipeline.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Get-CsBackupServiceStatus](get-csbackupservicestatus.md)

