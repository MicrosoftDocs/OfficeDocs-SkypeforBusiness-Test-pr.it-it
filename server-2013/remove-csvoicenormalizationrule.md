---
title: Remove-CsVoiceNormalizationRule
TOCTitle: Remove-CsVoiceNormalizationRule
ms:assetid: 6a1bf26c-d95b-4a03-8d2d-c17159dcb9be
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398501(v=OCS.15)
ms:contentKeyID: 49300867
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsVoiceNormalizationRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una regola di normalizzazione vocale. Le regole di normalizzazione vocale sono utilizzate per convertire requisiti di composizione telefonica (ad esempio la composizione di 9 per l'accesso a una linea esterna) nel formato per numeri di telefono E.164 utilizzato da Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsVoiceNormalizationRule -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene rimossa la regola di normalizzazione vocale con Identity site:Redmond/SeattleRule1.

    Remove-CsVoiceNormalizationRule -Identity site:Redmond/SeattleRule1

## ESEMPIO 2

In questo esempio vengono rimosse tutte le regole di normalizzazione vocali dal sito Redmond.

    Remove-CsVoiceNormalizationRule -Identity site:Redmond

## Descrizione dettagliata

Questo cmdlet consente di rimuovere una regola di normalizzazione vocale denominata. Queste regole sono una parte obbligatoria dell'autorizzazione telefonica e del routing delle chiamate. Definiscono i requisiti per la conversione dei numeri dal formato Lync Server interno a un formato standard (E.164). È utile conoscere l'utilizzo delle espressioni regolari per definire i formati numerici da convertire.

Le regole rimosse utilizzando questo cmdlet verranno eliminate dai dial plan dell'organizzazione, pertanto non verranno restituite dal cmdlet **Get-CsVoiceNormalizationRule** e non saranno visibili nella proprietà NormalizationRules restituita da una chiamata al cmdlet **Get-CsDialPlan**. Ciò significa che se si chiama il cmdlet **Remove-CsVoiceNormalizationRule**, il dial plan potrebbe non contenere più alcuna regola di normalizzazione.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Remove-CsVoiceNormalizationRule** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsVoiceNormalizationRule"}

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
<td><p>L'identità univoca della regola da rimuovere. Se l'identità specificata include l'ambito seguito da una barra e quindi dal nome (ad esempio, site:Redmond/Rule1, in cui site:Redmond è l'ambito e Rule1 è il nome), verrà rimossa la regola con tale identità univoca. Se il valore specificato per Identity contiene solo l'ambito (site:Redmond), verranno rimosse tutte le regole di normalizzazione nell'ambito.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule. Accetta input tramite pipeline da oggetti regola di normalizzazione.

## Tipi restituiti

Questo cmdlet consente di eliminare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule.

## Vedere anche

#### Ulteriori risorse

[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[Set-CsVoiceNormalizationRule](set-csvoicenormalizationrule.md)  
[Get-CsVoiceNormalizationRule](get-csvoicenormalizationrule.md)  
[Test-CsVoiceNormalizationRule](test-csvoicenormalizationrule.md)  
[Remove-CsDialPlan](remove-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)

