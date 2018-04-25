---
title: Set-CsImFilterConfiguration
TOCTitle: Set-CsImFilterConfiguration
ms:assetid: c2b08cc0-8261-4b8b-b2e9-5efa902ceb40
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412960(v=OCS.15)
ms:contentKeyID: 49301902
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsImFilterConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una configurazione del filtro di messaggistica istantanea esistente. Le impostazioni del filtro di messaggistica istantanea vengono utilizzate per impedire agli utenti di inviare messaggi istantanei contenenti collegamenti ipertestuali attivi (su cui è possibile fare clic). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsImFilterConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsImFilterConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Action <Allow | Block | Warn>] [-AllowMessage <String>] [-BlockFileExtension <$true | $false>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-IgnoreLocal <$true | $false>] [-Prefixes <PSListModifier>] [-WarnMessage <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato in questo esempio disabilita il meccanismo di filtro URI per la configurazione del filtro di messaggistica istantanea con valore Identity site:Redmond. Per eseguire questa attività, viene specificato il parametro Enabled con valore $False nella chiamata al cmdlet **Set-CsImFilterConfiguration**.

    Set-CsImFilterConfiguration -Identity site:Redmond -Enabled $False

## ESEMPIO 2

Nell'esempio 2 viene aggiunto un nuovo prefisso URI (urn:) all'elenco dei prefissi vietati dalla configurazione del filtro di messaggistica istantanea per site:Redmond. Per aggiungere il nuovo prefisso, viene utilizzato il cmdlet **Get-CsImFilterConfiguration** per recuperare la configurazione per site:Redmond. L'oggetto restituito che rappresenta la configurazione viene archiviato in una variabile denominata $x. Dopo il recupero delle impostazioni, viene chiamato il metodo Add() nella riga 2 per aggiungere urn: al set dei prefissi memorizzati nella proprietà Prefixes. Questa operazione cambia il valore del riferimento dell'oggetto $x. Per cambiare la configurazione vera e propria, la riga 3 chiama il cmdlet **Set-CsImFilterConfiguration**, passando $x come unico valore del parametro.

    $x = Get-CsImFilterConfiguration -Identity site:Redmond
    $x.Prefixes.Add("urn:")
    Set-CsImFilterConfiguration -Instance $x

## ESEMPIO 3

L'esempio 3 esegue la stessa operazione descritta nell'esempio 2, ma lo fa in un'unica riga. In questo comando viene utilizzato il parametro Prefixes del cmdlet **Set-CsImFilterConfiguration** per aggiungere urn: all'elenco dei prefissi. Il modificatore di elenco Add è utilizzato per aggiungere questo valore all'elenco dei prefissi.

    Set-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{add="urn:"}

## ESEMPIO 4

In questo esempio, il prefisso urn: viene rimosso dall'elenco dei prefissi bloccati dalla configurazione del filtro di messaggistica istantanea per site:Redmond. Questo esempio è identico all'esempio 3: la sola differenza consiste nel fatto che, invece di chiamare il modificatore di elenco Add per aggiungere un prefisso all'elenco, viene chiamato il modificatore di elenco Remove per rimuovere un prefisso.

    Set-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{remove="urn:"}

## Descrizione dettagliata

Quando vengono inviati messaggi istantanei, gli utenti possono incorporare nel testo del messaggio un URI (Uniform Resource Identifier) per rimandare a una condivisione o a un sito Web particolare gli altri partecipanti alla conversazione. È possibile configurare Lync Server in modo che i collegamenti ipertestuali con determinati prefissi vengano bloccati o non risultino attivi. In altri termini, i partecipanti non possono semplicemente fare clic sul collegamento per accedere al sito a cui fa riferimento l'URI, ma devono manualmente copiare e incollare il collegamento in un browser.

Il cmdlet **Set-CsImFilterConfiguration** consente di modificare un elenco di prefissi URI da filtrare, nonché di abilitare e disabilitare completamente il filtro a livello globale o all'interno di un sito specifico. Con questo cmdlet è anche possibile aggiornare i diversi messaggi di avviso visualizzati agli utenti.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsImFilterConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsImFilterConfiguration"}

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
<td><p><em>Action</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>UrlFilterAction</p></td>
<td><p>Il valore di questo parametro determina l'azione da eseguire quando in un messaggio istantaneo è incluso un collegamento ipertestuale:</p>
<p>Allow - I collegamenti ipertestuali contengono un carattere di sottolineatura (_) come prefisso in modo che i collegamenti non siano più attivi. Se inoltre si specifica un messaggio nella proprietà AllowMessage, verrà inserito un messaggio di notifica all'inizio di ogni messaggio istantaneo contenente collegamenti ipertestuali.</p>
<p>Block - La consegna di messaggi contenenti collegamenti ipertestuali attivi è bloccata e Lync Server invia un messaggio di errore al mittente.</p>
<p>Warn - I messaggi contenenti collegamenti ipertestuali attivi vengono recapitati ai destinatari, unitamente a un messaggio di avviso inserito all'inizio dei messaggi. È possibile specificare il messaggio di avviso utilizzando la proprietà WarnMessage. Se si specifica Warn e non si immette la proprietà WarnMessage, il filtro di protezione dei messaggi istantanei viene disabilitato, anche se le impostazioni relative alla proprietà BlockFileExtension vengono comunque rispettate.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>AllowMessage</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Se si specifica un valore per il parametro, quando il valore della proprietà Action è impostato su Allow, la stringa viene inserita all'inizio di ogni messaggio contenente collegamenti ipertestuali. È possibile utilizzare questo messaggio per l'invio di notifiche agli utenti, ad esempio sui potenziali pericoli che derivano dalla selezione di collegamenti sconosciuti o sui criteri e i requisiti relativi all'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>BlockFileExtension</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se il parametro è impostato su True, viene bloccato un collegamento ipertestuale contenente un percorso file con un'estensione specificata dalla proprietà Extensions definita nella classe Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileTransferFilterConfiguration (recuperata tramite il cmdlet <strong>Get-CsFileTransferFilterConfiguration</strong>) e viene restituito un messaggio di errore al mittente. Se il parametro è impostato su False, non viene eseguito alcun particolare controllo sui percorsi e sulle estensioni dei file.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Consente di abilitare o disabilitare questa funzionalità. Se il parametro è impostato su True, i messaggi istantanei verranno esaminati alla ricerca di collegamenti ipertestuali e si applicheranno le regole all'interno della configurazione. Se il parametro è impostato su False, i messaggi non verranno controllati alla ricerca di collegamenti ipertestuali.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>XdsIdentity</p></td>
<td><p>L'identificatore univoco delle impostazioni di configurazione del filtro dei messaggi istantanei che si desidera modificare. Questo valore sarà global o site:&lt;nome sito&gt;, dove &lt;nome sito&gt; è il sito a cui si applica la configurazione, ad esempio site:Redmond.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreLocal</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Il valore di questo parametro controlla se il filtraggio viene eseguito sugli URI della Intranet locale passati nei messaggi istantanei. Se il parametro è impostato su True, qualsiasi URI definito all'interno dell'area Intranet del computer locale viene ignorato. Il computer locale è il Front End Server che esegue l'applicazione del filtro di messaggistica istantanea. Se il parametro è impostato su False, il filtro di protezione specificato viene applicato a tutti i collegamenti ipertestuali.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>ImFilterConfiguration</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro. Il cmdlet accetta un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration, che può essere recuperato chiamando il cmdlet <strong>Get-CsImFilterConfiguration</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Prefixes</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>L'elenco dei prefissi URI che verranno filtrati. Qualsiasi collegamento ipertestuale incluso in un messaggio istantaneo con un prefisso corrispondente a uno dei prefissi in elenco verrà filtrato in base alle impostazioni specifiche.</p>
<p>Valore predefinito: callto:, file:, ftp., ftp:, gopher:, href, http:, https:, ldap:, mailto:, news:, nntp:, sip:, sips:, tel:, telnet:, www*.</p></td>
</tr>
<tr class="odd">
<td><p><em>WarnMessage</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Quando il valore della proprietà Action è impostato su Warn, questo parametro contiene il messaggio di avviso inserito all'inizio di ogni messaggi istantaneo contenente i collegamenti ipertestuali. Questo tipo di messaggio viene generalmente utilizzato per l'invio di notifiche sui potenziali pericoli derivanti dalla selezione di collegamenti sconosciuti o sui criteri e i requisiti relativi all'organizzazione.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration. Accetta l'input da pipeline di oggetti di configurazione del filtro di messaggistica istantanea.

## Tipi restituiti

Il cmdlet **Set-CsImFilterConfiguration** non restituisce un valore o un oggetto. Il cmdlet configura invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsImFilterConfiguration](new-csimfilterconfiguration.md)  
[Remove-CsImFilterConfiguration](remove-csimfilterconfiguration.md)  
[Get-CsImFilterConfiguration](get-csimfilterconfiguration.md)

