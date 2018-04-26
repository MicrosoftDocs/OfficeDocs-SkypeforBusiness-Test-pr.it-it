---
title: Get-CsUserDatabaseState
TOCTitle: Get-CsUserDatabaseState
ms:assetid: c90150cd-fdb0-4c79-af58-c9ad884cb043
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398831(v=OCS.15)
ms:contentKeyID: 49301969
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsUserDatabaseState

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sullo stato online (True o False) di uno o più database utenti di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsUserDatabaseState [-RegistrarPool <Fqdn>] <COMMON PARAMETERS>

    Get-CsUserDatabaseState [-Identity <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS:

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 viene restituito lo stato online di ogni database utenti configurato per l'utilizzo nell'organizzazione.

    Get-CsUserDatabaseState

## ESEMPIO 2

Con il comando mostrato nell'esempio 2 viene restituito lo stato online di un solo database utenti: ovvero il database con identità UserDatabase:atl-sql-001.litwareinc.com.

    Get-CsUserDatabaseState -Identity "UserDatabase:atl-sql-001.litwareinc.com"

## ESEMPIO 3

Nell'esempio 3 le informazioni sullo stato vengono restituite per tutti i database utenti inclusi nel pool di registrazione atl-cs-001.litwareinc.com.

    Get-CsUserDatabaseState -RegistrarPool "atl-cs-001.litwareinc.com"\

## ESEMPIO 4

Nell'esempio 4 le informazioni vengono restituite per tutti i database utenti attualmente online. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsUserDatabaseState** senza alcun parametro. Viene restituita una raccolta di tutti i database utenti un uso nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona unicamente i database con proprietà Online uguale a True.

    Get-CsUserDatabaseState | Where-Object {$_.Online -eq $True}

## Descrizione dettagliata

In Lync Server i database utenti (conosciuti anche come archivi personali) vengono utilizzati per gestire informazioni sulla presenza e il routing relative agli utenti di Lync Server. Il cmdlet **Get-CsUserDatabaseState** consente di verificare lo stato corrente, online oppure offline, di qualsiasi database utenti attualmente in uso nell'organizzazione.

Per impostazione predefinita, le eccezioni del firewall per SQL Server Express non sono abilitate quando si installa Lync Server Standard Edition. Non sarà quindi possibile eseguire il cmdlet **Get-CsUserDatabaseState** da un'istanza remota di Windows PowerShell. Il comando infatti non potrà attraversare il firewall e accedere al database di SQL Server Express. Sarà comunque possibile eseguire il cmdlet localmente, ovvero sul server Standard Edition. Per eseguire il cmdlet **Get-CsUserDatabaseState** da postazione remota, tuttavia, sarà necessario abilitare manualmente le eccezioni del firewall di SQL Server Express.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsUserDatabaseState** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsUserDatabaseState"}

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
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Identificatore univoco del database utenti di cui deve essere restituito lo stato online. Ad esempio: -Identity &quot;UserDatabase:atl-sql-001.litwareinc.com&quot;.</p>
<p>Non è possibile utilizzare i parametri Identity e RegistrarPool nello stesso comando né specificare caratteri jolly in questi parametri. Se si omettono entrambi i parametri, il cmdlet <strong>Get-CsUserDatabaseState</strong> restituirà informazioni su tutti i database utenti attualmente in uso.</p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPool</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del pool Registrar che ospita i database utenti di cui restituire lo stato online. Ad esempio: -RegistrarPool &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p>Non è possibile utilizzare i parametri Identity e RegistrarPool nello stesso comando, né specificare caratteri jolly in questi parametri. Se si omettono entrambi i parametri, <strong>Get-CsUserDatabaseState</strong> restituirà informazioni su tutti i database utenti attualmente in uso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsUserDatabaseState** non accetta input inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsUserDatabaseState** restituisce le istanze dell'oggetto Microsoft.Rtc.Management.Xds.UserStoreState.

## Vedere anche

#### Ulteriori risorse

[Set-CsUserDatabaseState](set-csuserdatabasestate.md)  
[Update-CsUserDatabase](update-csuserdatabase.md)

