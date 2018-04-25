---
title: Set-CsWatcherNodeConfiguration
TOCTitle: Set-CsWatcherNodeConfiguration
ms:assetid: 001b49ab-de17-4161-9d0c-9d5d9626558f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204620(v=OCS.15)
ms:contentKeyID: 49299476
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsWatcherNodeConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta esistente di impostazioni di configurazione dei nodi Watcher. I nodi Watcher sono computer che utilizzano periodicamente transazioni sintetiche di Lync Server 2013 e Microsoft System Center Operations Manager per verificare il corretto funzionamento dei componenti di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsWatcherNodeConfiguration [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsWatcherNodeConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-ExtendedTests <PSListModifier>] [-Force <SwitchParameter>] [-PortNumber <UInt16>] [-Tests <PSListModifier>] [-TestUsers <PSListModifier>] [-UseInternalWebUrls <$true | $false>] [-WhatIf [<SwitchParameter>]] [-XmppTestReceiverMailAddress <String>]

## Esempi

## Esempio 1

I comandi riportati nell'esempio 1 aggiungono un nuovo test di provider di servizi di audioconferenza alle impostazioni di configurazione dei nodi Watcher applicate al pool atl-cs-001.litwareinc.com. A tale scopo, il primo comando dell'esempio utilizza il cmdlet **New-CsExtendedTest** per creare il nuovo test. Questo test solo in memoria è archiviato nella variabile $x. Nel secondo comando il cmdlet **Set-CsWatcherNodeConfiguration** aggiunge il nuovo test alle impostazioni di configurazione dei nodi Watcher utilizzando il parametro ExtendedTests e la sintassi @{Add=$x}.

    $x = New-CsExtendedTest -TestUsers "sip:kenmyer@litwareinc.com", "sip:pilar@litwareinc.com" -Name "Audio Conferencing Test" -TestType "AudioConferencingProvider"
    
    Set-CsWatcherNodeConfiguration -Identity "atl-cs-001.litwareinc.com" -ExtendedTests @{Add=$x}

## Esempio 2

I comandi riportati nell'esempio 2 mostrano come rimuovere un test esteso da una raccolta di impostazioni di configurazione dei nodi Watcher. A tale scopo, il primo comando riportato nell'esempio utilizza il cmdlet **Get-CsWatcherNodeConfiguration** per restituire un riferimento oggetto alle impostazioni dei nodi Watcher per il pool atl-cs-001.litwareinc.com. Questo riferimento oggetto è archiviato in una variabile denominata $x.

Nel secondo comando viene utilizzato il metodo RemoveAt() per rimuovere il primo test esteso nel riferimento oggetto $x. I test estesi vengono archiviati come elementi in una matrice. Al primo elemento viene assegnato il numero di indice 0, al secondo il numero di indice 1 e così via. La sintassi RemoveAt(0) rimuove l'elemento con numero di indice 0, ovvero il primo elemento nell'insieme di test estesi. Per rimuovere il secondo test esteso, utilizzare la sintassi RemoveAt(1).

Dopo l'aggiornamento del riferimento oggetto, il comando finale utilizza il cmdlet **Set-CsWatcherNodeConfiguration** e il parametro Instance per scrivere le modifiche apportate al riferimento oggetto nelle impostazioni effettive dei nodi Watcher per il pool atl-cs-001.litwareinc.com.

    $x = Get-CsWatcherNodeConfiguration -Identity "atl-cs-001.litwareinc.com"
    
    $x.ExtendedTests.RemoveAt(0)
    
    Set-CsWatcherNodeConfiguration -Instance $x

## Esempio 3

Nell'esempio 3 vengono rimossi tutti i test estesi configurati per il nodo Watcher atl-cs-001.litwareinc.com. Questa attività viene eseguita includendo il parametro ExtendedTests con valore $Null.

    Set-CsWatcherNodeConfiguration -Identity "atl-cs-001.litwareinc.com" -ExtendedTests $Null

## Descrizione dettagliata

