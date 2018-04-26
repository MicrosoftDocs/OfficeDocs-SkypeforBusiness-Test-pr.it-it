---
title: Get-CsWatcherNodeConfiguration
TOCTitle: Get-CsWatcherNodeConfiguration
ms:assetid: 20dae017-375c-4361-8d65-b56f4c09b375
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204739(v=OCS.15)
ms:contentKeyID: 49299906
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsWatcherNodeConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle impostazioni di configurazione dei nodi Watcher in uso nell'organizzazione. I nodi Watcher sono computer che utilizzano periodicamente transazioni sintetiche di Lync Server 2013 e Microsoft System Center Operations Manager per verificare il corretto funzionamento dei componenti di Lync Server. Le impostazioni di configurazione dei nodi Watcher indicano quali pool sono stati associati a un nodo Watcher. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsWatcherNodeConfiguration [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsWatcherNodeConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce informazioni su tutti i nodi Watcher configurati per l'utilizzo nell'organizzazione.

    Get-CsWatcherNodeConfiguration

## Esempio 2

Nell'esempio 2 vengono restituite informazioni sul nodo Watcher associato al pool.

    Get-CsWatcherNodeConfiguration -Identity "atl-cs-001.litwareinc.com"

## Esempio 3

Il comando riportato nell'esempio 3 restituisce informazioni su tutti i nodi Watcher i cui utenti di test includono l'utente con indirizzo SIP sip:kenmyer@litwareinc.com. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsWatcherNodeConfiguration** per restituire una raccolta di tutti i nodi Watcher dell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i nodi la cui proprietà TestUsers include l'indirizzo SIP sip:kenmyer@litwareinc.com.

    Get-CsWatcherNodeConfiguration | Where-Object {$_.TestUsers -contains "sip:kenmyer@litwareinc.com"}

## Esempio 4

Nell'esempio 4 vengono restituite informazioni su tutti i nodi Watcher che includono il tipo di test PSTN. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsWatcherNodeConfiguration** per restituire una raccolta di tutti i nodi Watcher dell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i nodi Watcher la cui proprietà ExtendedTests include (-matches) il valore stringa "TestType=PSTN".

    Get-CsWatcherNodeConfiguration | Where-Object {$_.ExtendedTests -match "TestType=PSTN"}

## Descrizione dettagliata

Se si utilizza Microsoft System Center Operations Manager per monitorare Lync Server 2013, è possibile configurare "nodi Watcher", ovvero computer che eseguono periodicamente e automaticamente transazioni sintetiche per verificare il corretto funzionamento di Lync Server. I nodi Watcher vengono assegnati ai pool e vengono gestiti utilizzando i cmdlet **CsWatcherNodeConfiguration**. Si noti che non è necessario installare nodi Watcher se si utilizza System Center Operations Manager. È comunque possibile monitorare il sistema senza utilizzare i nodi Watcher, con la differenza che le eventuali transazioni sintetiche che si desidera eseguire dovranno essere richiamate manualmente, poiché non vengono richiamate automaticamente da Operations Manager.

Il cmdlet **Get-CsWatcherNodeConfiguration** restituisce informazioni su tutti i nodi Watcher configurati per l'utilizzo nell'organizzazione.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsWatcherNodeConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsWatcherNodeConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare caratteri jolly per restituire uno o più nodi Watcher. Per restituire ad esempio tutti i nodi Watcher del dominio litwareinc.com, utilizzare la sintassi seguente:</p>
<p>-Filter &quot;*.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome di dominio completo del pool a cui è stato assegnato il nodo Watcher, ad esempio:</p>
<p>-Identity &quot;atl-cs-001.litwareinc.com&quot;</p>
<p>Se non si specifica questo parametro, il cmdlet <strong>Get-CsWatcherNodeConfiguration</strong> restituirà informazioni su tutti i nodi Watcher configurati per l'utilizzo nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione dei nodi Watcher dalla replica locale dell'archivio di gestione centrale anziché direttamente dall'archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsWatcherNodeConfiguration** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsWatcherNodeConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.WatcherNode.TargetPool\#Decorated.

## Vedere anche

#### Ulteriori risorse

[New-CsWatcherNodeConfiguration](new-cswatchernodeconfiguration.md)  
[Remove-CsWatcherNodeConfiguration](remove-cswatchernodeconfiguration.md)  
[Set-CsWatcherNodeConfiguration](set-cswatchernodeconfiguration.md)  
[Test-CsWatcherNodeConfiguration](test-cswatchernodeconfiguration.md)

