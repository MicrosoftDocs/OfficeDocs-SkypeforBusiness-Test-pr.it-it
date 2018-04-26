---
title: New-CsExtendedTest
TOCTitle: New-CsExtendedTest
ms:assetid: d4756daa-a4ce-4d74-926b-89754cf7e0b2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205275(v=OCS.15)
ms:contentKeyID: 49302095
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsExtendedTest

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un test del provider di servizi PSTN o di audioconferenza che può successivamente essere assegnato alla configurazione di un nodo Watcher. I nodi Watcher sono computer che utilizzano periodicamente transazioni sintetiche di Microsoft System Center Operations Manager e Lync Server 2013 per verificare il corretto funzionamento dei componenti di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    New-CsExtendedTest -Name <String> -TestType <AudioConferencingProvider | PSTN> [-TestUsers <PSListModifier>]

## Esempi

## Esempio 1

I comandi riportati nell'esempio 1 creano un nuovo test esteso (con TestType PSTN) e quindi aggiungono tale test esteso a un nuovo Watcher per il pool atl-cs-001.litwareinc.com. Nel primo comando dell'esempio, viene utilizzato il cmdlet **New-CsExtendedTest** per creare un test esteso denominato PSTN Test. Questo test include gli utenti test sip:kenmyer@litwareinc.com e sip:pilar@litwareinc.com. Si noti che questi due utenti test devono essere già stati configurati utilizzando il cmdlet **Set-CsTestUserCredential**. L'oggetto test esteso risultante viene quindi archiviato in una variabile denominata $x.

Nel secondo comando, il nuovo test esteso viene aggiunto al nodo Watcher appena creato per atl-cs-001.litwareinc.com. A tal fine, viene utilizzato il parametro ExtendedTests e la sintassi @{Add=$x}.

    $x = New-CsExtendedTest -TestUsers "sip:kenmyer@litwareinc.com", "sip:pilar@litwareinc.com" -Name "PSTN Test" -TestType "PSTN"
    
    New-CsWatcherNodeConfiguration -TargetFqdn "atl-cs-001.litwareinc.com" -PortNumber 5061 -TestUsers "sip:kenmyer@litwareinc.com","sip:pilar@litwareinc.com" -ExtendedTests @{Add=$x}

## Descrizione dettagliata

Se si utilizza Microsoft System Center Operations Manager per monitorare Lync Server 2013, è possibile configurare "nodi Watcher", ovvero computer che eseguono periodicamente e automaticamente transazioni sintetiche per verificare il corretto funzionamento di Lync Server. I nodi Watcher vengono assegnati ai pool e vengono gestiti utilizzando i cmdlet CsWatcherNodeConfiguration. Si noti che non è necessario installare nodi Watcher se si utilizza System Center Operations Manager. È comunque possibile monitorare il sistema senza utilizzare i nodi Watcher, con la differenza che le eventuali transazioni sintetiche che si desidera eseguire dovranno essere richiamate manualmente, poiché non vengono eseguite automaticamente da Operations Manager.

Quando si configura un nodo Watcher, è possibile aggiungere un test del provider di servizi PSTN o di audioconferenza come "test esteso". Questi test estesi possono essere utilizzati in sostituzione o in aggiunta all'set standard di test eseguiti da un computer con nodi Watcher. I test estesi devono essere creati utilizzando il cmdlet **New-CsExtendedTest** e quindi aggiunti al nodo Watcher appropriato.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsExtendedTest"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **New-CsExtendedTest** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome descrittivo assegnato al test esteso.</p></td>
</tr>
<tr class="even">
<td><p><em>TestType</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.WatcherNode.TestType</p></td>
<td><p>Tipo di test che verrà effettuato dal test esteso. I valori consentiti sono:</p>
<p>* PSTN</p>
<p>* AudioConferencingProvider</p>
<p>È possibile specificare un solo TestType per test esteso.</p></td>
</tr>
<tr class="odd">
<td><p><em>TestUsers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Indirizzo SIP degli account utente che fungeranno da utenti test. È possibile specificare più account separandoli con virgole, ad esempio:</p>
<p>–TestUsers &quot;sip:kenmyer@litwareinc.com&quot;, &quot;sip:pilar@litwareinc.com&quot;</p>
<p>È necessario specificare almeno due utenti test quando si utilizza il TestType PSTN.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsExtendedTest** non accetta input inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **New-CsExtendedTest** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.WatcherNode.ExtendedTest.

## Vedere anche

#### Ulteriori risorse

[New-CsWatcherNodeConfiguration](new-cswatchernodeconfiguration.md)  
[Set-CsWatcherNodeConfiguration](set-cswatchernodeconfiguration.md)

