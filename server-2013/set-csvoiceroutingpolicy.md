---
title: Set-CsVoiceRoutingPolicy
TOCTitle: Set-CsVoiceRoutingPolicy
ms:assetid: cff51726-88c6-4cdf-aaad-a7246c4408c5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205313(v=OCS.15)
ms:contentKeyID: 49302035
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceRoutingPolicy

 

_**Ultima modifica dell'argomento:** 2015-05-28_

Modifica criteri di routing vocale esistenti. I criteri di routing vocale gestiscono gli utilizzi PSTN per gli utenti della funzionalità vocale ibrida. Questa funzionalità consente agli utenti ospitati in Skype for Business online di usufruire delle funzionalità di VoIP aziendale disponibili in un'installazione locale di Lync Server 2013. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsVoiceRoutingPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceRoutingPolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-Name <String>] [-PstnUsages <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando illustrato nell'esempio 1 consente di aggiungere l'utilizzo di PSTN "Lunga distanza" ai criteri di routing vocali RedmondVoiceRoutingPolicy per ogni singolo utente.

    Set-CsVoiceRoutingPolicy -Identity "RedmondVoiceRoutingPolicy" -PstnUsages @{Add="Long Distance"}

## Esempio 2

Nell'esempio 2 l'utilizzo di PSTN "Locale" viene rimosso dai criteri di routing vocali RedmondVoiceRoutingPolicy per ogni singolo utente.

    Set-CsVoiceRoutingPolicy -Identity "RedmondVoiceRoutingPolicy" -PstnUsages @{Remove="Local"}

## Esempio 3

Nell'esempio 3 l'utilizzo di PSTN "Locale" viene rimosso da tutti i criteri di routing vocale che includono questo utilizzo. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsVoiceRoutingPolicy** senza parametri per restituire una raccolta di tutti i criteri di routing vocali disponibili. Questa raccolta viene quindi inviata al cmdlet Where-Object che sceglie solo i criteri per i quali la proprietà PstnUsages include (-contains) l'utilizzo "Local". Questi criteri vengono quindi inviati tramite pipe al cmdlet **Set-CsVoiceRoutingPolicy** che elimina l'utilizzo Locale da tutti i criteri.

    Get-CsVoiceRoutingPolicy | Where-Object {$_.PstnUsages -contains "Local"} | Set-CsVoiceRoutingPolicy -PstnUsages @{Remove="Local"}

## Descrizione dettagliata

I criteri di routing vocale vengono utilizzati in scenari "ibridi", ovvero scenari in cui alcuni utenti sono ospitati nella versione locale di Lync Server e altri in Skype for Business online. L'assegnazione di criteri di routing vocale agli utenti di Skype for Business online consente loro di ricevere ed effettuare chiamate sulla rete PSTN (Public Switched Telephone Network) utilizzando i trunk SIP locali.

Si noti che la sola assegnazione di criteri di routing vocale agli utenti non comporta l'abilitazione per le chiamate PSTN tramite Skype for Business online. Tali utenti dovranno essere abilitati anche per VoIP aziendale e dovranno disporre di criteri vocali e di un dial plan appropriati.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceRoutingPolicy"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet Set-CsVoiceRoutingPolicy non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Richiede la conferma prima dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire testo esplicativo per i criteri di routing vocali. La descrizione potrebbe ad esempio includere informazioni sugli utenti a cui devono essere assegnati i criteri.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Impedisce la visualizzazione di eventuali messaggi di errore non irreversibili che potrebbero verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco assegnato ai criteri alla sua creazione. I criteri di routing vocali possono essere assegnati nell'ambito globale o nell'ambito di ogni singolo utente. Per fare riferimento all'istanza globale, utilizzare la seguente sintassi:</p>
<p>-Identity global</p>
<p>Per fare riferimento a criteri specifici di ogni utente, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;RedmondVoiceRoutingPolicy&quot;</p>
<p>Se non si specifica un valore Identity, il cmdlet <strong>Set-CsVoiceRoutingPolicy</strong> modificherà i criteri globali.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Consente di passare un riferimento a un oggetto al cmdlet anziché impostare singoli valori di parametri.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome descrittivo di questi criteri.</p></td>
</tr>
<tr class="odd">
<td><p><em>PstnUsages</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>A questi criteri di routing vocale è possibile applicare un elenco di utilizzi PSTN (ad esempio Local o Long Distance). L'utilizzo PSTN deve essere già esistente. Per recuperare gli utilizzi PSTN è possibile chiamare il cmdlet <strong>Get-CsPstnUsage</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive cosa accadrebbe se si eseguisse il comando senza eseguirlo effettivamente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Set-CsVoiceRoutingPolicy** accetta istanze da pipeline dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceRoutingPolicy.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsVoiceRoutingPolicy** modifica invece le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceRoutingPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsVoiceRoutingPolicy](get-csvoiceroutingpolicy.md)  
[Grant-CsVoiceRoutingPolicy](grant-csvoiceroutingpolicy.md)  
[New-CsVoiceRoutingPolicy](new-csvoiceroutingpolicy.md)  
[Remove-CsVoiceRoutingPolicy](remove-csvoiceroutingpolicy.md)

