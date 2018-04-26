---
title: Test-CsWatcherNodeConfiguration
TOCTitle: Test-CsWatcherNodeConfiguration
ms:assetid: 085507a1-17e8-4dfa-aa6a-062620584335
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204652(v=OCS.15)
ms:contentKeyID: 49299596
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsWatcherNodeConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica le impostazioni di configurazione dei nodi Watcher in uso nell'organizzazione. I nodi Watcher sono computer che utilizzano periodicamente transazioni sintetiche di Lync Server 2013 e Microsoft System Center Operations Manager per verificare il corretto funzionamento dei componenti di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Test-CsWatcherNodeConfiguration [-FileName <String>] [-ReadCredentialsFromCurrentUserStore <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 verifica le impostazioni di configurazione per ogni nodo Watcher in uso nell'organizzazione.

    Test-CsWatcherNodeConfiguration

## Descrizione dettagliata

Se si utilizza Microsoft System Center Operations Manager per monitorare Lync Server 2013, è possibile configurare "nodi Watcher", ovvero computer che eseguono periodicamente e automaticamente transazioni sintetiche per verificare il corretto funzionamento di Lync Server. I nodi Watcher vengono assegnati ai pool e vengono gestiti utilizzando i cmdlet **CsWatcherNodeConfiguration**. Si noti che non è necessario installare nodi Watcher se si utilizza System Center Operations Manager. È comunque possibile monitorare il sistema senza utilizzare i nodi Watcher, con la differenza che le eventuali transazioni sintetiche che si desidera eseguire dovranno essere richiamate manualmente, poiché non vengono richiamate automaticamente da Operations Manager.

Il cmdlet **Test-CsWatcherNodeConfiguration** consente di verificare che un nodo Watcher sia stato configurato correttamente e sia stato assegnato a un pool di Lync Server 2013 valido. Si noti che il cmdlet **Test-CsWatcherNodeConfiguration** deve essere eseguito sul nodo Watcher stesso. Non può essere eseguito su computer remoti.

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Test-CsWatcherNodeConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>FileName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet, ad esempio:</p>
<p>-Report &quot;C:\Logs\WatcherNode.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>ReadCredentialsFromCurrentUserStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, indica al cmdlet <strong>Test-CsWatcherNodeConfiguration</strong> di recuperare le credenziali utente dall'archivio credenziali dell'utente. Per impostazione predefinita, il cmdlet <strong>Test-CsWatcherNodeConfiguration</strong> cerca le credenziali nell'archivio credenziali dell'account del servizio di rete.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsWatcherNodeConfiguration** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Test-CsWatcherNodeConfiguration** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Get-CsWatcherNodeConfiguration](get-cswatchernodeconfiguration.md)  
[New-CsWatcherNodeConfiguration](new-cswatchernodeconfiguration.md)  
[Remove-CsWatcherNodeConfiguration](remove-cswatchernodeconfiguration.md)  
[Set-CsWatcherNodeConfiguration](set-cswatchernodeconfiguration.md)

