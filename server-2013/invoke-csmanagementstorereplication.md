---
title: Invoke-CsManagementStoreReplication
TOCTitle: Invoke-CsManagementStoreReplication
ms:assetid: fa3dece3-afd8-4669-94f9-fc3b70201e81
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413060(v=OCS.15)
ms:contentKeyID: 49302542
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Invoke-CsManagementStoreReplication

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Forza i servizi di replica di Lync Server a inviare i dati di configurazione completi ai computer specificati. Questa operazione viene eseguita eliminando lo stato di replica dei computer dall'archivio di gestione centrale. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Invoke-CsManagementStoreReplication [-ReplicaFqdn <String>] [-Force <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 il cmdlet **Invoke-CsManagementStoreReplication** viene chiamato senza parametri. In questo modo si forza l'esecuzione della replica in tutti i computer Lync Server.

    Invoke-CsManagementStoreReplication

## ESEMPIO 2

Nell'esempio 2 il parametro ReplicaFQDN viene utilizzato quando si chiama il cmdlet **Invoke-CsManagementStoreReplication**. In questo modo la replica viene eseguita solo nel computer atl-cs-001.litwareinc.com.

    Invoke-CsManagementStoreReplication -ReplicaFqdn atl-cs-001.litwareinc.com

## Descrizione dettagliata

Quando un amministratore apporta qualsiasi tipo di modifica a Lync Server, ad esempio creando un nuovo criterio vocale o modificando le impostazioni di configurazione del server della Rubrica, tale modifica viene registrata nel archivio di gestione centrale. Tale modifica deve quindi essere replicata in tutti i computer che eseguono i servizi o i ruoli del server di Lync Server.

Per poter replicare i dati, Master Replicator (in esecuzione nel server di gestione centrale) crea uno snapshot dei dati di configurazione modificati e una copia di questo snapshot viene quindi inviata a ogni computer che esegue i servizi o i ruoli del server di Lync Server. In tali computer un agente di replica riceve lo snapshot e carica i dati modificati, quindi invia al Master Replicator un messaggio in cui è indicato lo stato aggiornato della replica.

La replica in genere non richiede l'intervento dell'utente ed consigliabile lasciare che l'intero processo di replica sia gestito dal Master Replicator. Tuttavia, in alcuni casi può essere necessario avviare forzatamente la replica in un computer o in un gruppo di computer senza attendere che il ciclo standard di repliche segua il suo corso. In tal caso, è possibile replicare forzatamente le informazioni in un computer utilizzando il cmdlet **Invoke-CsManagementStoreReplication**.

In genere la replica funziona su base incrementale. Quando si replicano i dati, ovvero, vengono replicate solo le modifiche anziché l'intero set dei dati di configurazione. Quando si chiama il cmdlet **Invoke-CsManagementStoreReplication**, si forza tuttavia una replica completa di tutti i dati anziché replicare solo le modifiche. La replica potrebbe non essere eseguita immediatamente quando si chiama il cmdlet **Invoke-CsManagementStoreReplication**. È possibile che vi sia un ritardo di due o tre minuti per consentire a Master Replicator di elaborare le modifiche.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Invoke-CsManagementStoreReplication** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Invoke-CsManagementStoreReplication"}

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
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>ReplicaFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del computer in cui avviare la replica. Ad esempio: -ReplicaFqdn &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p>Se questo parametro non è incluso, la replica verrà avviata in tutti i computer Lync Server.</p>
<p></p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Invoke-CsManagementStoreReplication** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Invoke-CsManagementStoreReplication** non restituisce alcun oggetto.

## Vedere anche

#### Ulteriori risorse

[Get-CsManagementStoreReplicationStatus](get-csmanagementstorereplicationstatus.md)

