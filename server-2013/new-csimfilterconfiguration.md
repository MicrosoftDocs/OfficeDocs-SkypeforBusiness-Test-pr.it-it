---
title: New-CsImFilterConfiguration
TOCTitle: New-CsImFilterConfiguration
ms:assetid: 1964cbf9-d7f1-4b4e-99d1-951ac42d82fe
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398244(v=OCS.15)
ms:contentKeyID: 49299825
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsImFilterConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova configurazione del filtro di messaggistica istantanea. I filtri di messaggistica istantanea vengono utilizzati per impedire agli utenti di inviare messaggi istantanei contenenti collegamenti ipertestuali attivi. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsImFilterConfiguration -Identity <XdsIdentity> [-Action <Allow | Block | Warn>] [-AllowMessage <String>] [-BlockFileExtension <$true | $false>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-IgnoreLocal <$true | $false>] [-InMemory <SwitchParameter>] [-Prefixes <PSListModifier>] [-WarnMessage <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 il cmdlet **New-CsImFilterConfiguration** viene utilizzato per creare una nuova configurazione del filtro di messaggistica istantanea con identità (Identity) site:Redmond. Dal momento che non sono stati specificati parametri aggiuntivi, queste impostazioni verranno create utilizzando i valori predefiniti.

    New-CsImFilterConfiguration -Identity site:Redmond

## ESEMPIO 2

In questo comando il cmdlet **New-CsImFilterConfiguration** viene utilizzato per creare una nuova configurazione del filtro di messaggistica istantanea con identità site:Redmond. Poiché è stato specificato il parametro Prefixes, la nuova configurazione includerà tutti i valori predefiniti, compresi i prefissi predefiniti da filtrare, più due prefissi URI aggiuntivi, ovvero rtsp: e urn:. Questi prefissi vengono aggiunti utilizzando il modificatore per l'aggiunta di prefissi all'elenco predefinito.

    New-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{add="rtsp:","urn:"}

## ESEMPIO 3

In questo comando il cmdlet **New-CsFileTransferFilterConfiguration** viene utilizzato per creare una nuova configurazione del filtro di messaggistica istantanea con identità site:Redmond. Questo esempio è simile all'esempio 2, tranne per il fatto che è stato utilizzato il modificatore per la sostituzione dell'elenco, anziché quello per l'aggiunta all'elenco. In pratica, tutti i prefissi URI predefiniti saranno sostituiti da questi due prefissi (rtsp: e urn:). Di conseguenza, saranno filtrati solo gli URI con i prefissi rtsp: o urn: nei messaggi istantanei per il sito Redmond.

    New-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{replace="rtsp:","urn:"}

## Descrizione dettagliata

Quando si inviano messaggi istantanei, gli utenti possono incorporare nel testo del messaggio un URI (Uniform Resource Identifier) per rimandare a una condivisione o a un sito Web specifico gli altri partecipanti alla conversazione. È possibile configurare Lync Server in modo che i collegamenti ipertestuali con determinati prefissi vengano bloccati o non risultino attivi. In altri termini, i partecipanti non possono semplicemente fare clic sul collegamento per accedere al sito a cui fa riferimento l'URI, ma devono copiare e incollare manualmente il collegamento in un browser.

Il cmdlet **New-CsImFilterConfiguration** consente di definire un elenco di prefissi URI da filtrare (nonché di abilitare e disabilitare del tutto il filtro) all'interno di un sito specifico. Una chiamata al cmdlet **New-CsImFilterConfiguration** in cui è specificata solamente un'identità consente di creare una nuova configurazione con tale identità e di inserire nell'elenco Prefissi di quel sito un set di prefissi predefiniti che saranno filtrati.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **New-CsImFilterConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsImFilterConfiguration"}

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
<td><p>XdsIdentity</p></td>
<td><p>Un identificatore univoco che specifica l'ambito della configurazione del filtro di messaggistica istantanea. Le impostazioni globali esistono per impostazione predefinita, quindi non è possibile ricrearle con il cmdlet <strong>New-CsImFilterConfiguration</strong>; tuttavia, è possibile creare impostazioni a livello di sito specificando un'identità site:&lt;nome sito&gt;, dove &lt;nome sito&gt; è il nome del sito a cui saranno applicate le impostazioni (ad esempio site:Redmond).</p>
<p>Tipo di dati completi: Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
</tr>
<tr class="even">
<td><p><em>Action</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>UrlFilterAction</p></td>
<td><p>Il valore di questo parametro determina l'azione da eseguire quando in un messaggio istantaneo è incluso un collegamento ipertestuale:</p>
<p>Allow - I collegamenti ipertestuali contengono un carattere di sottolineatura (_) come prefisso in modo che i collegamenti non siano più attivi. Se si specifica un messaggio nella proprietà AllowMessage, tale messaggio verrà inserito all'inizio di ogni messaggio istantaneo contenente collegamenti ipertestuali.</p>
<p>Block - Il recapito di messaggi contenenti collegamenti ipertestuali attivi è bloccato e Lync Server invia un messaggio di errore al mittente.</p>
<p>Warn - I messaggi contenenti collegamenti ipertestuali attivi vengono recapitati ai destinatari, unitamente a un messaggio di avviso inserito all'inizio dei messaggi. È possibile specificare il messaggio di avviso utilizzando la proprietà WarnMessage. Se si specifica Warn e non si immette la proprietà WarnMessage, il filtro di protezione dei messaggi istantanei viene disabilitato, anche se le impostazioni relative alla proprietà BlockFileExtension vengono comunque rispettate.</p>
<p>Valore predefinito: Allow, a meno che un messaggio contenga più di 1.000 URL, caso in cui l'impostazione predefinita è Block.</p>
<p>Tipo di dati completi: Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.UrlFilterAction</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowMessage</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Se si specifica un valore per il parametro, quando il valore della proprietà Action è impostato su Allow, la stringa viene inserita all'inizio di ogni messaggio contenente collegamenti ipertestuali. È possibile utilizzare questo messaggio per l'invio di notifiche agli utenti, ad esempio sui potenziali pericoli che derivano dalla selezione di collegamenti sconosciuti o sui criteri e i requisiti relativi all'organizzazione.</p></td>
</tr>
<tr class="even">
<td><p><em>BlockFileExtension</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se il parametro è impostato su True, un collegamento ipertestuale contenente un percorso file con un'estensione specificata dalla proprietà Extensions definita nella configurazione del filtro di trasferimento file applicabile (recuperata tramite il cmdlet <strong>Get-CsFileTransferFilterConfiguration</strong>) è bloccato e viene restituito un messaggio di errore al mittente. Se il parametro è impostato su False, non viene eseguito alcun particolare controllo sulle estensioni dei file.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Consente di abilitare o disabilitare questa funzionalità. Se il parametro è impostato su True, i messaggi istantanei verranno esaminati alla ricerca di collegamenti ipertestuali e si applicheranno le regole all'interno della configurazione. Se il parametro è impostato su False, i messaggi non verranno controllati alla ricerca di collegamenti ipertestuali.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreLocal</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Il valore di questo parametro controlla se il filtraggio viene eseguito sugli URI della Intranet locale passati nei messaggi istantanei. Se il parametro è impostato su True, qualsiasi URI definito all'interno dell'area Intranet del computer locale viene ignorato. Il computer locale è il Front End Server che esegue l'applicazione del filtro di messaggistica istantanea. Se il parametro è impostato su False, il filtro di protezione specificato viene applicato a tutti i collegamenti ipertestuali.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
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

Nessuno.

## Tipi restituiti

Crea un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration.

## Vedere anche

#### Ulteriori risorse

[Remove-CsImFilterConfiguration](remove-csimfilterconfiguration.md)  
[Set-CsImFilterConfiguration](set-csimfilterconfiguration.md)  
[Get-CsImFilterConfiguration](get-csimfilterconfiguration.md)