Se si utilizza Microsoft System Center Operations Manager per monitorare Lync Server 2013, è possibile configurare "nodi Watcher", ovvero computer che eseguono periodicamente e automaticamente transazioni sintetiche per verificare il corretto funzionamento di Lync Server. I nodi Watcher vengono assegnati ai pool e vengono gestiti utilizzando i cmdlet **CsWatcherNodeConfiguration**. Si noti che non è necessario installare nodi Watcher se si utilizza System Center Operations Manager. È comunque possibile monitorare il sistema senza utilizzare i nodi Watcher, con la differenza che le eventuali transazioni sintetiche che si desidera eseguire dovranno essere richiamate manualmente, anziché essere eseguite automaticamente da Operations Manager.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsWatcherNodeConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Set-CsWatcherNodeConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Abilita o disabilita il nodo Watcher. Il valore predefinito è True ($True).</p></td>
</tr>
<tr class="odd">
<td><p><em>ExtendedTests</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Riferimento oggetto a una o più istanze dell'oggetto ExtendedTest. Questi oggetti devono essere creati utilizzando il cmdlet <strong>New-CsExtendedTest</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome di dominio completo del pool associato alle impostazioni di configurazione del nodo Watcher.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSObject</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>PortNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta SIP utilizzata dal servizio di registrazione.</p></td>
</tr>
<tr class="even">
<td><p><em>Tests</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Transazioni sintetiche che devono essere eseguite dal nodo Watcher. I valori consentiti sono:</p>
<p>* Registration</p>
<p>* IM</p>
<p>* GroupIM</p>
<p>* P2PAV</p>
<p>* AvConference</p>
<p>* Presence</p>
<p>* ABS</p>
<p>* ABWQ</p>
<p>* MCXP2PIM</p>
<p>* ExumConnectivity</p>
<p>* JoinLauncher</p>
<p>* PersistentChatMessage</p>
<p>* DataConference</p>
<p>* XmppIM</p>
<p>* UnifiedContactStore</p>
<p>* AVEdgeConnectivity</p>
<p>Per abilitare test aggiuntivi per un nodo Watcher, utilizzare una sintassi simile alla seguente:</p>
<p>-Tests @{Add=&quot;ExumConnectivity&quot;,&quot;JoinLauncher&quot;,&quot;UnifiedContactStore&quot;}</p>
<p>Per disabilitare uno o più test da un nodo Watcher, utilizzare una sintassi simile alla seguente:</p>
<p>-Tests @{Remove=&quot;ABS&quot;,&quot;ABWQ&quot;}</p>
<p>Per disabilitare tutti i test per un nodo Watcher, impostare il valore del parametro Tests su $Null:</p>
<p>-Tests $Null</p></td>
</tr>
<tr class="odd">
<td><p><em>TestUsers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Indirizzi SIP degli utenti test utilizzati dal nodo Watcher. Per aggiungere ulteriori utenti test al nodo, utilizzare una sintassi simile alla seguente:</p>
<p>-TestUsers @{Add=&quot;sip:aidan@litwareinc.com&quot;}</p>
<p>Per rimuovere un utente test dal nodo Watcher, utilizzare una sintassi simile alla seguente:</p>
<p>-TestUsers @{Remove=&quot;sip:aidan@litwareinc.com&quot;</p>
<p>Per sostituire un utente esistente con un nuovo utente, utilizzare il metodo Replace. La sintassi seguente ad esempio consente di sostituire l'utente sip:pilar@litwareinc.com con il nuovo utente sip:aidan@litwareinc.com:</p>
<p>-TestUsers @{Replace=&quot;sip:pilar@litwareinc.com&quot;,&quot;sip:aidan@litwareinc.com&quot;}</p>
<p>Devono essere presenti almeno due utenti test per nodo Watcher. Se sono presenti due utenti e si tenta di rimuoverne uno, lasciando apparentemente il nodo con un solo utente test, il comando avrà esito negativo.</p></td>
</tr>
<tr class="even">
<td><p><em>UseInternalWebUrls</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True ($True), indica al nodo Watcher di utilizzare gli URL Web interni anziché quelli esterni. In questo modo, è possibile verificare la validità degli URL per gli utenti protetti dal firewall dell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
<tr class="even">
<td><p><em>XmppTestReceiverMailAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo di posta elettronica XMPP da utilizzare per il test del gateway XMPP.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Set-CsWatcherNodeConfiguration** accetta le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.WatcherNode.TargetPool\#Decorated inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsWatcherNodeConfiguration** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.WatcherNode.TargetPool\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsWatcherNodeConfiguration](get-cswatchernodeconfiguration.md)  
[New-CsWatcherNodeConfiguration](new-cswatchernodeconfiguration.md)  
[Remove-CsWatcherNodeConfiguration](remove-cswatchernodeconfiguration.md)  
[Test-CsWatcherNodeConfiguration](test-cswatchernodeconfiguration.md)

