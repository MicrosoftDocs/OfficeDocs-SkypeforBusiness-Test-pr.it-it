---
title: Get-CsVoiceRoutingPolicy
TOCTitle: Get-CsVoiceRoutingPolicy
ms:assetid: 60245b7d-4e95-4925-aae5-c0fa1e9f38fc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204940(v=OCS.15)
ms:contentKeyID: 49300734
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoiceRoutingPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui criteri di routing vocale configurati per l'utilizzo nell'organizzazione. I criteri di questo tipo consentono di gestire gli utilizzi PSTN per gli utenti della funzionalità vocale ibrida. Tale funzionalità consente agli utenti presenti in Skype for Business online di avvalersi delle funzionalità di VoIP aziendale disponibili in un'installazione locale di Lync Server 2013. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsVoiceRoutingPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsVoiceRoutingPolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce informazioni su tutti i criteri di routing vocale configurati per l'utilizzo nell'organizzazione.

    Get-CsVoiceRoutingPolicy

## Esempio 2

Nell'esempio 2 vengono restituite informazioni su un singolo criterio di routing vocale, ovvero il criterio con identità (Identity) RedmondVoiceRoutingPolicy.

    Get-CsVoiceRoutingPolicy -Identity "RedmondVoiceRoutingPolicy"

## Esempio 3

Il comando riportato nell'esempio 3 restituisce informazioni su tutti i criteri di routing vocale configurati nell'ambito per utente. Per ottenere questo risultato, il comando utilizza il parametro Filter con valore "tag:\*". Questo valore di filtro restituisce solo i dati relativi ai criteri con identità (Identity) che inizia con il valore stringa "tag:".

    Get-CsVoiceRoutingPolicy -Filter "tag:*"

## Esempio 4

Nell'esempio 4 vengono restituite informazioni solo sui criteri di routing vocale che includono l'utilizzo PSTN "Long Distance". A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsVoiceRoutingPolicy** senza parametri. In questo modo viene restituita una raccolta di tutti i criteri di routing vocale configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i criteri in cui la proprietà PstnUsages include (-contains) l'utilizzo "Long Distance".

    Get-CsVoiceRoutingPolicy | Where-Object {$_.PstnUsages -contains "Long Distance"}

## Esempio 5

L'esempio 5 è una variante del comando riportato nell'esempio 4. In questo caso tuttavia vengono restituite informazioni solo sui criteri di routing vocale che non includono l'utilizzo PSTN "Long Distance". A tale scopo, il cmdlet **Where-Object** utilizza l'operatore -notcontains, che restituisce solo i dati relativi ai criteri che non includono l'utilizzo "Long Distance".

    Get-CsVoiceRoutingPolicy | Where-Object {$_.PstnUsages -notcontains "Long Distance"}

## Descrizione dettagliata

I criteri di routing vocale vengono utilizzati in scenari "ibridi", ovvero scenari in cui alcuni utenti sono situati nella versione locale di Lync Server e altri nella versione Skype for Business online. L'assegnazione di un criterio di routing vocale agli utenti di Skype for Business online consente loro di ricevere ed effettuare chiamate sulla rete PSTN (Public Switched Telephone Network) utilizzando i trunk SIP locali.

Si noti che la sola assegnazione di un criterio di routing vocale agli utenti non comporta l'abilitazione per le chiamate PSTN tramite Skype for Business online. Tali utenti dovranno essere abilitati anche per VoIP aziendale e dovranno disporre di un criterio vocale e di un dial plan appropriati.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli del controllo di accesso basato sui ruoli creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoiceRoutingPolicy"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet Get-CsVoiceRoutingPolicy non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Consente di utilizzare i caratteri jolly per recuperare uno o più criteri di routing vocale. Per restituire ad esempio tutti i criteri configurati nell'ambito per utente, utilizzare la sintassi seguente:</p>
<p>-Filter &quot;tag:*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco del criterio di routing vocale da recuperare. Per restituite il criterio globale, utilizzare la sintassi seguente:</p>
<p>-Identity global</p>
<p>Per restituire un criterio configurato nell'ambito del servizio, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;RedmondVoiceRoutingPolicy&quot;</p>
<p>Non è possibile utilizzare caratteri jolly quando si specifica l'identità.</p>
<p>Se non vengono specificati né il parametro Identity né il parametro Filter, il cmdlet <strong>Get-CsVoiceRoutingPolicy</strong> restituisce tutti i criteri di routing vocale configurati per l'utilizzo nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati dei criteri vocale dalla replica locale dell'archivio di gestione centrale anziché direttamente dall'archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsVoiceRoutingPolicy** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsVoiceRoutingPolicy** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceRoutingPolicy.

## Vedere anche

#### Ulteriori risorse

[Grant-CsVoiceRoutingPolicy](grant-csvoiceroutingpolicy.md)  
[New-CsVoiceRoutingPolicy](new-csvoiceroutingpolicy.md)  
[Remove-CsVoiceRoutingPolicy](remove-csvoiceroutingpolicy.md)  
[Set-CsVoiceRoutingPolicy](set-csvoiceroutingpolicy.md)

