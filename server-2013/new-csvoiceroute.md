---
title: New-CsVoiceRoute
TOCTitle: New-CsVoiceRoute
ms:assetid: 1118f74f-b06c-41d2-8b1b-5cc1e1957b77
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398197(v=OCS.15)
ms:contentKeyID: 49299720
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoiceRoute

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova route vocale. Le route vocali contengono istruzioni che comunicano a Lync Server come instradare le chiamate effettuate da utenti di VoIP aziendale ai numeri di telefono della rete PSTN (Public Switched Telephone Network) o di un centralino (PBX, Private Branch Exchange). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsVoiceRoute -Name <String> <COMMON PARAMETERS>

    New-CsVoiceRoute -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AlternateCallerId <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-NumberPattern <String>] [-Priority <Int32>] [-PstnGatewayList <PSListModifier>] [-PstnUsages <PSListModifier>] [-SuppressCallerId <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando in questo esempio consente di creare una nuova route vocale con identità Route1. Tutte le altre proprietà vengono impostate sui valori predefiniti.

    New-CsVoiceRoute -Identity Route1

## ESEMPIO 2

Il comando in questo esempio consente di creare una nuova route vocale con identità Route1. Inoltre, aggiunge l'utilizzo PSTN Long Distance all'elenco di utilizzi e l'ID di servizio PstnGateway:redmondpool.litwareinc.com all'elenco di gateway PSTN.

    New-CsVoiceRoute -Identity Route1 -PstnUsages @{add="Long Distance"} -PstnGatewayList @{add="PstnGateway:redmondpool.litwareinc.com"}

## ESEMPIO 3

In questo esempio viene creata una nuova route vocale denominata Route1 e nell'elenco di utilizzi PSTN della route vengono inseriti tutti gli utilizzi esistenti per l'organizzazione. Il primo comando dell'esempio recupera l'elenco di utilizzi PSTN globali. La chiamata al cmdlet **Get-CsPstnUsage** è tra parentesi, pertanto verrà innanzitutto recuperato un oggetto contenente le informazioni sugli utilizzi PSTN. Dal momento che esiste un solo utilizzo PSTN globale, verrà recuperato un solo oggetto. Il comando quindi recupera la proprietà Usage di questo oggetto. Tale proprietà, che include un elenco di utilizzi, viene assegnata alla variabile $x. Nella seconda riga di questo esempio viene chiamato il cmdlet **New-CsVoiceRoute** per creare una nuova route vocale. Questa route vocale utilizzerà l'identità Route1. Si noti il valore passato al parametro PstnUsages: @{add=$x}. Questo valore indica la necessità di aggiungere il contenuto di $x, ovvero l'elenco di utilizzi telefono recuperati nella riga 1, all'elenco di utilizzi PSTN per questa route.

    $x = (Get-CsPstnUsage).Usage
    New-CsVoiceRoute -Identity Route1 -PstnUsages @{add=$x}

## Descrizione dettagliata

Utilizzare questo cmdlet per creare una nuova route vocale. Tutte le route vocali vengono create con ambito globale. Tuttavia, è possibile definire più route vocali globali. Per ottenere tale risultato viene utilizzato il parametro Identity, che richiede un nome di route univoco.

Le route vocali sono associate ai criteri vocali per mezzo degli utilizzi PSTN. Una route vocale include un'espressione regolare che identifica quali numeri di telefono saranno instradati attraverso una data route vocale: i numeri di telefono corrispondenti all'espressione regolare saranno instradati attraverso questa route.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **New-CsVoiceRoute** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoiceRoute"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Un nome che identifica in modo univoco la route vocale. Le route vocali possono essere definite solo nell'ambito globale, pertanto l'identità non è altro che il nome che si desidera assegnare alla route. Nel nome della route è possibile inserire spazi, come nel caso di Test Route, ma è necessario racchiudere l'intera stringa tra virgolette doppie nella chiamata al cmdlet <strong>New-CsVoiceRoute</strong>.</p>
<p>Se viene specificato il parametro Identity, Name deve rimanere vuoto. Al parametro Name sarà assegnato il valore di Identity.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il nome univoco della route vocale. Se viene impostato questo parametro, il relativo valore viene automaticamente applicato al parametro Identity della route vocale. Non è possibile specificare sia Identity sia Name.</p></td>
</tr>
<tr class="odd">
<td><p><em>AlternateCallerId</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Se il parametro SuppressCallerId è impostato su True, i destinatari vedranno il valore del parametro AlternateCallerId al posto del numero effettivo del chiamante. Questo numero deve essere valido e può essere utilizzato per rappresentare una divisione all'interno di un'organizzazione, ad esempio l'assistenza tecnica o l'ufficio delle risorse umane.</p>
<p>Se il parametro SuppressCallerId è impostato su False, il parametro AlternateCallerId viene ignorato.</p>
<p>Questo valore deve corrispondere all'espressione regolare (\+)?[1-9]\d*(;ext=[1-9]\d*)?. In altre parole, il valore può, ma non deve, iniziare con un segno più (+), deve essere costituito da un qualsiasi numero di cifre e può essere seguito da un interno che inizia con ;ext= seguito da un qualsiasi numero di cifre. Se si include un interno, la stringa deve essere racchiusa tra virgolette doppie.</p></td>
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
<td><p>Una descrizione dello scopo della route vocale.</p></td>
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
<td><p><em>NumberPattern</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Un'espressione regolare che specifica i numeri di telefono a cui si applica questa route. I numeri che corrispondono a questo modello saranno instradati in base alle rimanenti impostazioni di routing.</p>
<p>Valore predefinito: [0-9]{10}</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Un numero potrebbe essere risolto in più route vocali. La priorità determina l'ordine di applicazione delle route nel caso sia possibile utilizzare più di una route.</p></td>
</tr>
<tr class="even">
<td><p><em>PstnGatewayList</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>In Lync Server un Mediation Server può essere associato a più gateway. Questo parametro include un elenco dei gateway associati a questa route vocale. Ogni membro dell'elenco deve corrispondere all'identità di servizio del gateway PSTN o del Mediation Server. Il valore può fare riferimento a un Mediation Server solo se il Mediation Server è configurato per Microsoft Office Communications Server 2007 o Microsoft Office Communications Server 2007 R2. Per Lync Server è necessario utilizzare un gateway PSTN. L'identità di servizio è una stringa nel formato &lt;RuoloServizio&gt;:&lt;FQDN&gt;, dove RuoloServizio è il nome del ruolo di servizio (PSTNGateway), mentre FQDN è il nome di dominio completo del pool o l'indirizzo IP del server. Ad esempio, PSTNGateway:redmondpool.litwareinc.com. Le identità di servizio possono essere recuperate chiamando il comando Get-CsService | Select-Object Identity.</p>
<p>Per impostazione predefinita, questo elenco è vuoto. Tuttavia, se si lascia vuoto questo parametro quando si crea una nuova route vocale, viene visualizzato un messaggio di avviso.</p></td>
</tr>
<tr class="odd">
<td><p><em>PstnUsages</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>A questa route vocale è possibile applicare un elenco di utilizzi PSTN (ad esempio Locali o Internazionali). L'utilizzo PSTN deve essere già esistente. Per recuperare gli utilizzi PSTN è possibile chiamare il cmdlet <strong>Get-CsPstnUsage</strong>.</p>
<p>Per impostazione predefinita, questo elenco è vuoto. Tuttavia, se si lascia vuoto questo parametro quando si crea una nuova route vocale, viene visualizzato un messaggio di avviso.</p></td>
</tr>
<tr class="even">
<td><p><em>SuppressCallerId</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Consente di determinare se durante le chiamate in uscita sarà visualizzato l'ID del chiamante. Se questo parametro è impostato su True, l'ID del chiamante non viene visualizzato. Al posto dell'ID vero e proprio, viene visualizzato il valore di AlternateCallerId. Se SuppressCallerId è impostato su True, deve essere fornito un valore per AlternateCallerId.</p></td>
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

Consente di creare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route.

## Vedere anche

#### Ulteriori risorse

[Remove-CsVoiceRoute](remove-csvoiceroute.md)  
[Set-CsVoiceRoute](set-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)  
[Test-CsVoiceRoute](test-csvoiceroute.md)  
[Get-CsPstnUsage](get-cspstnusage.md)  
[Get-CsService](get-csservice.md)

