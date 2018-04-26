---
title: New-CsWatcherNodeConfiguration
TOCTitle: New-CsWatcherNodeConfiguration
ms:assetid: c7f78c92-7965-4879-9efa-1b5adcd1881b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205254(v=OCS.15)
ms:contentKeyID: 49301920
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsWatcherNodeConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Assegna a un pool una nuova raccolta di impostazioni di configurazione dei nodi Watcher. I nodi Watcher sono computer che utilizzano periodicamente transazioni sintetiche di Microsoft System Center Operations Manager e Lync Server 2013 per verificare il corretto funzionamento dei componenti di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    New-CsWatcherNodeConfiguration -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    New-CsWatcherNodeConfiguration -TargetFqdn <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: -PortNumber <UInt16> [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-ExtendedTests <PSListModifier>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Tests <PSListModifier>] [-TestUsers <PSListModifier>] [-UseInternalWebUrls <$true | $false>] [-WhatIf [<SwitchParameter>]] [-XmppTestReceiverMailAddress <String>]

## Esempi

## Esempio 1

I comandi illustrati nell'esempio 1 consentono di creare una nuova raccolta di impostazioni di configurazione del nodo Watcher per il pool atl-cs-001.litwareinc.com. A tale scopo, i primi due comandi dell'esempio consentono di creare una coppia di utenti di prova del nodo Watcher (sip:kenmyer@litwareinc.com e sip:pilar@litwareinc.com). Dopo che gli utenti di prova sono stati creati, il terzo comando nell'esempio consente di creare un nuovo test PSTN esteso con i due utenti appena creati. Questo nuovo test, che in questo momento esiste solo in memoria, viene archiviato in una variabile denominata $x.

Infine, il quarto comando nell'esempio consente di creare le impostazioni di configurazione del nodo Watcher per atl-cs-001.litwareinc.com. Queste nuove impostazioni utilizzano la porta 5061, i due nuovi utenti di di prova e il test esteso archiviato nella variabile d$x.

    Set-CsTestUserCredential -SipAddress "sip:kenmyer@litwareinc.com" -UserName "litwareinc\kenmyer" -Password "07Apples"
    
    Set-CsTestUserCredential -SipAddress "sip:pilar@litwareinc.com" -UserName "litwareinc\pilar" -Password "07Apples"
    
    $x = New-CsExtendedTest -TestUsers "sip:kenmyer@litwareinc.com", "sip:pilar@litwareinc.com" -Name "PSTN Test" -TestType "PSTN"
    
    New-CsWatcherNodeConfiguration -TargetFqdn "atl-cs-001.litwareinc.com" -PortNumber 5061 -TestUsers "sip:kenmyer@litwareinc.com","sip:pilar@litwareinc.com"} -ExtendedTests @{Add=$x}

## Descrizione dettagliata

Se si utilizza Microsoft System Center Operations Manager per monitorare Lync Server 2013, è possibile configurare "nodi Watcher", ovvero computer che eseguono periodicamente e automaticamente transazioni sintetiche per verificare il corretto funzionamento di Lync Server. I nodi Watcher vengono assegnati ai pool e vengono gestiti utilizzando i cmdlet **CsWatcherNodeConfiguration**. Si noti che non è necessario installare nodi Watcher se si utilizza System Center Operations Manager. È comunque possibile monitorare il sistema senza utilizzare i nodi Watcher, con la differenza che le eventuali transazioni sintetiche che si desidera eseguire dovranno essere richiamate manualmente, anziché essere eseguite automaticamente da Operations Manager.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsWatcherNodeConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **New-CsWatcherNodeConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Nome di dominio completo del pool associato alle impostazioni di configurazione del nodo Watcher. È possibile utilizzare il parametro Identity o TargetFqdn per specificare il pool. Non è tuttavia possibile utilizzare entrambi questi parametri nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>PortNumber</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta SIP utilizzata dal servizio di registrazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del pool associato alle impostazioni di configurazione del nodo Watcher. È possibile utilizzare il parametro TargetFqdn o Identity per specificare il pool. Non è tuttavia possibile utilizzare entrambi questi parametri nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Abilita o disabilita il nodo Watcher. Il valore predefinito è True ($True).</p></td>
</tr>
<tr class="even">
<td><p><em>ExtendedTests</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Test PSTN o del provider di servizi di audioconferenza che è possibile assegnare alla configurazione di un nodo Watcher. Questi test devono essere creati utilizzando il cmdlet <strong>New-CsExtendedTest</strong> e archiviati in una variabile, ad esempio $x. Il test può quindi essere assegnato a un nodo Watcher utilizzando una sintassi simile alla seguente:</p>
<p>–ExtendedTests @{Add=$x}</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
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
<p>Per configurare i test al momento della creazione di un nuovo nodo Watcher, utilizzare la sintassi seguente, separando i singoli test con le virgole:</p>
<p>-Tests &quot;ABS&quot;,&quot;ABWQ&quot;,&quot;IM&quot;,&quot;GroupIM&quot;,&quot;XmppIM&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>TestUsers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Indirizzi SIP degli utenti test da assegnare al nodo Watcher. Questi account utente devono essere stati configurati in precedenza tramite il cmdlet <strong>Set-CsTestUserCredential</strong>. Per aggiungere utenti test, utilizzare una sintassi simile alla seguente, separando gli indirizzi utente con delle virgole:</p>
<p>–TestUsers &quot;sip:kenmyer@litwareinc.com&quot;,&quot;sip:pilar@litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>UseInternalWebUrls</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True ($True), indica al nodo Watcher di utilizzare gli URL Web interni anziché quelli esterni. In questo modo, è possibile verificare la validità degli URL per gli utenti protetti dal firewall dell'organizzazione.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
<tr class="odd">
<td><p><em>XmppTestReceiverMailAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo di posta elettronica XMPP da utilizzare per il test del gateway XMPP.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsWatcherNodeConfiguration** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **New-CsWatcherNodeConfiguration** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.WatcherNode.TargetPool\#Decorated.

