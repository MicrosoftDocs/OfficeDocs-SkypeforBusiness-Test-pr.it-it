---
title: Get-CsManagementStoreReplicationStatus
TOCTitle: Get-CsManagementStoreReplicationStatus
ms:assetid: ea7162d6-d1e5-4301-b162-38da4e422293
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399052(v=OCS.15)
ms:contentKeyID: 49302374
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsManagementStoreReplicationStatus

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sul processo di replica di Lync Server, indicando anche se la replica è attualmente aggiornata per i computer Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsManagementStoreReplicationStatus [-ReplicaFqdn <String>] [-CentralManagementStoreStatus <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene chiamato il cmdlet **Get-CsManagementStoreReplicationStatus** senza alcun parametro. In questo modo viene restituito lo stato della replica (aggiornato o meno) per tutti i computer Lync Server.

    Get-CsManagementStoreReplicationStatus

## ESEMPIO 2

Nell'esempio 2 viene restituita una raccolta di tutti i computer in cui la replica non è aggiornata. A tale scopo, viene innanzitutto utilizzato il cmdlet **Get-CsManagementStoreReplicationStatus** per recuperare una raccolta contenente lo stato della replica per tutti i server. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che applica un filtro per limitare i dati restituiti ai computer in cui il valore della proprietà UpToDate è uguale a False.

    Get-CsManagementStoreReplicationStatus | Where-Object {$_.UpToDate -eq $False}

## ESEMPIO 3

Nell'esempio 3, i dati restituiti sono limitati a un singolo computer: atl-cs-001.litwareinc.com/

    Get-CsManagementStoreReplicationStatus -ReplicaFqdn atl-cs-001.litwareinc.com

## ESEMPIO 4

Nell'esempio 4 vengono restituite informazioni sui computer la cui ultima replica è stata eseguita prima delle 20.00 dell'11 agosto 2010. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsManagementStoreReplicationStatus** per restituire le informazioni sulla replica per tutti i computer Lync Server. Tali informazioni vengono quindi inviate tramite pipe al cmdlet **Where-Object**, che seleziona solo i computer in cui il valore della proprietà LastUpdateCreation è minore delle 20.00 dell'11 agosto 2010 (8/11/2010 8:00 PM). Per restituire le informazioni sui computer la cui ultima replica è stata eseguita dopo le 20.00 dell'11 agosto 2010, utilizzare l'operatore -gt (maggiore di):

Where-Object {$\_.LastUpdateCreation -gt "8/11/2010 8:00 PM"}

Per le date specificate in questo esempio vengono utilizzati valori di data e ora nel formato dell'inglese americano. Specificare le date utilizzando un formato compatibile con le impostazioni internazionali e della lingua in uso nel proprio sistema.

    Get-CsManagementStoreReplicationStatus | Where-Object {$_.LastUpdateCreation -lt "8/11/2010 8:00 PM"}

## ESEMPIO 5

Nel comando dell'esempio 5 viene utilizzato il parametro CentralManagementStoreStatus per restituire informazioni dettagliate sullo stato corrente dell'archivio di gestione centrale. Tali informazioni includono i nomi di dominio completi dei servizi dell'agente di trasferimento dei file e di Active Master, nonché la data e l'ora dell'ultimo heartbeat rilevato per ognuno di questi servizi.

    Get-CsManagementStoreReplicationStatus -CentralManagementStoreStatus

## Descrizione dettagliata

Quando un amministratore apporta qualsiasi tipo di modifica a Lync Server, ad esempio creando un nuovo criterio vocale o modificando le impostazioni di configurazione del server della Rubrica, tale modifica viene registrata nell'archivio di gestione centrale. Tale modifica deve quindi essere replicata in tutti i computer che eseguono i ruoli del server o i servizi di Lync Server.

Per replicare i dati, Master Replicator (in esecuzione nel server di gestione centrale) crea uno snapshot dei dati di configurazione modificati e una copia di questo snapshot viene quindi inviata a ogni computer che esegue ruoli del server o servizi di Lync Server. In tali computer un agente di replica riceve lo snapshot e carica i dati modificati. L'agente quindi invia a Master Replicator un messaggio in cui è indicato l'ultimo stato della replica.

Il cmdlet **Get-CsManagementStoreReplicationStatus** consente di verificare lo stato della replica di qualsiasi o di tutti i computer Lync Server dell'organizzazione.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsManagementStoreReplicationStatus** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsManagementStoreReplicationStatus"}

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
<td><p><em>CentralManagementStoreStatus</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce ulteriori informazioni sullo stato corrente dell'archivio di gestione centrale, tra cui un elenco delle repliche attive e di quelle eliminate, nonché la posizione dei servizi dell'agente di trasferimento dei file e di Active Master.</p></td>
</tr>
<tr class="even">
<td><p><em>ReplicaFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo (FQDN) del computer di cui deve essere verificato lo stato della replica. Ad esempio: -ReplicaFqdn &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p>Se il parametro non è incluso, verranno restituite le informazioni sullo stato della replica per tutti i computer Lync Server.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsManagementStoreReplicationStatus** non accetta input inviato tramite pipeline.

## Tipi restituiti

Per impostazione predefinita, il cmdlet **Get-CsManagementStoreReplicationStatus** restituisce istanze dell'oggetto Microsoft.Rtc.Management.Xds.ReplicaState. Se viene utilizzato il parametro CentralManagementStoreStatus, il cmdlet restituirà le istanze dell'oggetto Microsoft.Rtc.Management.Xds.CentralManagementStoreStatusResult.

## Vedere anche

#### Ulteriori risorse

[Invoke-CsManagementStoreReplication](invoke-csmanagementstorereplication.md)

