---
title: New-CsVoiceNormalizationRule
TOCTitle: New-CsVoiceNormalizationRule
ms:assetid: 189809ff-559e-476a-a32c-8b3812371883
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398240(v=OCS.15)
ms:contentKeyID: 49299820
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoiceNormalizationRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova regola di normalizzazione vocale. Le regole di normalizzazione vocale sono utilizzate per convertire un requisito di composizione telefonica (ad esempio la composizione di 9 per l'accesso a una linea esterna) nel formato per numeri di telefono E.164 utilizzato da Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsVoiceNormalizationRule -Name <String> -Parent <String> <COMMON PARAMETERS>

    New-CsVoiceNormalizationRule -Identity <XdsIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-IsInternalExtension <$true | $false>] [-Pattern <String>] [-Priority <Int32>] [-Translation <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con questo esempio viene creata una nuova regola di normalizzazione per il sito Redmond denominato Prefix Redmond. Dal momento che non sono specificati altri parametri, la regola viene creata con i valori predefiniti. Il valore passato al parametro Identity è racchiuso tra virgolette doppie perché il nome della regola (Prefix Redmond) contiene uno spazio. Se il nome della regola non contiene uno spazio non è necessario racchiudere il valore di Identity tra virgolette doppie.

È opportuno tenere presente che un dial plan del sito Redmond deve essere presente affinché il comando venga eseguito correttamente. È possibile creare un nuovo dial plan chiamando il cmdlet **New-CsDialPlan**.

    New-CsVoiceNormalizationRule -Identity "site:Redmond/Prefix Redmond"

## ESEMPIO 2

Con questo esempio viene creata una nuova regola di normalizzazione vocale denominata SeattleFourDigit che può essere applicata al dial plan per utente con Identity SeattleUser. Nota: invece di specificare Parent e Name, è possibile creare la stessa regola specificando -Identity SeattleUser/SeattleFourDigit. È stata inclusa una descrizione che spiega come questa regola converte i numeri composti internamente utilizzando solamente un interno di 4 cifre. Sono stati inoltre specificati i valori Pattern e Translation. Questi valori consentono di convertire un numero di quattro cifre (specificato dall'espressione regolare in Pattern) nello stesso numero di quattro cifre preceduto dal valore di Translation (+1206555). Ad esempio, se è stato immesso il numero di interno 1234, la regola lo converte nel numero +12065551234.

Si noti l'utilizzo delle virgolette singole che racchiudono i valori Pattern e Translation. Per questi valori sono richieste le virgolette singole. In questo caso non è possibile utilizzare virgolette doppie né omettere le virgolette.

Come illustrato nell'esempio 1, è richiesto un dial plan con l'ambito specificato. In questo caso deve essere presente un dial plan con Identity SeattleUser.

    New-CsVoiceNormalizationRule -Parent SeattleUser -Name SeattleFourDigit -Description "Dialing with internal four-digit extension" -Pattern '^(\d{4})$' -Translation '+1206555$1'

## Descrizione dettagliata

Questo cmdlet crea una regola di normalizzazione vocale denominata. Queste regole sono una parte obbligatoria dell'autorizzazione telefonica e del routing delle chiamate. Definiscono i requisiti per la conversione dei numeri dal formato Lync Server interno a un formato standard (E.164). È utile conoscere l'utilizzo delle espressioni regolari per definire i formati numerici da convertire.

Le regole create utilizzando questo cmdlet sono parte del dial plan e, oltre ad essere accessibili tramite il cmdlet **Get-CsVoiceNormalizationRule**, possono essere recuperate attraverso la proprietà NormalizationRules restituita da una chiamata al cmdlet **Get-CsDialPlan**. Non è possibile creare una regola di normalizzazione, se non è già presente un dial plan con un valore Identity corrispondente all'ambito specificato nella Identity della regola di normalizzazione stessa. Ad esempio, non è possibile creare una regola di normalizzazione con Identity site:Redmond/RedmondNormalizationRule a meno che non sia presente un dial plan per site:Redmond.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **New-CsVoiceNormalizationRule** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoiceNormalizationRule"}

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
<td><p>Un identificatore univoco per la regola. Il parametro Identity specificato deve includere l'ambito seguito da una barra e dal nome, come in site:Redmond/Rule1, dove site:Redmond è l'ambito e Rule1 è il nome. La parte del nome viene archiviata automaticamente nella proprietà Name. Non è consentito specificare valori per Identity e Name nello stesso comando.</p>
<p>Le regole di normalizzazione vocale possono essere create negli ambiti riportati di seguito: Global, Site, Service (solo Registrar e PSTNGateway) e Per User. Prima di creare una nuova regola è necessario che sia già presente un dial plan con Identity corrispondente all'ambito della regola di normalizzazione. Per recuperare un elenco di dial plan, chiamare il cmdlet <strong>Get-CsDialPlan</strong>.</p>
<p>Il parametro Identity è obbligatorio, tranne nel caso in cui sia specificato il parametro Parent. Non è possibile includere il parametro Identity e il parametro Parent nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome della regola. Questo parametro è obbligatorio se è stato specificato un valore per il parametro Parent. Se non è stato specificato un valore per il parametro Parent, il nome corrisponde per impostazione predefinita a quello specificato nel parametro Identity. Ad esempio, se viene creata una regola con site:Redmond/RedmondRule, Name corrisponde per impostazione predefinita a RedmondRule. Non è possibile utilizzare il parametro Name e il parametro Identity nello stesso comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Ambito in cui sarà creata la nuova regola di normalizzazione. Questo valore deve corrispondere a Global, a site:&lt;nomesito&gt;, dove &lt;nomesito&gt; è il nome del sito Lync Server, al gateway PSTN o al servizio di registrazione, ad esempio PSTNGateway:redmond.litwareinc.com, oppure a una stringa che designa una regola per utente. È necessario che sia già presente un dial plan con l'ambito specificato. In caso contrario, il comando avrà esito negativo.</p>
<p>Il parametro Parent è obbligatorio, tranne nel caso in cui sia specificato il parametro Identity. Non è possibile includere il parametro Identity e il parametro Parent nello stesso comando. Se si include il parametro Parent è obbligatorio specificare il parametro Name.</p></td>
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
<td><p>Una descrizione della regola di normalizzazione.</p>
<p>Lunghezza massima della stringa: 512 caratteri.</p></td>
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
<td><p><em>IsInternalExtension</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, il risultato dell'applicazione di questa regola è un numero interno all'organizzazione. Se impostato su False, l'applicazione della regola produce un numero esterno. Questo valore viene ignorato se il valore della proprietà OptimizeDeviceDialing del dial plan associato è impostato su False.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="odd">
<td><p><em>Pattern</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Un'espressione regolare a cui il numero composto deve corrispondere affinché sia applicata questa regola.</p>
<p>Valore predefinito: ^(\d{11})$ (il valore predefinito rappresenta qualsiasi set di numeri, fino a 11 cifre).</p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>L'ordine di applicazione delle regole. Un numero di telefono potrebbe rispondere a più regole. Questo parametro stabilisce l'ordine di test delle regole sul numero.</p></td>
</tr>
<tr class="odd">
<td><p><em>Translation</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il modello di espressione regolare che sarà applicato al numero per convertirlo nel formato E.164.</p>
<p>Valore predefinito: +$1 (il valore predefinito impone un segno più [+] come prefisso del numero).</p></td>
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

Nessuno.

## Tipi restituiti

Questo cmdlet consente di creare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule.

## Vedere anche

#### Ulteriori risorse

[Remove-CsVoiceNormalizationRule](remove-csvoicenormalizationrule.md)  
[Set-CsVoiceNormalizationRule](set-csvoicenormalizationrule.md)  
[Get-CsVoiceNormalizationRule](get-csvoicenormalizationrule.md)  
[Test-CsVoiceNormalizationRule](test-csvoicenormalizationrule.md)  
[New-CsDialPlan](new-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)

