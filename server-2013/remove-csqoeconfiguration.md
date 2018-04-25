---
title: Remove-CsQoEConfiguration
TOCTitle: Remove-CsQoEConfiguration
ms:assetid: 3b50e857-c524-4aad-b191-d324fc7c837c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425879(v=OCS.15)
ms:contentKeyID: 49300248
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsQoEConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una raccolta di impostazioni di qualità percepita dagli utenti (QoE, Quality of Experience). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsQoEConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene utilizzato il cmdlet **Remove-CsQoEConfiguration** per rimuovere le impostazioni della qualità percepita dagli utenti (QoE) assegnate al sito Redmond. Utilizzando il parametro Identity, vengono rimosse solo le impostazioni assegnate al sito specificato.

    Remove-CsQoEConfiguration -Identity site:Redmond

## ESEMPIO 2

Il comando riportato nell'esempio 2 rimuove tutte le impostazioni della qualità percepita dagli utenti (QoE) assegnate nell'ambito del sito. A tale scopo, il comando innanzitutto utilizza il cmdlet **Get-CsQoEConfiguration** e il parametro Filter per recuperare le impostazioni QoE appropriate. La stringa con caratteri jolly "site:\*" fa in modo che vengano restituite solo le impostazioni la cui identità inizia con site:. La raccolta filtrata viene quindi passata al cmdlet **Remove-CsQoEConfiguration**, che elimina tutti gli elementi della raccolta.

    Get-CsQoEConfiguration -Filter site:* | Remove-CsQoEConfiguration

## ESEMPIO 3

Nell'esempio 3 vengono eliminate tutte le impostazioni della qualità percepita dagli utenti (QoE) in cui la proprietà KeepQoEDataForDays è minore di 30. A tale scopo, il comando chiama il cmdlet **Get-CsQoEConfiguration** senza alcun parametro per restituire una raccolta di tutte le impostazioni QoE attualmente in uso nell'organizzazione. La raccolta così ottenuta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà KeepQoEDataForDays è minore di (-lt) 30 giorni. Questa raccolta filtrata viene a sua volta inviata tramite pipe al cmdlet **Remove-CsQoEConfiguration**, che elimina ogni elemento della raccolta.

    Get-CsQoEConfiguration | Where-Object {$_.KeepQoEDataForDays -lt 30} | Remove-CsQoEConfiguration

## Descrizione dettagliata

La metrica QoE consente di tenere traccia delle chiamate audio e video effettuate all'interno dell'organizzazione, inclusi dati quali il numero di pacchetti di rete persi, il rumore di fondo e l'instabilità (differenze nel ritardo dei pacchetti). Questa metrica viene archiviata in un database dedicato, diverso da quello degli altri dati (ad esempio, record dettagli chiamata) e ciò consente di abilitare e disabilitare la qualità percepita dagli utenti (QoE) indipendentemente dalla registrazione degli altri dati. Utilizzare questo cmdlet per rimuovere le impostazioni di configurazione della qualità percepita dagli utenti (QoE) a livello di sito. Se si utilizza questo cmdlet nella configurazione della qualità percepita dagli utenti (QoE) a livello globale, per tutte le proprietà verranno ripristinati i valori predefiniti.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Remove-CsQoEConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsQoEConfiguration"}

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
<td><p>Identificatore univoco delle impostazioni che si desidera rimuovere. I valori possibili sono global e site:&lt;nome sito&gt;, dove &lt;nome sito&gt; è il nome del sito nella distribuzione di Lync Server contenente le impostazioni da rimuovere.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.QoE.QoESettings. Accetta input tramite pipeline da oggetti configurazione QoE.

## Tipi restituiti

Questo cmdlet non restituisce alcun oggetto o valore. Il cmdlet rimuove invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.QoE.QoESettings.

## Vedere anche

#### Ulteriori risorse

[New-CsQoEConfiguration](new-csqoeconfiguration.md)  
[Set-CsQoEConfiguration](set-csqoeconfiguration.md)  
[Get-CsQoEConfiguration](get-csqoeconfiguration.md)

