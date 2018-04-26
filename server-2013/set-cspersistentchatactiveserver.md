---
title: Set-CsPersistentChatActiveServer
TOCTitle: Set-CsPersistentChatActiveServer
ms:assetid: 88c0af42-cb47-4c34-bf54-9c134dcbb843
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205065(v=OCS.15)
ms:contentKeyID: 49301227
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPersistentChatActiveServer

 

_**Ultima modifica dell'argomento:** 2013-03-07_

Gestisce l'elenco dei server Chat persistente attivi. Un server attivo è un server Chat persistente (in un pool del servizio Chat persistente specificato) completamente operativo e in grado di accettare nuove connessioni client. I server del pool non contrassegnati come server attivi potrebbero essere operativi, ma attualmente non essere in grado di accettare nuove connessioni client. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsPersistentChatActiveServer -ActiveServers <PSListModifier> <COMMON PARAMETERS>

    Set-CsPersistentChatActiveServer -Swap <SwitchParameter> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Identity <XdsGlobalRelativeIdentity>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 aggiunge il server atl-gc-001.litwareinc.com alla raccolta di server Chat persistente attivi.

    Set-CsPersistentChatActiveServer -Identity "global" -ActiveServers @{Add="atl-gc-001.litwareinc.com"}

## Esempio 2

Nell'esempio 2 il server atl-gc-001.litwareinc.com viene rimosso dalla raccolta di server Chat persistente attivi.

    Set-CsPersistentChatActiveServer -Identity "global" -ActiveServers @{Remove="atl-gc-001.litwareinc.com"}

## Esempio 3

Il comando riportato nell'esempio 3 rimuove tutti i server Chat persistente attivi. La rimozione di tutti i server attivi in genere viene eseguita in uno scenario di failback o di failover.

    Set-CsPersistentChatActiveServer -Identity "global" -ActiveServers $Null

## Descrizione dettagliata

Il cmdlet **Set-CsPersistentChatActiveServer** consente agli amministratori di abilitare o disabilitare il servizio Chat persistente in uno o più server in un pool di Chat persistente. I server riportati nell'elenco dei server attivi sono in grado di accettare nuove connessioni client. I server non inclusi nell'elenco invece non sono in grado di accettare nuove connessioni client. Il server tuttavia continuerà a gestire le eventuali connessioni client effettuate prima della rimozione dall'elenco. Per abilitare il servizio Chat persistente in un server Chat persistente, aggiungere il server all'elenco dei server attivi. Per disabilitare il servizio, rimuovere il server dall'elenco dei server attivi.

Per abilitare/disabilitare il servizio Chat persistente in tutti i server di un pool, utilizzare il cmdlet **Set-CsPersistentChatState**.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPersistentChatActiveServer"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Set-CsPersistentChatActiveServer** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>ActiveServers</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Raccolta di nomi di dominio completi che rappresentano i server Chat persistente attivi.</p></td>
</tr>
<tr class="even">
<td><p><em>Swap</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se si specifica questo parametro, verrà scambiato lo stato attivo di tutti i server Chat persistente del pool specificato. I server attivi verranno contrassegnati come non attivi e quelli non attivi verranno contrassegnati come attivi.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identità univoca per la raccolta di server attivi. È possibile disporre di una sola raccolta globale di server Chat persistente.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Set-CsPersistentChatActiveServer** non accetta input tramite pipeline.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Set-CsPersistentChatState](set-cspersistentchatstate.md)

