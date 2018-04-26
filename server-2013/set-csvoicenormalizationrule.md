---
title: Set-CsVoiceNormalizationRule
TOCTitle: Set-CsVoiceNormalizationRule
ms:assetid: 68850abb-4ac7-4ae1-bb6e-d991385f92a4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398491(v=OCS.15)
ms:contentKeyID: 49300845
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceNormalizationRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una regola di normalizzazione vocale. Le regole di normalizzazione vocale sono utilizzate per convertire un requisito di composizione telefonica (ad esempio la composizione di 9 per l'accesso a una linea esterna) nel formato per numeri di telefono E.164 utilizzato da Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsVoiceNormalizationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceNormalizationRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-IsInternalExtension <$true | $false>] [-Pattern <String>] [-Priority <Int32>] [-Translation <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con questo esempio la descrizione della regola Prefix Redmond per il sito Redmond viene impostata su "Add a prefix to all numbers on site Redmond".

    Set-CsVoiceNormalizationRule -Identity "site:Redmond/Prefix Redmond" -Description "Add a prefix to all numbers on site Redmond"

## ESEMPIO 2

Con questo esempio viene modificata la regola di normalizzazione vocale con identità global/SeattleFourDigit. È stata specificata una nuova descrizione per riflettere le modifiche alla regola. Inoltre, è stato specificato un valore di conversione che modifica la regola per convertire qualsiasi numero corrispondente al modello esistente di questa regola nello stesso numero ma con il prefisso +1206556. Ad esempio, se il modello esistente corrispondeva a qualsiasi numero di quattro cifre e veniva immesso il numero 1234, la regola converte tale numero di interno nel numero +12065561234.

    Set-CsVoiceNormalizationRule -Identity global/SeattleFourDigit -Description "Translate an internal four-digit extension" -Translation '+1206556$1'

## ESEMPIO 3

Con l'esempio 3 viene modificato il nome della regola di normalizzazione. La modifica del nome comporta anche la modifica della parte del nome nell'identità. Il cmdlet **Set-CsVoiceNormalizationRule** non dispone di un parametro Name, quindi per cambiare il nome è necessario chiamare innanzitutto il cmdlet **Get-CsVoiceNormalizationRule** per recuperare la regola con identità (Identity) global/RedmondFourDigit e assegnare l'oggetto restituito alla variabile $a. A questo punto è possibile assegnare la stringa RedmondRule alla proprietà Name dell'oggetto. Successivamente si passa la variabile al parametro Instance del cmdlet **Set-CsVoiceNormalizationRule** per rendere definitiva la modifica.

    $a = Get-CsVoiceNormalizationRule -Identity global/RedmondFourDigit
    $a.name = "RedmondRule"
    Set-CsVoiceNormalizationRule -Instance $a

## Descrizione dettagliata

Questo cmdlet modifica una regola di normalizzazione vocale denominata. Queste regole sono una parte obbligatoria dell'autorizzazione telefonica e del routing delle chiamate. Definiscono i requisiti per la conversione dei numeri dal formato Lync Server interno a un formato standard (E.164). È utile conoscere l'utilizzo delle espressioni regolari per definire i formati numerici da convertire.

Le regole modificate utilizzando questo cmdlet sono parte del dial plan e, oltre ad essere accessibili tramite il cmdlet **Get-CsVoiceNormalizationRule**, possono essere recuperate attraverso la proprietà NormalizationRules restituita da una chiamata al cmdlet **Get-CsDialPlan**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Set-CsVoiceNormalizationRule** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceNormalizationRule"}

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
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Una descrizione della regola di normalizzazione.</p>
<p>Lunghezza massima della stringa: 512 caratteri.</p></td>
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
<td><p>Un identificatore univoco per la regola. Il parametro Identity specificato deve includere l'ambito seguito da una barra e quindi dal nome, come in site:Redmond/Rule1, dove site:Redmond è l'ambito e Rule1 è il nome.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>NormalizationRule</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro. Questo oggetto deve essere di tipo NormalizationRule e può essere recuperato chiamando il cmdlet <strong>Get-CsVoiceNormalizationRule</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>IsInternalExtension</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, il risultato dell'applicazione di questa regola è un numero interno all'organizzazione. Se impostato su False, l'applicazione della regola produce un numero esterno. Questo valore viene ignorato se il valore della proprietà OptimizeDeviceDialing del dial plan associato è impostato su False.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>Pattern</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Un'espressione regolare a cui il numero composto deve corrispondere affinché sia applicata questa regola.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>L'ordine di applicazione delle regole. Un numero potrebbe rispondere a più regole. Questo parametro stabilisce l'ordine di test delle regole sul numero.</p></td>
</tr>
<tr class="odd">
<td><p><em>Translation</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il modello di espressione regolare che sarà applicato al numero per convertirlo nel formato E.164.</p>
<p></p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule. Il cmdlet **Set-CsVoiceNormalizationRule** accetta l'input di oggetti regola di normalizzazione vocale inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsVoiceNormalizationRule** non restituisce alcun oggetto o valore. Configura invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule.

## Vedere anche

#### Ulteriori risorse

[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[Remove-CsVoiceNormalizationRule](remove-csvoicenormalizationrule.md)  
[Get-CsVoiceNormalizationRule](get-csvoicenormalizationrule.md)  
[Test-CsVoiceNormalizationRule](test-csvoicenormalizationrule.md)  
[Set-CsDialPlan](set-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)

