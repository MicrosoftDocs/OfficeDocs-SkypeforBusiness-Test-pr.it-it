---
title: Set-CsBandwidthPolicyServiceConfiguration
TOCTitle: Set-CsBandwidthPolicyServiceConfiguration
ms:assetid: b39af1ca-465d-4598-96a3-e19283ddf731
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412863(v=OCS.15)
ms:contentKeyID: 49301714
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsBandwidthPolicyServiceConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una configurazione del servizio dei criteri di larghezza di banda esistente. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsBandwidthPolicyServiceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsBandwidthPolicyServiceConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableLogging <$true | $false>] [-Force <SwitchParameter>] [-LogCleanUpInterval <TimeSpan>] [-MaxLogFileSizeMb <UInt32>] [-MaxTokenLifetime <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

L'esempio mostra la modifica della configurazione del servizio dei criteri di larghezza di banda per il sito Redmond (-Identity site:Redmond). La configurazione viene modificata per abilitare la registrazione e per cambiare la durata massima di un token a tre ore e il numero di giorni prima della pulizia del log a cinque giorni. Tutte queste operazioni vengono eseguite con un solo comando. Per attivare la registrazione, il parametro EnableLogging è impostato su True ($true). Il parametro MaxTokenLifetime riceve successivamente un valore corrispondente a 3:00:00, che rappresenta tre ore. Il parametro LogCleanUpInterval riceve infine un valore 5.00:00:00, che indica cinque giorni.

    Set-CsBandwidthPolicyServiceConfiguration -Identity site:Redmond -EnableLogging $true -MaxTokenLifetime 3:00:00 -LogCleanUpInterval 5.00:00:00

## Descrizione dettagliata

La funzionalità Controllo di ammissione di chiamata consente di determinare se consentire sessioni di comunicazione in tempo reale, ad esempio chiamate audio o video, in base ai vincoli di larghezza di banda. Nell'implementazione Lync Server di Controllo di ammissione di chiamata le aree, i siti e le subnet vengono definiti in una rete insieme alle relazioni e ai collegamenti tra tali entità in modo da stabilire i relativi vincoli di larghezza di banda. Il servizio dei criteri di larghezza di banda è il componente che esegue la funzionalità Controllo di ammissione di chiamata nella distribuzione di Lync Server, consentendo di decidere se la larghezza di banda esistente è sufficiente per una chiamata da effettuare. Questo cmdlet modifica una configurazione del servizio dei criteri di larghezza di banda esistente.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsBandwidthPolicyServiceConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsBandwidthPolicyServiceConfiguration"}

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
<td><p><em>EnableLogging</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Impostare questo parametro su True per generare log di stato dell'errore e del collegamento CAC relativi al servizio dei criteri di larghezza di banda.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>L'identificatore univoco della configurazione che si desidera cambiare. Questo identificatore includerà l'ambito (per la configurazione globale) o l'ambito e il nome (per una configurazione a livello del sito, ad esempio site:Redmond).</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>BandwidthPolicyServiceConfiguration</p></td>
<td><p>Il riferimento a un oggetto di configurazione del servizio dei criteri di larghezza di banda. L'oggetto deve essere di tipo BandwidthPolicyServiceConfiguration, che può essere recuperato chiamando il cmdlet <strong>Get-CsBandwidthPolicyServiceConfiguration</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>LogCleanUpInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Il periodo di tempo dopo il quale i log di stato dell'errore e del collegamento CAC saranno rimossi.</p>
<p>Il valore deve essere compreso nell'intervallo da 1 giorno a 60 giorni. Il valore deve essere immesso nel formato gg.hh:mm:ss, in cui &quot;g&quot; è il giorno, &quot;h&quot; sono le ore, &quot;m&quot; i minuti e &quot;s&quot; i secondi. Ad esempio, il valore per 20 giorni è 20.00:00:00.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxLogFileSizeMb</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>La dimensione massima consentita per il file di log. Il valore di questo parametro deve essere un numero positivo che specifica la dimensione del file in megabyte. Ad esempio, per consentire al file di log di raggiungere una dimensione massima di 10 megabyte, immettere il valore 10.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxTokenLifetime</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Il tempo massimo di esistenza del token emesso dal servizio di autenticazione dei criteri della larghezza di banda.</p>
<p>Il valore deve essere compreso nell'intervallo da 1 ora a 24 ore. Il valore deve essere immesso nel formato gg.hh:mm:ss, in cui &quot;g&quot; è il giorno, &quot;h&quot; sono le ore, &quot;m&quot; i minuti e &quot;s&quot; i secondi. Ad esempio, il valore per 12 ore è 12:00:00.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.BandwidthPolicyServiceConfiguration.BandwidthPolicyServiceConfiguration. Accetta l'input da pipeline di oggetti configurazione del servizio dei criteri di larghezza di banda.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Consente di modificare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.BandwidthPolicyServiceConfiguration.BandwidthPolicyServiceConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsBandwidthPolicyServiceConfiguration](new-csbandwidthpolicyserviceconfiguration.md)  
[Remove-CsBandwidthPolicyServiceConfiguration](remove-csbandwidthpolicyserviceconfiguration.md)  
[Get-CsBandwidthPolicyServiceConfiguration](get-csbandwidthpolicyserviceconfiguration.md)

