---
title: Remove-CsImFilterConfiguration
TOCTitle: Remove-CsImFilterConfiguration
ms:assetid: 0c6f5f69-ae41-46d6-b817-fa1c6751c615
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398171(v=OCS.15)
ms:contentKeyID: 49299655
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsImFilterConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove la configurazione del filtro di messaggistica istantanea specificata. Le impostazioni del filtro di messaggistica istantanea vengono utilizzate per impedire agli utenti di inviare messaggi istantanei contenenti collegamenti ipertestuali. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsImFilterConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene utilizzato il cmdlet **Remove-CsImFilterConfiguration** per rimuovere la configurazione del filtro IM con Identity site:Redmond. Quando da un sito viene rimossa una configurazione del filtro IM, per quel sito verranno automaticamente utilizzate le impostazioni globali.

    Remove-CsImFilterConfiguration -Identity site:Redmond

## ESEMPIO 2

Nell'esempio 2 vengono rimosse tutte le configurazioni del filtro IM nell'ambito del sito. A tale scopo, il comando innanzitutto utilizza il cmdlet **Get-CsImFilterConfiguration** e il parametro Filter per restituire tutte le configurazioni nell'ambito del sito. La stringa con caratteri jolly site:\* indica al cmdlet **Get-CsImFilterConfiguration** di restituire solo le configurazioni la cui identità inizia con il valore stringa site:. La raccolta di configurazioni filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsImFilterConfiguration**, che elimina ogni configurazione inclusa nella raccolta.

    Get-CsImFilterConfiguration -Filter site:* | Remove-CsImFilterConfiguration

## Descrizione dettagliata

Quando si inviano messaggi istantanei, gli utenti possono incorporare nel testo del messaggio un URI (Uniform Resource Identifier) per rimandare a una condivisione o a un sito Web specifico gli altri partecipanti alla conversazione. È possibile configurare Lync Server in modo che i collegamenti ipertestuali con determinati prefissi vengano bloccati o non risultino attivi. In altri termini, i partecipanti non possono semplicemente fare clic sul collegamento per accedere al sito a cui fa riferimento l'URI, ma devono copiare e incollare manualmente il collegamento in un browser.

Il cmdlet **Remove-CsImFilterConfiguration** consente di rimuovere le impostazioni del filtro IM per una determinata identità, ad esempio, un sito specifico. L'utilizzo di questo cmdlet per l'identità Global consente di ripristinare le impostazioni predefinite nella configurazione globale.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Remove-CsImFilterConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsImFilterConfiguration"}

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
<td><p>L'identità univoca della configurazione da rimuovere. Per questo cmdlet Identity sarà Global o Site:&lt;nome sito&gt;, in cui &lt;nome sito&gt; indica il nome del sito a cui sono applicate le impostazioni.</p>
<p>Tipo di dati completi: Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration. Accetta l'input tramite pipeline degli oggetti configurazione filtro IM.

## Tipi restituiti

Consente di rimuovere un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsImFilterConfiguration](new-csimfilterconfiguration.md)  
[Set-CsImFilterConfiguration](set-csimfilterconfiguration.md)  
[Get-CsImFilterConfiguration](get-csimfilterconfiguration.md)

