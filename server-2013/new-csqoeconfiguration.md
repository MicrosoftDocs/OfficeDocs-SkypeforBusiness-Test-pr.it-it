---
title: New-CsQoEConfiguration
TOCTitle: New-CsQoEConfiguration
ms:assetid: 4fc607d5-1a85-4de5-9d18-39d0425c82dc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398325(v=OCS.15)
ms:contentKeyID: 49300553
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsQoEConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni di qualità percepita dagli utenti (QoE, Quality of Experience). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsQoEConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableExternalConsumer <$true | $false>] [-EnablePurging <$true | $false>] [-EnableQoE <$true | $false>] [-ExternalConsumerIssuedCertId <IssuedCertId>] [-ExternalConsumerName <String>] [-ExternalConsumerURL <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-KeepQoEDataForDays <UInt32>] [-PurgeHourOfDay <UInt32>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando nell'Esempio 1 utilizza il cmdlet **New-CsQoEConfiguration** per creare un nuovo gruppo di impostazioni della qualità percepita dagli utenti (QoE) con Identity site:Redmond. Oltre a Identity site:Redmond le nuove impostazioni hanno anche la proprietà EnableQoE impostata su False. Dal momento che le impostazioni del sito hanno la precedenza sulle impostazioni globali, QoE sarà disabilitato per il sito Redmond, indipendentemente dal fatto che QoE sia stata abilitato o meno nell'ambito globale.

    New-CsQoEConfiguration -Identity site:Redmond -EnableQoE $False

## ESEMPIO 2

Questo comando consente di creare nuove impostazioni QoE che si applicano al sito Dublin. In questo esempio il parametro KeepQoEDataForDays è stato impostato su 30, in modo tale che i dati QoE verranno eliminati ogni 30 giorni piuttosto che ogni 60 giorni (valore predefinito). Inoltre, è stato impostato il parametro PurgeHourOfDay su 4. Ciò significa che tutti i dati creati più di 30 giorni prima verranno eliminati alle quattro di mattina.

Nota se sono stati abilitati QoE e la registrazione dettagli chiamata (CDR), per ragioni legate alle prestazioni è buona norma assicurarsi che l'impostazione PurgeHourOfDay di QoE sia diversa da quella di CDR.

    New-CsQoEConfiguration -Identity site:Dublin -KeepQoEDataForDays 30 -PurgeHourOfDay 4

## Descrizione dettagliata

La metrica QoE consente di tenere traccia delle chiamate audio e video effettuate all'interno dell'organizzazione, inclusi dati quali il numero di pacchetti di rete persi, il rumore di fondo e l'instabilità (differenze nel ritardo dei pacchetti). Questa metrica viene archiviata in un database dedicato, diverso da quello degli altri dati (ad esempio, record dettagli chiamata) e ciò consente di abilitare e disabilitare la qualità percepita dagli utenti (QoE) indipendentemente dalla registrazione degli altri dati. Utilizzare questo cmdlet per creare le impostazioni di configurazione della qualità percepita dagli utenti (QoE) a livello di sito. Le impostazioni a livello globale sono presenti per impostazione predefinita e non possono essere rimosse.

Poiché QoE fa parte del ruolo Monitoring Server, è necessario distribuire il Monitoring Server nell'installazione di Lync Server affinché la registrazione QoE abbia effetto o sia possibile raccogliere i dati QoE.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsQoEConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsQoEConfiguration"}

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
<td><p>Sito a cui vengono applicate le nuove impostazioni. Il formato deve essere site:&lt;nome sito&gt;, dove &lt;nome sito&gt; indica il nome del sito nella distribuzione di Lync Server.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableExternalConsumer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se un consumatore esterno è in grado di ricevere rapporti QoE.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePurging</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se i record verranno cancellati dopo la scadenza del valore definito nella proprietà KeepQoEDataForDays.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableQoE</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se i record QoE verranno raccolti e salvati nel database di monitoraggio.</p>
<p>Si noti che anche se EnableQoE è impostato su True, i dati QoE non verranno raccolti a meno che non sia stato distribuito un Monitoring Server e associato ad un pool di registrazione.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalConsumerIssuedCertId</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.BaseTypes.IssuedCertId</p></td>
<td><p>L'ID del certificato che consente l'accesso al servizio Web dei consumatori esterni.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExternalConsumerName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome descrittivo del consumatore esterno del report QoE.</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalConsumerURL</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>L'URL del consumatore esterno a cui verranno inviati i rapporti QoE.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>KeepQoEDataForDays</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Il numero di giorni in cui i dati QoE verranno archiviati prima di essere eliminati dal database. Questo valore viene ignorato se EnablePurging è impostato su False.</p>
<p>Deve essere un valore compreso tra 1 e 2562.</p>
<p>Valore predefinito: 60</p></td>
</tr>
<tr class="even">
<td><p><em>PurgeHourOfDay</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>L'ora in cui verranno eliminati i record QoE che hanno superato il valore relativo al numero di giorni specificato nella proprietà KeepQoEDataForDays.</p>
<p>Deve essere un valore compreso tra 0 e 23. Ad esempio, 0 indica la mezzanotte e 14 indica le due del pomeriggio. Valore predefinito: 1</p></td>
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

Nessuno.

## Tipi restituiti

Consente di creare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.QoE.QoESettings.

## Vedere anche

#### Ulteriori risorse

[Remove-CsQoEConfiguration](remove-csqoeconfiguration.md)  
[Set-CsQoEConfiguration](set-csqoeconfiguration.md)  
[Get-CsQoEConfiguration](get-csqoeconfiguration.md)

