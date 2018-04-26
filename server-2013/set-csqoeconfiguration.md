---
title: Set-CsQoEConfiguration
TOCTitle: Set-CsQoEConfiguration
ms:assetid: 199f0127-7444-4f88-993a-8e6a33fdcb61
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398245(v=OCS.15)
ms:contentKeyID: 49299831
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsQoEConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta esistente di impostazioni di qualità percepita dagli utenti (QoE, Quality of Experience). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsQoEConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsQoEConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableExternalConsumer <$true | $false>] [-EnablePurging <$true | $false>] [-EnableQoE <$true | $false>] [-ExternalConsumerIssuedCertId <IssuedCertId>] [-ExternalConsumerName <String>] [-ExternalConsumerURL <String>] [-Force <SwitchParameter>] [-KeepQoEDataForDays <UInt32>] [-PurgeHourOfDay <UInt32>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con il comando nell'esempio 1 viene utilizzato il cmdlet **Set-CsQoEConfiguration** per modificare le impostazioni per la qualità percepita dagli utenti per il sito Redmond (-Identity site:Redmond). Le nuove impostazioni disattivano QoE impostando il parametro EnableQoE su False.

    Set-CsQoEConfiguration -Identity site:Redmond -EnableQoE $False

## ESEMPIO 2

Con questo comando vengono modificate le impostazioni QoE applicate al sito Dublin. Con questo esempio il parametro KeepQoEDataForDays viene impostato su 45, quindi i dati QoE saranno eliminati dal database dopo 45 giorni. Inoltre, il parametro PurgeHourOfDay è stato impostato su 4, quindi i dati più vecchi di 45 giorni appena specificati saranno eliminati alle 4.00.

Nota: Se QoE e la registrazione dei dettagli delle chiamate (CDR) sono stati abilitati, per motivi di prestazioni si consiglia di verificare che l'impostazione PurgeHourOfDay sia diversa per QoE e per CDR.

    Set-CsQoEConfiguration -Identity site:Dublin -KeepQoEDataForDays 45 -PurgeHourOfDay 4

## Descrizione dettagliata

Le metriche QoE registrano la qualità delle chiamate audio e video effettuate nell'organizzazione, includendo informazioni quali il numero di pacchetti di rete persi, i rumori di fondo e la quantità di "instabilità" (differenze nel ritardo dei pacchetti). Queste metriche vengono memorizzate in un database a parte quale, ad esempio, registrazione dettagli chiamata (CDR, Call Detail Record), in modo che sia possibile abilitare e disabilitare il servizio QoE indipendentemente dalle altre registrazioni di dati. Utilizzare questo cmdlet per modificare le impostazioni che configurano QoE a livello globale o di sito.

Poiché QoE fa parte del ruolo Monitoring Server, è necessario distribuire il Monitoring Server nell'installazione di Lync Server affinché la registrazione QoE abbia effetto o sia possibile raccogliere i dati QoE.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Set-CsQoEConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsQoEConfiguration"}

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
<td><p><em>EnableExternalConsumer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Consente di specificare se un consumer esterno è in grado di ricevere i report QoE.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePurging</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Consente di specificare se i record saranno eliminati una volta trascorso il tempo definito nella proprietà KeepQoEDataForDays.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableQoE</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Consente di specificare se i record QoE saranno raccolti e salvati nel database di monitoraggio.</p>
<p>Anche se EnableQoE è impostato su True, i dati QoE non saranno raccolti se non è stato distribuito un Monitoring Server successivamente associato a un pool di registrazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExternalConsumerIssuedCertId</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.BaseTypes.IssuedCertId</p></td>
<td><p>L'ID del certificato che consente l'accesso al servizio Web del consumer esterno.</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalConsumerName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome descrittivo del consumer esterno del report QoE.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExternalConsumerURL</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>L'URL del consumer esterno in cui saranno pubblicati i report QoE.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni da modificare. I valori possibili sono global e site:&lt;nome sito&gt;, dove &lt;nome sito&gt; è il nome del sito nella distribuzione di Lync Server a cui si desidera applicare le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>QoESettings</p></td>
<td><p>Riferimento a un oggetto di configurazione QoE. Questo oggetto deve essere di tipo QoESettings e può essere recuperato chiamando il cmdlet <strong>Get-CsQoEConfiguration</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>KeepQoEDataForDays</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Il numero di giorni di conservazione dei dati QoE prima dello svuotamento del database. Questo valore viene ignorato se EnablePurging è impostato su False.</p>
<p>Deve essere un valore compreso tra 1 e 2562.</p></td>
</tr>
<tr class="even">
<td><p><em>PurgeHourOfDay</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>L'ora del giorno in cui saranno eliminati i record QoE che hanno superato il numero di giorni specificato in KeepQoEDataForDays.</p>
<p>Deve essere un valore compreso tra 0 e 23, che rappresenta l'ora del giorno. Ad esempio, 0 corrisponde a mezzanotte, 13 alle 13.00.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.QoE.QoESettings. Consente di accettare l'input da pipeline di oggetti configurazione QoE.

## Tipi restituiti

Il cmdlet **Set-CsQoEConfiguration** non restituisce alcun oggetto o valore. Il cmdlet invece configura le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.QoE.QoESettings.

## Vedere anche

#### Ulteriori risorse

[New-CsQoEConfiguration](new-csqoeconfiguration.md)  
[Remove-CsQoEConfiguration](remove-csqoeconfiguration.md)  
[Get-CsQoEConfiguration](get-csqoeconfiguration.md)

