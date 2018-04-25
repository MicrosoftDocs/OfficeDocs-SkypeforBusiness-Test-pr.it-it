---
title: Remove-CsBandwidthPolicyServiceConfiguration
TOCTitle: Remove-CsBandwidthPolicyServiceConfiguration
ms:assetid: cf920168-3f65-4747-86cd-d3e287c84349
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398877(v=OCS.15)
ms:contentKeyID: 49302028
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsBandwidthPolicyServiceConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una configurazione del servizio dei criteri di larghezza di banda esistente. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsBandwidthPolicyServiceConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene rimossa la configurazione del servizio criteri di larghezza di banda definita per il sito di Redmond (-Identity site:Redmond).

    Remove-CsBandwidthPolicyServiceConfiguration -Identity site:Redmond

## ESEMPIO 2

Nell'esempio vengono rimosse tutte le configurazioni del servizio criteri di larghezza di banda in cui la registrazione è disabilitata. A tale scopo, l'esempio inizia con una chiamata del cmdlet **Get-CsBandwidthPolicyServiceConfiguration** che restituirà una raccolta di tutte le configurazioni del servizio criteri di larghezza di banda nella distribuzione di Lync Server. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che circoscrive la raccolta alle configurazioni con proprietà EnableLogging uguale a (-eq) False ($False), ottenendo quindi una raccolta di configurazioni con la registrazione disabilitata. La raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsBandwidthPolicyServiceConfiguration**, che rimuove tutti gli elementi presenti nella raccolta.

    Get-CsBandwidthPolicyServiceConfiguration | Where-Object {$_.EnableLogging -eq $False} | Remove-CsBandwidthPolicyServiceConfiguration

## Descrizione dettagliata

La funzionalità Controllo di ammissione di chiamata consente di determinare se autorizzare sessioni di comunicazioni in tempo reale, ad esempio chiamate audio o video, in base ai vincoli di larghezza di banda. Nell'ambito dell'implementazione di Controllo di ammissione di chiamata in Lync Server vengono definiti le aree, i siti e le subnet di una rete insieme alle relazioni e ai collegamenti tra tali entità in modo da imporre vincoli di larghezza di banda. Il servizio criteri di larghezza di banda è il componente che esegue la funzionalità Controllo di ammissione di chiamata nella distribuzione di Lync Server, consentendo di decidere se la larghezza di banda esistente è sufficiente per una chiamata da effettuare. Questo cmdlet rimuove la configurazione di un servizio criteri di larghezza di banda definito a livello di sito. È inoltre possibile utilizzare il cmdlet per rimuovere il servizio criteri di larghezza di banda globale, sebbene in questo caso il servizio globale non venga effettivamente rimosso ma vengono semplicemente reimpostati i valori predefiniti.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsBandwidthPolicyServiceConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsBandwidthPolicyServiceConfiguration"}

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
<td><p>Identificatore univoco della configurazione che si desidera rimuovere. Questo identificatore includerà l'ambito (per la configurazione globale) o l'ambito e il nome (per una configurazione a livello del sito, ad esempio site:Redmond).</p></td>
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
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.BandwidthPolicyServiceConfiguration.BandwidthPolicyServiceConfiguration. Accetta l'input da pipeline di oggetti configurazione del servizio criteri di larghezza di banda.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Consente di rimuovere un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.BandwidthPolicyServiceConfiguration.BandwidthPolicyServiceConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsBandwidthPolicyServiceConfiguration](new-csbandwidthpolicyserviceconfiguration.md)  
[Set-CsBandwidthPolicyServiceConfiguration](set-csbandwidthpolicyserviceconfiguration.md)  
[Get-CsBandwidthPolicyServiceConfiguration](get-csbandwidthpolicyserviceconfiguration.md)

