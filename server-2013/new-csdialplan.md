---
title: New-CsDialPlan
TOCTitle: New-CsDialPlan
ms:assetid: 3889c696-1070-47bd-beb9-da7e18ec90f0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425860(v=OCS.15)
ms:contentKeyID: 49300210
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsDialPlan

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo dial plan. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsDialPlan -Identity <XdsIdentity> [-City <String>] [-Confirm [<SwitchParameter>]] [-CountryCode <String>] [-Description <String>] [-DialinConferencingRegion <String>] [-ExternalAccessPrefix <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-NormalizationRules <PSListModifier>] [-OptimizeDeviceDialing <$true | $false>] [-SimpleName <String>] [-State <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 è possibile creare un nuovo dial plan con identità RedmondDialPlan. L'assenza di un ambito nel valore di Identity indica che si tratta di un criterio per utente. I dial plan creati con ambito per utente possono essere assegnati direttamente a utenti e gruppi. Tutte le altre proprietà del dial plan sono impostate sui valori predefiniti.

    New-CsDialPlan -Identity RedmondDialPlan

## ESEMPIO 2

I comandi riportati nell'esempio 2 creano un nuovo dial plan con Identity site:Redmond (vale a dire che il dial plan si applica a tutti gli utenti nel sito Redmond a cui non è assegnato un dial plan a livello di servizio o per utente) e SimpleName RedmondSiteDialPlan. La riga successiva dell'esempio quindi crea una nuova regola di normalizzazione associata al dial plan. La regola di normalizzazione predefinita per un dial plan viene creata principalmente come segnaposto, in quanto i valori sono di uso limitato. Dopo avere chiamato il cmdlet **New-CsDialPlan** per creare un nuovo dial plan, è pertanto opportuno chiamare il cmdlet **New-CsVoiceNormalizationRule** per creare una regola denominata funzionale per l'organizzazione. Questo è lo scopo della riga 2 dell'esempio, che chiama il cmdlet **New-CsVoiceNormalizationRule** e crea per il sito Redmond una regola con il nome SeattlePrefix, specificando le proprietà Pattern e Translation per la regola. Non sono necessari altri passaggi per modificare il dial plan. Le modifiche alla regola di normalizzazione vengono infatti applicate automaticamente al dial plan la cui identità corrisponde a quella della regola di normalizzazione. La parte site:Redmond del parametro Identity corrisponde all'identità del dial plan. SeattlePrefix è il nome della regola di normalizzazione. A un dial plan è possibile applicare più regole di normalizzazione, quindi ogni regola di normalizzazione necessita di un nome univoco in un determinato ambito.

    New-CsDialPlan -Identity site:Redmond -SimpleName RedmondSiteDialPlan
    New-CsVoiceNormalizationRule -Identity "site:Redmond/SeattlePrefix" -Pattern "^9(\d*){1,5}$" -Translation "+1206$1"

## ESEMPIO 3

Con il comando mostrato nell'esempio 3 è possibile creare un nuovo dial plan con Identity RedmondDialPlan e specificare un parametro Description che spieghi lo scopo del dial plan. I dial plan creati con ambito per utente possono essere assegnati direttamente a utenti e gruppi. A tutti gli altri parametri saranno assegnati i valori predefiniti.

    New-CsDialPlan -Identity RedmondDialPlan -Description "Dial plan for Redmond users"

## Descrizione dettagliata

Questo cmdlet consente di creare un nuovo dial plan (detto anche profilo località). I dial plan forniscono informazioni necessarie per consentire agli utenti di VoIP aziendale di effettuare telefonate. I dial plan sono utilizzati anche da applicazione Operatore Conferenza per le conferenze telefoniche con accesso esterno. Un dial plan determina le regole di normalizzazione applicate e se è necessario comporre un prefisso per le chiamate esterne.

La creazione di un dial plan provoca la creazione automatica di una regola di normalizzazione vocale predefinita. Le regole di normalizzazione possono essere modificate chiamando il cmdlet **Set-CsVoiceNormalizationRule**. Le nuove regole di normalizzazione possono essere aggiunte a un dial plan chiamando il cmdlet **New-CsVoiceNormalizationRule**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **New-CsDialPlan** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsDialPlan"}

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
<td><p>Un identificatore univoco che specifica l'ambito e il nome (sito), il ruolo del servizio e il nome di dominio completo, oppure il nome (per utente) per identificare il dial plan. Ad esempio, l'identità di un sito deve essere immessa nel formato &lt;nomeSito&gt;, dove nomeSito è il nome del sito. Un dial plan nell'ambito del servizio deve essere un servizio gateway PSTN o Registrar, il cui valore di identità è formattato come segue: Registrar:Redmond.litwareinc.com. Un'identità per utente viene immessa come un valore stringa univoco.</p></td>
</tr>
<tr class="even">
<td><p><em>City</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Questo parametro non è utilizzato con questo cmdlet.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>CountryCode</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Questo parametro non è utilizzato con questo cmdlet.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Una descrizione del dial plan: qual è il suo scopo, a quale tipo di utente si applica o qualsiasi altra informazione utile per identificare lo scopo del dial plan.</p>
<p>Numero massimo di caratteri: 512</p></td>
</tr>
<tr class="even">
<td><p><em>DialinConferencingRegion</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome dell'area geografica associata a questo dial plan. Specificare un valore per questo parametro se il dial plan sarà utilizzato per le conferenze telefoniche con accesso esterno. In questo modo è possibile assegnare il numero di accesso corretto quando l'organizzatore configura la conferenza. Per recuperare le aree geografiche disponibili è possibile chiamare il cmdlet <strong>Get-CsNetworkRegion</strong>.</p>
<p>Numero massimo di caratteri: 512</p></td>
</tr>
<tr class="odd">
<td><p><em>ExternalAccessPrefix</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Un numero (o un set di numeri) che identifica la chiamata come esterna all'organizzazione. Ad esempio, per chiamare una linea esterna potrebbe essere necessario premere 9. Questo prefisso sarà ignorato dalle regole di normalizzazione, che saranno quindi applicate alla parte rimanente del numero.</p>
<p>Il parametro OptimizeDeviceDialing deve essere impostato su True affinché questo valore abbia effetto.</p>
<p>Questo parametro deve corrispondere all'espressione regolare [0-9]{1,4}. Significa che deve essere un valore compreso tra 0 e 9 con una lunghezza compresa tra una e quattro cifre.</p>
<p>Valore predefinito: 9</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di ignorare le richieste di conferma prima di apportare modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>NormalizationRules</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Un elenco di regole di normalizzazione applicate a questo dial plan.</p>
<p>Anche se l'elenco e le regole possono essere creati direttamente con questo cmdlet, è consigliabile creare le regole di normalizzazione con il cmdlet <strong>New-CsVoiceNormalizationRule</strong>, che consente di creare la regola e assegnarla al dial plan specificato.</p>
<p>Ogni volta che viene creato un nuovo dial plan, viene creata anche una nuova regola di normalizzazione vocale con impostazioni predefinite per tale dial plan di sito, servizio o per utente. Per impostazione predefinita, l'identità della nuova regola di normalizzazione vocale corrisponde all'identità del dial plan seguita da una barra e dal nome Prefix All. Ad esempio: site:Redmond/Prefix All.</p>
<p>Valore predefinito: {Description=;Pattern=^(\d11)$;Translation=+$1;Name=Prefix All;IsInternalExtension=False } Nota: questa impostazione predefinita non è altro che un segnaposto. Perché il dial plan sia utile, è necessario modificare la regola di normalizzazione creata dal dial plan oppure creare una nuova regola per il sito, il servizio o l'utente. È possibile creare una nuova regola di normalizzazione chiamando il cmdlet <strong>New-CsVoiceNormalizationRule</strong>. Per modificare una regola di normalizzazione, chiamare il cmdlet <strong>Set-CsVoiceNormalizationRule</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>OptimizeDeviceDialing</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Impostando questo parametro su True, alle chiamate esterne all'organizzazione sarà applicato il prefisso specificato nel parametro ExternalAccessPrefix. Questo valore può essere impostato su True solo se è stato specificato un valore per il parametro ExternalAccessPrefix.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="even">
<td><p><em>SimpleName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome visualizzato del dial plan. Questo nome deve essere univoco all'interno della distribuzione di Lync Server.</p>
<p>La stringa può contenere fino a 256 caratteri. I caratteri validi sono le lettere dell'alfabeto e i numeri, il trattino (-), il punto (.), il segno più (+), il carattere di sottolineatura (_) e le parentesi (()).</p>
<p>Questo parametro deve includere un valore. Se però non si specifica un valore nella chiamata al cmdlet <strong>New-CsDialPlan</strong>, viene utilizzato un valore predefinito. Il valore predefinito per un dial plan globale è Prefix All. L'impostazione predefinita per un dial plan a livello di sito è il nome del sito. L'impostazione predefinita per un servizio è il nome del servizio (funzione di registrazione o gateway PSTN) seguito da un carattere di sottolineatura e dal nome di dominio completo (FQDN) del servizio. Ad esempio: Registrar_pool0.litwareinc.com. L'impostazione predefinita per un dial plan per utente è l'identità del dial plan.</p></td>
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

Nessuno.

## Tipi restituiti

Questo cmdlet consente di creare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile.

## Vedere anche

#### Ulteriori risorse

[Remove-CsDialPlan](remove-csdialplan.md)  
[Set-CsDialPlan](set-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Grant-CsDialPlan](grant-csdialplan.md)  
[Test-CsDialPlan](test-csdialplan.md)  
[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[Set-CsVoiceNormalizationRule](set-csvoicenormalizationrule.md)  
[Remove-CsVoiceNormalizationRule](remove-csvoicenormalizationrule.md)  
[Get-CsVoiceNormalizationRule](get-csvoicenormalizationrule.md)

