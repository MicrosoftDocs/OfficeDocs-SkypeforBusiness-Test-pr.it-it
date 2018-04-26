---
title: Remove-CsVoiceRoutingPolicy
TOCTitle: Remove-CsVoiceRoutingPolicy
ms:assetid: 3729e908-5c0d-4970-bdff-5869ba2082c9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204799(v=OCS.15)
ms:contentKeyID: 49300177
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsVoiceRoutingPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Elimina un criterio di routing vocale esistente. I criteri di questo tipo gestiscono gli utilizzi PSTN per gli utenti della funzionalità vocale ibrida. Questa funzionalità consente agli utenti presenti in Skype for Business online di usufruire delle funzionalità di VoIP aziendale disponibili in un'installazione locale di Lync Server 2013. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsVoiceRoutingPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 elimina il criterio di routing vocale RedmondVoiceRoutingPolicy

    Remove-CsVoiceRoutingPolicy -Identity "RedmondVoiceRoutingPolicy"

## Esempio 2

Nell'esempio 2 vengono rimossi tutti i criteri di routing vocale configurati nell'ambito per utente. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsVoiceRoutingPolicy** con il parametro Filter. Il valore di filtro "tag:\*" restituisce solo i dati relativi ai criteri di routing vocale configurati nell'ambito per utente. Questi criteri per utente vengono quindi inviati tramite pipe al cmdlet **Remove-CsVoiceRoutingPolicy**, che li rimuove.

    Get-CsVoiceRoutingPolicy -Filter "tag:*" | Remove-CsVoiceRoutingPolicy

## Esempio 3

Nell'esempio 3 vengono rimossi tutti i criteri di routing vocale che includono l'utilizzo PSTN "Long Distance". A tale scopo, viene chiamato innanzitutto il cmdlet **Get-CsVoiceRoutingPolicy** senza parametri per restituire una raccolta di tutti i criteri di routing vocale disponibili. La raccolta viene quindi inviata tramite pipe al cmdlet Where-Object, che seleziona solo i criteri in cui la proprietà PstnUsages include (-contains) l'utilizzo "Long Distance". I criteri che soddisfano questo requisito vengono quindi inviati tramite pipe a **Remove-CsVoiceRoutingPolicy**, che rimuove ogni criterio di routing vocale che include l'utilizzo PSTN "Long Distance".

    Get-CsVoiceRoutingPolicy | Where-Object {$_.PstnUsages -contains "Long Distance"} | Remove-CsVoiceRoutingPolicy

## Descrizione dettagliata

I criteri di routing vocale vengono utilizzati in scenari "ibridi", ovvero scenari in cui alcuni utenti sono situati nella versione locale di Microsoft Lync Server 2013 e altri in Skype for Business online. L'assegnazione di un criterio di routing vocale agli utenti di Skype for Business online consente loro di ricevere ed effettuare chiamate telefoniche sulla rete PSTN (Public Switched Telephone Network) utilizzando i trunk SIP locali.

Si noti che la sola assegnazione di un criterio di routing vocale agli utenti non abilita automaticamente tali utenti per le chiamate PSTN tramite Skype for Business online. Tali utenti dovranno, tra l'altro, essere abilitati anche per VoIP aziendale e dovranno disporre di un criterio vocale e di un dial plan appropriati.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsVoiceRoutingPolicy"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Remove-CsVoiceRoutingPolicy** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco del criterio di routing vocale da rimuovere. Per &quot;rimuovere&quot; il criterio globale, utilizzare la sintassi seguente:</p>
<p>-Identity global</p>
<p>Si noti che in realtà il criterio globale non può essere rimosso, ma vengono ripristinati i valori predefiniti di tutte le proprietà.</p>
<p>Per rimuovere un criterio per utente, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;RedmondVoiceRoutingPolicy&quot;</p>
<p>Non è possibile utilizzare caratteri jolly quando si specifica un'identità (Identity) di criterio.</p></td>
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
<td><p>Se si specifica questo parametro, il criterio verrà rimosso automaticamente anche se è attualmente assegnato a un utente.</p>
<p>Se non si specifica questo parametro, il cmdlet <strong>Remove-CsVoiceRoutingPolicy</strong> non rimuoverà automaticamente un criterio per utente assegnato ad almeno un utente. Verrà invece visualizzato un messaggio in cui viene richiesto di confermare la rimozione del criterio. Per procedere con l'operazione e rimuovere il criterio, è necessario rispondere affermativamente (premendo il tasto Y).</p></td>
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

Il cmdlet **Remove-CsVoiceRoutingPolicy** accetta le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceRoutingPolicy inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsVoiceRoutingPolicy** invece elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceRoutingPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsVoiceRoutingPolicy](get-csvoiceroutingpolicy.md)  
[Grant-CsVoiceRoutingPolicy](grant-csvoiceroutingpolicy.md)  
[New-CsVoiceRoutingPolicy](new-csvoiceroutingpolicy.md)  
[Set-CsVoiceRoutingPolicy](set-csvoiceroutingpolicy.md)

