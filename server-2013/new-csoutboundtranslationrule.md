---
title: New-CsOutboundTranslationRule
TOCTitle: New-CsOutboundTranslationRule
ms:assetid: aa6011e5-c48d-4fcc-ba65-bdec341234ed
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412803(v=OCS.15)
ms:contentKeyID: 49301612
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsOutboundTranslationRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova regola di conversione in uscita. Una regola di questo tipo converte i numeri di telefono nel formato di composizione locale per agevolare l'interazione con i sistemi PBX (Private Branch Exchange). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsOutboundTranslationRule -Name <String> -Parent <String> <COMMON PARAMETERS>

    New-CsOutboundTranslationRule -Identity <XdsIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Pattern <String>] [-Priority <Int32>] [-Translation <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene creata una regola di conversione in uscita per il sito Redmond denominata Prefix Redmond. Dal momento che non sono specificati altri parametri, la regola viene creata con i valori predefiniti. Il valore passato al parametro -Identity è racchiuso tra virgolette doppie perché il nome della regola (Prefix Redmond) contiene uno spazio. Se il nome della regola non contiene uno spazio non è necessario racchiudere il valore di Identity tra virgolette doppie.

    New-CsOutboundTranslationRule -Identity "site:Redmond/Prefix Redmond"

## ESEMPIO 2

In questo esempio viene creata una nuova regola di conversione in uscita globale denominata SeattleFourDigit. Nota: invece di specificare Parent e Name, è possibile creare la stessa regola specificando -Identity global/SeattleSevenDigit. È stata inclusa una descrizione in cui viene illustrato che questa regola è per la conversione di numeri dal formato E.164 al formato a sette cifre. Sono stati inoltre specificati i valori Pattern e Translation. Tali valori convertono un numero in formato E.164 (in questo caso 12 cifre che iniziano con +1425), specificato dall'espressione regolare in Pattern, in un numero di sette cifre rimuovendo le prime cinque cifre. Ad esempio, il numero +14255551212 verrebbe convertito nel numero 5551212.

    New-CsOutboundTranslationRule -Parent global -Name SeattleSevenDigit -Description "Convert to seven digits" -Pattern '^\+1425(\d{7})$' -Translation '$1'

## Descrizione dettagliata

Chiamare questo cmdlet per creare una nuova regola di conversione in uscita. Lync Server normalizza i numeri di telefono al formato E.164. Numerosi sistemi PBX privati non sono tuttavia in grado di supportare questo formato. Le regole di conversione in uscita convertono il numero nel formato di composizione locale prima di inviarlo al Mediation Server o al gateway.

Ogni regola di conversione in uscita è associata a una configurazione di trunk. A ogni configurazione può essere associata più di una regola di conversione in uscita. Pertanto, l'identità (Identity) per ogni regola è costituita da un ambito con un nome univoco per tale ambito nel formato ambito/nome, ad esempio site:Redmond/OBR1. La regola viene associata automaticamente alla configurazione di trunk con lo stesso ambito. Se si chiama il cmdlet **New-CsOutboundTranslationRule** e si specifica un ambito in cui non è stata ancora definita una configurazione di trunk, verrà creata la configurazione di trunk con l'ambito specificato, la regola di conversione in uscita e i valori predefiniti.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsOutboundTranslationRule** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsOutboundTranslationRule"}

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
<td><p>Identificatore univoco per la regola di conversione in uscita. Il parametro Identity include l'ambito in cui viene applicata la regola e il nome della regola e deve essere incluso nell'ambito globale, del sito o del servizio (solo PSTNGateway), ad esempio site:Redmond/OutboundRule1 e PstnGateway:Redmond.litwareinc.com/OutboundRule2.</p>
<p>Se il parametro Identity è specificato, non è possibile specificare valori per i parametri Name o Parent.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome della regola di conversione in uscita. Se non viene fornito alcun nome, è necessario specificare un'identità formata da un ambito e nome. Se viene fornito un nome, è richiesto anche il parametro Parent ma non è possibile specificare un'identità.</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Ambito della regola di conversione in uscita. Se viene specificato un valore per questo parametro è necessario specificare anche un valore per il parametro Name. Non è tuttavia possibile specificare il parametro Identity. Se non vengono specificati i parametri Parent e Name, è necessario specificare il parametro Identity.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Descrizione della regola di conversione in uscita. Questa descrizione consente di identificare lo scopo della regola.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>Pattern</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Espressione regolare che rappresenta il formato del numero a cui la conversione verrà applicata.</p>
<p>Valore predefinito: ^\+(\d*)$</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Se un numero corrisponde al formato di più regole di conversione in uscita, le regole vengono applicate in ordine di priorità. Utilizzare questo parametro per assegnare una priorità alla regola.</p></td>
</tr>
<tr class="even">
<td><p><em>Translation</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Espressione regolare che verrà applicata al numero corrispondente al formato per preparare tale numero per il routing in uscita.</p>
<p>Valore predefinito: $1</p></td>
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

Questo cmdlet consente di creare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule.

## Vedere anche

#### Ulteriori risorse

[Remove-CsOutboundTranslationRule](remove-csoutboundtranslationrule.md)  
[Set-CsOutboundTranslationRule](set-csoutboundtranslationrule.md)  
[Get-CsOutboundTranslationRule](get-csoutboundtranslationrule.md)

