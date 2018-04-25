---
title: Get-CsPoolBackupRelationship
TOCTitle: Get-CsPoolBackupRelationship
ms:assetid: 230bbb04-b4cb-410f-8284-00740558655d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204745(v=OCS.15)
ms:contentKeyID: 49299932
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPoolBackupRelationship

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sul pool di backup associato a un pool di Skype for Business online. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsPoolBackupRelationship -PoolFqdn <Fqdn> [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato in questo esempio restituisce informazioni sulla relazione di backup assegnata al pool atl-cs-001.litwareinc.com.

    Get-CsPoolBackupRelationship -PoolFqdn "atl-cs-001.litwareinc.com"

## Descrizione dettagliata

Il cmdlet **Get-CsPoolBackupRelationship** restituisce il nome di dominio completo del pool di backup associato a un pool di registrazione. Si noti che queste informazioni sono di sola lettura. Non esiste un cmdlet **Set-CsPoolBackupRelationship** corrispondente che consenta di utilizzare l'interfaccia della riga di comando Windows PowerShell per creare un'associazione di backup. I pool di backup devono essere assegnati invece utilizzando Generatore di topologie di Lync Server.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPoolBackupRelationship"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsPoolBackupRelationship** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Nome di dominio completo del pool di cui viene controllata la relazione di backup, ad esempio:</p>
<p>-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati relativi alla relazione di backup dalla replica locale dell'archivio di gestione centrale anziché direttamente dall'archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsPoolBackupRelationship** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsPoolBackupRelationship** restituisce istanze dell'oggetto Microsoft.Rtc.Management.Hadr.BackupService.BackupRelation.

