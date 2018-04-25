---
title: Set-CsOutboundTranslationRule
TOCTitle: Set-CsOutboundTranslationRule
ms:assetid: fbf82146-7884-418c-8239-66c0ca0f2ba6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413073(v=OCS.15)
ms:contentKeyID: 49302567
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsOutboundTranslationRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una regola di conversione in uscita esistente. Una regola di conversione in uscita converte i numeri di telefono nel formato di composizione locale per agevolare l'interazione con i sistemi PBX (Private Branch Exchange). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsOutboundTranslationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsOutboundTranslationRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-Pattern <String>] [-Priority <Int32>] [-Translation <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene modificata la regola di conversione in uscita globale con l'identità site:Redmond/Prefix Redmond. È stata inclusa una descrizione che spiega che questa regola è destinata alla conversione dei numeri dal formato E.164 al formato di un numero telefonico di sette cifre. Sono stati inoltre specificati i valori Pattern e Translation, che modificheranno i valori esistenti per queste proprietà. Tali valori convertono un numero in formato E.164 (in questo caso 12 cifre che iniziano con +1425), specificato dall'espressione regolare in Pattern, in un numero di sette cifre rimuovendo le prime cinque cifre. Ad esempio, il numero +14255551212 verrebbe convertito nel numero 5551212.

    Set-CsOutboundTranslationRule -Identity "site:Redmond/Prefix Redmond" -Description "Convert to seven digits" -Pattern '^\+1425(\d{7})$' -Translation '$1'

## ESEMPIO 2

In questo esempio viene modificata la proprietà Name di una regola di conversione in uscita. In questo modo si modifica l'identità della regola. Il primo comando in questo esempio è una chiamata al cmdlet **Get-CsOutboundTranslationRule**. Viene specificata l'identità site:Redmond\\OBR1, che restituirà una regola di conversione, ovvero quella con l'identità fornita. Anziché visualizzare questa regola, viene assegnata alla variabile $a. Nella riga 2 di questo esempio viene assegnata la stringa "Outbound Rule 1" alla proprietà Name della variabile $a, ovvero la variabile contenente un riferimento alla regola site:Redmond/OBR1. Nell'ultima riga di questo esempio viene chiamato il cmdlet **Set-CsOutboundTranslationRule**, specificando il parametro Instance e passandolo alla variabile $a. Se a questo punto si chiama il cmdlet **Get-CsOutboundTranslationRule** con un valore di identità site:Redmond/OBR1, non verrà restituito alcun valore, poiché la regola con tale identità non esiste più. È stata infatti sostituita dalla stessa regola ma con identità site:Redmond/Outbound Rule 1.

    $a = Get-CsOutboundTranslationRule -Identity "site:Redmond/OBR1"
    $a.Name = "Outbound Rule 1"
    Set-CsOutboundTranslationRule -Instance $a

## Descrizione dettagliata

In Lync Server i numeri di telefono vengono normalizzati nel formato E.164. Numerosi sistemi PBX privati non sono tuttavia in grado di supportare questo formato. Pertanto le regole di conversione in uscita consentono di convertire il numero nel formato di composizione locale prima dell'invio del numero a Mediation Server o al gateway. Chiamare questo cmdlet per modificare una regola di conversione in uscita esistente.

Ogni regola di conversione in uscita è associata a una configurazione del trunk. Pertanto, se si utilizza questo cmdlet per modificare una regola, si inciderà sulla configurazione del trunk corrispondente. A ogni configurazione può essere associata più di una regola di conversione in uscita. Pertanto, l'identità per ogni regola è costituita da un ambito con un nome univoco per tale ambito nel formato ambito/nome, ad esempio site:Redmond/OBR1. La regola viene associata automaticamente alla configurazione del trunk con lo stesso ambito. Per modificare le regole di conversione in uscita in una configurazione del trunk, è consigliabile chiamare il cmdlet **Set-CsOutboundTranslationRule**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsOutboundTranslationRule** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsOutboundTranslationRule"}

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
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Descrizione della regola di conversione in uscita. Questa descrizione può essere utilizzata per aiutare gli amministratori a identificare con facilità lo scopo della regola.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Identificatore univoco della regola di conversione in uscita da modificare. L'identità è costituita dall'ambito seguito da un nome univoco per ogni ambito. Ad esempio, site:Redmond/OutboundRule1.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>TranslationRule</p></td>
<td><p>Un riferimento oggetto a una regola di conversione in uscita. Tale oggetto deve essere di tipo Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule, che può essere recuperato chiamando il cmdlet <strong>Get-CsOutboundTranslationRule</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Pattern</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Espressione regolare che rappresenta il formato del numero a cui la conversione verrà applicata.</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Int32</p></td>
<td><p>Se un numero corrisponde al formato di più regole di conversione in uscita, le regole vengono applicate in ordine di priorità. Utilizzare questo parametro per assegnare una priorità alla regola.</p></td>
</tr>
<tr class="even">
<td><p><em>Translation</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Espressione regolare che verrà applicata al numero corrispondente al formato per preparare tale numero per il routing in uscita.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule. Accetta l'invio tramite pipe di oggetti regole di conversione in uscita.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Modifica un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule.

## Vedere anche

#### Ulteriori risorse

[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)  
[Remove-CsOutboundTranslationRule](remove-csoutboundtranslationrule.md)  
[Get-CsOutboundTranslationRule](get-csoutboundtranslationrule.md)

