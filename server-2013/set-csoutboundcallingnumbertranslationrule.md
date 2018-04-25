---
title: Set-CsOutboundCallingNumberTranslationRule
TOCTitle: Set-CsOutboundCallingNumberTranslationRule
ms:assetid: e9a7190a-a50d-4d01-8f33-66ed88a52b9e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205400(v=OCS.15)
ms:contentKeyID: 49302326
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsOutboundCallingNumberTranslationRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una regola di conversione dei numeri in uscita esistente. Una regola di questo tipo converte i numeri di telefono E.164 utilizzati da Lync Server 2013 in un formato utilizzabile dai peer di trunking che non supportano tali numeri. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsOutboundCallingNumberTranslationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsOutboundCallingNumberTranslationRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-Pattern <String>] [-Priority <Int32>] [-Translation <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 modifica la priorità della regola di conversione del numero di chiamata in uscita con l'identità site:Redmond/SevenDigit. In questo esempio, la priorità è impostata su 0.

    Set-CsOutboundCallingNumberTranslationRule -Identity "site:Redmond/SevenDigit" -Priority 0

## Descrizione dettagliata

Le regole di conversione dei numeri in uscita convertono i numeri di telefono E.164 utilizzati da Lync 2013 in un formato utilizzabile dai peer di trunking che non supportano i numeri E.164. Quando si crea una regola di conversione, si fornisce un'espressione regolare che rappresenta il numero E.164 in uscita (formato) e un'espressione regolare che rappresenta il numero convertito (conversione).

Le regole di conversione dei numeri in uscita devono essere associate a una raccolta di impostazioni di configurazione trunk. Quando si crea una nuova regola di conversione, è necessario specificare sia l'identità delle impostazioni di configurazione del trunking che il nome della nuova regola, ad esempio site:Redmond/RedmondTranslationRule. Si noti che le impostazioni di configurazione del trunking non devono necessariamente essere già presenti quando si crea una nuova regola. Si supponga ad esempio di creare la regola site:Redmond/RedmondTranslationRule e che non siano state create impostazioni di configurazione trunk per il sito Redmond. Se Redmond è un sito valido, le impostazioni di configurazione trunk verranno create automaticamente per il sito e la nuova regola di conversione verrà assegnata a tale raccolta di impostazioni. Il comando tuttavia avrà esito negativo se il sito Redmond non esiste.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsOutboundCallingNumberTranslationRule"}

**Pannello di controllo di Lync Server:** Per modificare una regola di conversione del numero di chiamata utilizzando Pannello di controllo di Lync Server, fare clic su Routing vocale, Configurazione trunk e quindi fare doppio clic sulle impostazioni di configurazione contenenti la regola da modificare. Nella finestra di dialogo Modifica configurazione trunk scorrere verso il basso fino alla sezione relativa alle regole di conversione del numero di chiamata e quindi fare doppio clic sulla regola da modificare.

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
<td><p>Consente di visualizzare una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire un testo aggiuntivo da associare a una regola di conversione. Questa descrizione può essere utilizzata per aiutare gli amministratori a identificare con facilità lo scopo della regola.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, verrebbe visualizzata prima di effettuare modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco della regola di conversione da modificare. L'identità è costituita dall'ambito seguito da un nome univoco per ogni ambito. Ad esempio:</p>
<p>-Identity &quot;site:Redmond/OutboundRule1&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>Pattern</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Espressione regolare che rappresenta il formato del numero a cui la conversione verrà applicata.</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Priorità assegnata alla regola. Se un numero corrisponde al formato di più regole di conversione in uscita, le regole vengono applicate in ordine di priorità. Le regole vengono elaborate in base alla priorità assegnata, ovvero la prima regola ad essere elaborata ha la priorità 0, la seconda ha la priorità 1 e così via.</p></td>
</tr>
<tr class="even">
<td><p><em>Translation</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Espressione regolare che verrà applicata al numero corrispondente al formato per preparare tale numero per il routing in uscita.</p></td>
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

Il cmdlet **Set-CsOutboundCallingNumberTranslationRule** accetta istanze da pipeline dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.CallingNumberTranslationRule\#Decorated.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsOutboundCallingNumberTranslationRule** modifica piuttosto le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.CallingNumberTranslationRule\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsOutboundCallingNumberTranslationRule](get-csoutboundcallingnumbertranslationrule.md)  
[New-CsOutboundCallingNumberTranslationRule](new-csoutboundcallingnumbertranslationrule.md)  
[Remove-CsOutboundCallingNumberTranslationRule](remove-csoutboundcallingnumbertranslationrule.md)

