---
title: Set-CsUserDatabaseState
TOCTitle: Set-CsUserDatabaseState
ms:assetid: c4d8fe5e-ebc1-443b-943d-fc54649e94fd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412973(v=OCS.15)
ms:contentKeyID: 49301929
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUserDatabaseState

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Abilita o disabilita uno o più database utenti di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsUserDatabaseState -RegistrarPool <Fqdn> <COMMON PARAMETERS>

    Set-CsUserDatabaseState -Identity <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: -Online <$true | $false> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 mette il database utenti UserDatabase:atl-sql-001.litwareinc.com offline. Questa operazione può essere eseguita impostando la proprietà Online su $False.

    Set-CsUserDatabaseState -Identity "UserDatabase:atl-sql-001.litwareinc.com" -Online $False

## ESEMPIO 2

Nell'esempio 2, tutti i database utenti nel pool di registrazione atl-cs-001.litwareinc.com sono messi offline.

    Set-CsUserDatabaseState -RegistrarPool atl-cs-001.litwareinc.com -Online $False

## ESEMPIO 3

Nell'esempio 3 vengono individuati tutti i database degli utenti attualmente offline e li riporta online. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsUserDatabaseState** senza parametri in modo da restituire una raccolta di tutti i database degli utenti all'interno dell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona unicamente i database con proprietà Online uguale a False. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **ForEach-Object**, che utilizza ogni database della raccolta e imposta la proprietà Online su True. La raccolta di database offline deve essere inviata tramite pipe al cmdlet **ForEach-Object** anziché al cmdlet **Set-CsUserDatabaseState**. Quest'ultimo cmdlet non è infatti in grado di accettare direttamente le informazioni da pipeline.

    Get-CsUserDatabaseState | Where-Object {$_.Online -eq $False} | ForEach-Object {Set-CsUserDatabaseState -Identity $_.Identity -Online $True}

## Descrizione dettagliata

In Lync Server i database utenti (conosciuti anche come archivi personali) vengono utilizzati per gestire informazioni sulla presenza e il routing relative agli utenti di Lync Server. Il cmdlet **Set-CsUserDatabaseState** consente di cambiare lo stato di uno o più database utenti: è possibile utilizzare il cmdlet per mettere offline un database o per rimettere online un database disabilitato.

Per impostazione predefinita, le eccezioni del firewall per SQL Server Express non sono abilitate quando si installa Lync Server Standard Edition. Non sarà quindi possibile eseguire il cmdlet **Set-CsUserDatabaseState** da un'istanza remota di Windows PowerShell. Il comando infatti non potrà attraversare il firewall e accedere al database di SQL Server Express. Sarà comunque possibile eseguire il cmdlet localmente, ovvero sul server Standard Edition. Per eseguire il cmdlet **Set-CsUserDatabaseState** da postazione remota, tuttavia, sarà necessario abilitare manualmente le eccezioni del firewall di SQL Server Express.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsUserDatabaseState** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsUserDatabaseState"}

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
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Identificatore univoco del database utenti il cui stato online deve essere modificato. Ad esempio: -Identity &quot;UserDatabase:atl-sql-001.litwareinc.com&quot;.</p>
<p>Non è possibile utilizzare i parametri Identity e RegistrarPool nello stesso comando né specificare caratteri jolly in questi parametri.</p></td>
</tr>
<tr class="even">
<td><p><em>Online</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando è impostato su True ($True), rende disponibile il database online. Quando è impostato su False ($False), mette il database offline.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPool</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN) del pool di registrazione che ospita i database utenti il cui stato online deve essere modificato. Ad esempio: -RegistrarPool atl-cs-001.litwareinc.com.</p>
<p>Non è possibile utilizzare i parametri –Identity e –RegistrarPool nello stesso comando né caratteri jolly con entrambi i parametri.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
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
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa. Il cmdlet **Set-CsUserDatabaseState** accetta un valore stringa che rappresenta l'identità del database degli utenti da aggiornare.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsUserDatabaseState** modifica piuttosto le istanze esistenti dell'oggetto Microsoft.Rtc.Management.Xds.UserStoreState.

## Vedere anche

#### Ulteriori risorse

[Get-CsUserDatabaseState](get-csuserdatabasestate.md)  
[Update-CsUserDatabase](update-csuserdatabase.md)

