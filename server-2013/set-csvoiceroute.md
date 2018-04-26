---
title: Set-CsVoiceRoute
TOCTitle: Set-CsVoiceRoute
ms:assetid: b786aec0-946e-4ce5-812e-25e5d8cfa4d5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412893(v=OCS.15)
ms:contentKeyID: 49301762
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceRoute

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una route vocale. Le route vocali contengono istruzioni che comunicano a Lync Server come instradare le chiamate effettuate da utenti di VoIP aziendale ai numeri di telefono della rete PSTN (Public Switched Telephone Network) o di un centralino (PBX, Private Branch Exchange). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsVoiceRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceRoute [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AlternateCallerId <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-NumberPattern <String>] [-Priority <Int32>] [-PstnGatewayList <PSListModifier>] [-PstnUsages <PSListModifier>] [-SuppressCallerId <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Questo comando imposta la descrizione della route vocale Route1 su "Test Route."

    Set-CsVoiceRoute -Identity Route1 -Description "Test Route"

## ESEMPIO 2

Il comando riportato in questo esempio modifica la route vocale con identità Route1 per aggiungere l'utilizzo PSTN "Long Distance" all'elenco di utilizzi della route vocale. "Long Distance" deve figurare nell'elenco di utilizzi PSTN globali, che è possibile recuperare chiamando il cmdlet **Get-CsPstnUsage**.

    Set-CsVoiceRoute -Identity Route1 -PstnUsages @{add="Long Distance"}

## ESEMPIO 3

In questo esempio viene modificata la route vocale denominata Route1 in modo da inserire nell'elenco di utilizzi PSTN di tale route tutti gli utilizzi esistenti per l'organizzazione. Il primo comando in questo esempio recupera l'elenco di utilizzi PSTN globali. La chiamata al cmdlet **Get-CsPstnUsage** è tra parentesi, a indicare che è necessario innanzitutto recuperare un oggetto contenente le informazioni sugli utilizzi PSTN. Dal momento che esiste un solo utilizzo PSTN globale, sarà recuperato un solo oggetto. Il comando recupera quindi la proprietà Usage di tale oggetto. Tale proprietà, che include un elenco di utilizzi PSTN, viene assegnata alla variabile $x. Nella seconda riga di questo esempio viene chiamato il cmdlet **Set-CsVoiceRoute** per modificare la route vocale con identità Route1. Si noti il valore passato al parametro PstnUsages: @{replace=$x}. Questo valore indica la necessità di sostituire ogni elemento nell'elenco PstnUsages della route con il contenuto di $x, che include l'elenco di utilizzi PSTN recuperati nella riga 1.

    $x = (Get-CsPstnUsage).Usage
    Set-CsVoiceRoute -Identity Route1 -PstnUsages @{replace=$x}

## ESEMPIO 4

Questo set di comandi modifica la proprietà Name della route vocale con identità Route1 in RouteA. La modifica della proprietà Name modificherà automaticamente la proprietà Identity, in questo caso in RouteA.

Nella prima riga viene chiamato il cmdlet **Get-CsVoiceRoute** per recuperare la route vocale con identità Route1. L'oggetto restituito viene archiviato nella variabile $x. In seguito, alla proprietà Name dell'oggetto viene assegnato il valore stringa "RouteA". L'oggetto contenuto nella variabile $x viene infine passato al parametro Instance del cmdlet **Set-CsVoiceRoute** per la modifica.

    $x = Get-CsVoiceRoute -Identity Route1
    $x.Name = "RouteA"
    Set-CsVoiceRoute -Instance $x

## ESEMPIO 5

In questo esempio viene modificata la route vocale denominata Route1 e nell'elenco di gateway PSTN della route (PstnGatewayList) viene inserito il ruolo del server del gateway con valore Identity uguale a PstnGateway:192.168.0.100. Nella prima riga dell'esempio viene chiamato il cmdlet **Get-CsVoiceRoute** per recuperare la route vocale che si desidera modificare, in questo caso Route1. Viene quindi chiamato il metodo Add per la proprietà PstnGatewayList di Route1. Al metodo Add viene passata l'identità del servizio che si intende aggiungere. Viene chiamato infine il cmdlet **Set-CsVoiceRoute**, passando al parametro Instance la variabile $y, che aggiornerà Route1 (archiviata in $y) con il gateway PSTN appena aggiunto.

    $y = Get-CsVoiceRoute -Identity Route1
    $y.PstnGatewayList.Add("PstnGateway:192.168.0.100")
    Set-CsVoiceRoute -Instance $y

## Descrizione dettagliata

Utilizzare questo cmdlet per modificare una route vocale esistente. Le route vocali sono associate ai criteri vocali attraverso la rete PSTN (Public switched telephone network). Una route vocale include un'espressione regolare che identifica quali numeri di telefono saranno instradati attraverso una data route vocale: i numeri di telefono corrispondenti all'espressione regolare saranno instradati attraverso questa route.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsVoiceRoute** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceRoute"}

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
<td><p>Una descrizione dello scopo della route telefonica.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>L'identità univoca della route vocale. (Se il nome della route contiene uno spazio come ad esempio Test Route, è necessario chiudere la stringa tra due parentesi).</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Route</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro. L'oggetto deve essere di tipo Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route e può essere recuperato chiamando il cmdlet <strong>Get-CsVoiceRoute</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>NumberPattern</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Un'espressione regolare che specifica i numeri di telefono a cui si applica questa route. I numeri che corrispondono a questo modello saranno instradati in base alle rimanenti impostazioni di routing. Il modello dei numeri predefinito [0-9]{10} ad esempio specifica un numero a 10 cifre contenente cifre comprese tra 0 e 9.</p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Un numero potrebbe essere risolto in più route vocali. La priorità determina l'ordine di applicazione delle route nel caso sia possibile utilizzare più di una route.</p></td>
</tr>
<tr class="odd">
<td><p><em>PstnGatewayList</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Un Mediation Server può essere associato a più gateway. Questo parametro include un elenco di gateway associati a questa route vocale. Ogni membro dell'elenco deve corrispondere all'identità del servizio del gateway PSTN o del Mediation Server. Il valore può fare riferimento a un Mediation Server solo se il Mediation Server è configurato per Microsoft Office Communications Server 2007 o Microsoft Office Communications Server 2007 R2. Per Lync Server è necessario utilizzare un gateway PSTN. L'identità del servizio è una stringa nel formato ServiceRole:FQDN, dove ServiceRole è il nome del ruolo del servizio (PSTNGateway) e FQDN è il nome di dominio completo del pool o l'indirizzo IP del server, ad esempio PSTNGateway:redmondpool.litwareinc.com. Le identità del servizio possono essere recuperate chiamando il comando Get-CsService | Select-Object Identity.</p>
<p>Se si apportano modifiche a una route vocale e si lascia l'elenco PstnGatewayList vuoto o se la modifica introdotta rimuove tutti le voci in elenco, gli utenti riceveranno un messaggio di avviso che notificherà l'impossibilità di effettuare chiamate PSTN.</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>A questa route vocale è possibile applicare un elenco di utilizzi PSTN (ad esempio Locali o Internazionali). L'utilizzo PSTN deve essere già esistente. Per recuperare gli utilizzi PSTN è possibile chiamare il cmdlet <strong>Get-CsPstnUsage</strong>.</p>
<p>Se si apportano modifiche a una route vocale e si lascia l'elenco PstnUsages vuoto o se la modifica introdotta rimuove tutti gli utilizzi PSTN nell'elenco, gli utenti riceveranno un messaggio di avviso che notificherà l'impossibilità di effettuare chiamate PSTN.</p></td>
</tr>
<tr class="odd">
<td><p><em>SuppressCallerId</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Consente di determinare se durante le chiamate in uscita sarà visualizzato l'ID del chiamante. Se questo parametro è impostato su True, l'ID del chiamante non viene visualizzato. Al posto dell'ID vero e proprio, viene visualizzato il valore di AlternateCallerId. Se SuppressCallerId è impostato su True, deve essere fornito un valore per AlternateCallerId.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route. Il cmdlet **Set-CsVoiceRoute** accetta l'input di oggetti route vocale inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsVoiceRoute** non restituisce un valore o un oggetto. Configura invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route.

## Vedere anche

#### Ulteriori risorse

[New-CsVoiceRoute](new-csvoiceroute.md)  
[Remove-CsVoiceRoute](remove-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)  
[Test-CsVoiceRoute](test-csvoiceroute.md)  
[Get-CsPstnUsage](get-cspstnusage.md)  
[Get-CsService](get-csservice.md)

