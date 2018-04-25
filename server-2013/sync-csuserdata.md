---
title: Sync-CsUserData
TOCTitle: Sync-CsUserData
ms:assetid: c385041f-f3f7-4db0-9ca7-b5f20a5d81d5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205242(v=OCS.15)
ms:contentKeyID: 49301907
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Sync-CsUserData

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Sincronizza i dati utente tra una coppia di pool di Lync Server 2013. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Sync-CsUserData -PoolFqdn <Fqdn> [-LocalStore <SwitchParameter>] [-RoutingGroup <String>] [-Target <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 sincronizza il pool atl-cs-001.litwareinc.com con il relativo pool di backup designato.

    Sync-CsUserData -PoolFqdn "atl-cs-001.litwareinc.com"

## Descrizione dettagliata

Il cmdlet **Sync-CsUserData** sincronizza i dati degli utenti tra un pool di registrazione e il pool di backup a esso assegnato. Si noti che le chiamate a questo cmdlet avranno esito negativo se nel pool in questione non è stato attivato il servizio di backup.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Sync-CsUserData"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Sync-CsUserData** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Nome di dominio completo del pool Lync Server 2013 primario. Esempio:</p>
<p>-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati utente dalla replica locale dell'Archivio di gestione centrale anziché dall'archivio stesso.</p></td>
</tr>
<tr class="odd">
<td><p><em>RoutingGroup</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di sincronizzare i dati solo per i gruppi di routing specificati. I gruppi di routing vengono utilizzati per indicare il Front End Server utilizzato dagli utenti per la registrazione.</p></td>
</tr>
<tr class="even">
<td><p><em>Target</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Sincronizza i dati con il pool di backup preassegnato.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Sync-CsUserData** non accetta output da pipeline.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Convert-CsUserData](convert-csuserdata.md)  
[Export-CsUserData](export-csuserdata.md)  
[Import-CsUserData](import-csuserdata.md)  
[Update-CsUserData](update-csuserdata.md)

