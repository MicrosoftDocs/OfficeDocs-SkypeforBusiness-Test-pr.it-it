---
title: Set-CsDialPlan
TOCTitle: Set-CsDialPlan
ms:assetid: 80277dc6-8853-4cbd-87cb-e64f9e135d5f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398644(v=OCS.15)
ms:contentKeyID: 49301133
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsDialPlan

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un dial plan esistente.Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsDialPlan [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsDialPlan [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-City <String>] [-Confirm [<SwitchParameter>]] [-CountryCode <String>] [-Description <String>] [-DialinConferencingRegion <String>] [-ExternalAccessPrefix <String>] [-Force <SwitchParameter>] [-NormalizationRules <PSListModifier>] [-OptimizeDeviceDialing <$true | $false>] [-SimpleName <String>] [-State <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene utilizzato il cmdlet **Set-CsDialPlan** per modificare il dial plan con identità (Identity) RedmondDialPlan. In questo caso l'unica proprietà modificata è Description. Per eseguire questa modifica viene specificato il parametro Description seguito dal testo della nuova descrizione.

    Set-CsDialPlan -Identity RedmondDialPlan -Description "This plan is for Redmond-based users only."

## ESEMPIO 2

In questo esempio viene utilizzato il cmdlet **Set-CsDialPlan** per cambiare il valore della proprietà ExternalAccessPrefix per tutti i dial plan configurati per l'utilizzo nell'organizzazione. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsDialPlan** per restituire una raccolta di tutti i dial plan dell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsDialPlan**, che assegna il valore 8 alla proprietà ExternalAccessPrefix per ogni profilo della raccolta.

    Get-CsDialPlan | Set-CsDialPlan -ExternalAccessPrefix 8

## Descrizione dettagliata

Questo cmdlet consente di modificare un dial plan esistente (detto anche profilo di numerazione locale). I dial plan forniscono informazioni necessarie per consentire agli utenti di VoIP aziendale di effettuare telefonate. I dial plan sono utilizzati anche da applicazione Operatore Conferenza per le conferenze telefoniche con accesso esterno. Un dial plan determina le regole di normalizzazione applicate e se è necessario comporre un prefisso per le chiamate esterne.

Nota: sebbene le regole di normalizzazione di un dial plan possano essere modificate con questo cmdlet, è consigliabile utilizzare il cmdlet **New-CsVoiceNormalizationRule**, **Set-CsVoiceNormalizationRule** o **Remove-CsVoiceNormalizationRule** per tale operazione. Le modifiche eseguite con questi cmdlet verranno apportate solo nel dial plan corrispondente.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Set-CsDialPlan** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsDialPlan"}

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
<td><p><em>City</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Questo parametro non è utilizzato con questo cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>CountryCode</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Questo parametro non è utilizzato con questo cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Una descrizione del dial plan: qual è il suo scopo, a quale tipo di utente si applica o qualsiasi altra informazione utile per identificare lo scopo del dial plan.</p>
<p>Numero massimo di caratteri: 512</p></td>
</tr>
<tr class="odd">
<td><p><em>DialinConferencingRegion</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome dell'area geografica associata a questo dial plan. Specificare un valore per questo parametro se il dial plan sarà utilizzato per le conferenze telefoniche con accesso esterno. In questo modo è possibile assegnare il numero di accesso corretto quando l'organizzatore configura la conferenza. Per recuperare le aree geografiche disponibili è possibile chiamare il cmdlet <strong>Get-CsNetworkRegion</strong>.</p>
<p>Numero massimo di caratteri: 512</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalAccessPrefix</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Un numero (o un set di numeri) che identifica la chiamata come esterna all'organizzazione. Ad esempio, per chiamare una linea esterna potrebbe essere necessario premere 9. Questo prefisso sarà ignorato dalle regole di normalizzazione, che saranno quindi applicate alla parte rimanente del numero.</p>
<p>Il parametro OptimizeDeviceDialing deve essere impostato su True affinché questo valore abbia effetto.</p>
<p>Il valore di questo parametro deve corrispondere all'espressione regolare [0-9]{1,4}. Significa che deve essere un valore con una lunghezza compresa tra una e quattro cifre e in cui ogni cifra è compresa tra 0 e 9.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di ignorare le richieste di conferma prima di apportare modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>L'identificatore univoco che specifica l'ambito, o nel caso dei dial plan per utente, il nome, che identifica il dial plan da modificare. Ad esempio, l'identità di un sito deve essere immessa nel formato site:&lt;nomeSito&gt;, dove nomeSito è il nome del sito. Un dial plan nell'ambito del servizio sarà un servizio gateway PSTN o Registrar, il cui valore di identità è formattato come segue: Registrar:Redmond.litwareinc.com. Un'identità per utente viene immessa come un valore stringa univoco.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>LocationProfile</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro. Per recuperare questo riferimento a oggetto è possibile chiamare il cmdlet <strong>Get-CsDialPlan</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>NormalizationRules</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Un elenco di regole di normalizzazione applicate a questo dial plan.</p>
<p>Anche se l'elenco e le regole possono essere create direttamente con questo cmdlet, è consigliabile creare le regole di normalizzazione con il cmdlet <strong>New-CsVoiceNormalizationRule</strong>, che crea la regola e la assegna al dial plan specificato, modificandole con il cmdlet <strong>Set-CsVoiceNormalizationRule</strong>.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>OptimizeDeviceDialing</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Impostando questo parametro su True, alle chiamate esterne all'organizzazione sarà applicato il prefisso specificato nel parametro ExternalAccessPrefix. Questo valore può essere impostato su True solo se è stato specificato un valore per il parametro ExternalAccessPrefix.</p></td>
</tr>
<tr class="even">
<td><p><em>SimpleName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome descrittivo del dial plan. I nomi dei dial plan devono essere univoci tra tutti i dial plan in una distribuzione di Lync Server.</p>
<p>La stringa può contenere fino a 256 caratteri. I caratteri validi sono le lettere dell'alfabeto e i numeri, il trattino (-), il punto (.), il segno più (+), il carattere di sottolineatura (_) e le parentesi (()).</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>State</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Questo parametro non è utilizzato con questo cmdlet.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile. Consente di accettare l'input da pipeline di oggetti dial plan.

## Tipi restituiti

Il cmdlet **Set-CsDialPlan** non restituisce alcun oggetto o valore. Configura invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile.

## Vedere anche

#### Ulteriori risorse

[New-CsDialPlan](new-csdialplan.md)  
[Remove-CsDialPlan](remove-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Grant-CsDialPlan](grant-csdialplan.md)  
[Test-CsDialPlan](test-csdialplan.md)  
[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[Set-CsVoiceNormalizationRule](set-csvoicenormalizationrule.md)  
[Remove-CsVoiceNormalizationRule](remove-csvoicenormalizationrule.md)  
[Get-CsVoiceNormalizationRule](get-csvoicenormalizationrule.md)

