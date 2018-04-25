---
title: Remove-CsWatcherNodeConfiguration
TOCTitle: Remove-CsWatcherNodeConfiguration
ms:assetid: 599c6d58-da3d-4f0b-bc1f-22ac3e33ec7f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204926(v=OCS.15)
ms:contentKeyID: 49300638
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsWatcherNodeConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una raccolta esistente di impostazioni di configurazione dei nodi Watcher. I nodi Watcher sono computer che utilizzano periodicamente transazioni sintetiche di Lync Server 2013 e System Center Operations Manager per verificare il corretto funzionamento dei componenti di Lync Server. Questo criterio è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsWatcherNodeConfiguration -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 rimuove le impostazioni di configurazione dei nodi Watcher applicate al pool atl-cs-001.litwareinc.com.

    Remove-CsWatcherNodeConfiguration -Identity "atl-cs-001.litwareinc.com"

## Esempio 2

Nell'esempio 2 vengono rimossi tutti i nodi Watcher configurati per l'utilizzo nell'organizzazione. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsWatcherNodeConfiguration** per restituire una raccolta di tutti i nodi Watcher. La raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsWatcherNodeConfiguration**, che rimuove ogni nodo Watcher della raccolta. In questo modo vengono rimossi efficacemente tutti i nodi Watcher dell'organizzazione.

    Get-CsWatcherNodeConfiguration | Remove-CsWatcherNodeConfiguration

## Esempio 3

Nell'esempio 3 vengono rimossi tutti i nodi Watcher che includono l'utente sip:kenmyer@litwareinc.com come utente di test. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsWatcherNodeConfiguration** per restituire una raccolta di tutti i nodi Watcher attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet Where-Object, che seleziona solo le impostazioni in cui la proprietà TestUsers include (-contains) l'utente sip:kenmyer@litwareinc.com. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsWatcherNodeConfiguration**, che rimuove ogni elemento della raccolta filtrata.

    Get-CsWatcherNodeConfiguration | Where-Object {$_.TestUsers -contains "sip:kenmyer@litwareinc.com"} | Remove-CsWatcherNodeConfiguration

## Descrizione dettagliata

Se si utilizza Microsoft System Center Operations Manager per monitorare Lync Server 2013, è possibile configurare "nodi Watcher", ovvero computer che eseguono periodicamente e automaticamente transazioni sintetiche per verificare il corretto funzionamento di Lync Server. I nodi Watcher vengono assegnati ai pool e vengono gestiti utilizzando i cmdlet **CsWatcherNodeConfiguration**. Si noti che non è necessario installare nodi Watcher se si utilizza System Center Operations Manager. È comunque possibile monitorare il sistema senza utilizzare i nodi Watcher, con la differenza che le eventuali transazioni sintetiche che si desidera eseguire dovranno essere richiamate manualmente perché non vengono richiamate automaticamente da Operations Manager.

Per rimuovere successivamente le autorizzazioni per un nodo Watcher, è possibile utilizzare il cmdlet **Remove-CsWatcherNodeConfiguration**. In alternativa, è possibile disabilitare temporaneamente (e successivamente abilitare di nuovo) un nodo Watcher utilizzando il cmdlet [Set-CsWatcherNodeConfiguration](set-cswatchernodeconfiguration.md).

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsWatcherNodeConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Remove-CsWatcherNodeConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome di dominio completo del pool a cui è stato assegnato il nodo Watcher da eliminare, ad esempio:</p>
<p>-Identity &quot;atl-cs-001.litwareinc.com&quot;</p></td>
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
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
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

Il cmdlet **Remove-CsWatcherNodeConfiguration** accetta le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.WatcherNode.TargetPool\#Decorated inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet Remove-CsWatcherNodeConfiguration invece elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.WatcherNode.TargetPool\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsWatcherNodeConfiguration](get-cswatchernodeconfiguration.md)  
[New-CsWatcherNodeConfiguration](new-cswatchernodeconfiguration.md)  
[Set-CsWatcherNodeConfiguration](set-cswatchernodeconfiguration.md)  
[Test-CsWatcherNodeConfiguration](test-cswatchernodeconfiguration.md)

