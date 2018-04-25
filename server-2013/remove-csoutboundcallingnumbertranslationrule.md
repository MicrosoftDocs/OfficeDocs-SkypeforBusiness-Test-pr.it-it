---
title: Remove-CsOutboundCallingNumberTranslationRule
TOCTitle: Remove-CsOutboundCallingNumberTranslationRule
ms:assetid: 41ca92c9-7c2e-44e0-8ec8-9f39843b73e7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204836(v=OCS.15)
ms:contentKeyID: 49300330
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsOutboundCallingNumberTranslationRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una regola di conversione dei numeri delle chiamate in uscita esistente. Una regola di questo tipo converte i numeri di telefono E.164 utilizzati da Lync Server 2013 in un formato utilizzabile dai peer di trunking che non supportano tali numeri. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsOutboundCallingNumberTranslationRule -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 rimuove la regola di conversione dei numeri in uscita con identità (Identity) site:Redmond/SevenDigit.

    Remove-CsOutboundCallingNumberTranslationRule -Identity "site:Redmond/SevenDigit"

## Esempio 2

Nell'esempio 2 vengono rimosse tutte le regole di conversione dei numeri delle chiamate in uscita configurate per il sito Redmond. A tale scopo, il comando chiama il cmdlet **Remove-CsOutboundCallingNumberTranslationRule** con il parametro Identity. Il valore di parametro "site:Redmond" garantisce che vengano rimosse tutte le regole di conversione configurate per il sito Redmond.

    Remove-CsOutboundCallingNumberTranslationRule -Identity "site:Redmond"

## Esempio 3

Nell'esempio 3 vengono eliminate tutte le regole di conversione dei numeri delle chiamate in uscita che utilizzano il formato (Pattern) "^\\+1425(\\d{7})$". A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsOutboundCallingNumberTranslationRule** per restituire una raccolta di tutte le regole di conversione utilizzate nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet Where-Object, che seleziona solo le regole in cui la proprietà Pattern è uguale a "^\\+1425(\\d{7})$". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsOutboundCallingNumberTranslationRule**, che elimina ogni regola della raccolta.

    Get-CsOutboundCallingNumberTranslationRule | Where-Object {$_.Pattern -eq '^\+1425(\d{7})$'} | Remove-CsOutboundCallingNumberTranslationRule

## Descrizione dettagliata

Le regole di conversione dei numeri delle chiamate in uscita convertono i numeri di telefono E.164 utilizzati da Lync 2013 in un formato utilizzabile dai peer di trunking che non supportano i numeri E.164. Quando si crea una regola di conversione, si specifica un'espressione regolare che rappresenta il numero E.164 in uscita (il formato o Pattern) e un'espressione regolare che rappresenta il numero convertito (la conversione o Translation).

Le regole di conversione dei numeri in uscita devono essere associate a una raccolta di impostazioni di configurazione trunk. Quando si crea una nuova regola di conversione, è necessario specificare sia l'identità delle impostazioni di configurazione del trunking che il nome della nuova regola, ad esempio site:Redmond/RedmondTranslationRule. Si noti che le impostazioni di configurazione del trunking non devono necessariamente essere già presenti quando si crea una nuova regola. Si supponga ad esempio di creare la regola site:Redmond/RedmondTranslationRule e che non siano state create impostazioni di configurazione trunk per il sito Redmond. Se Redmond è un sito valido, le impostazioni di configurazione trunk verranno create automaticamente per il sito e la nuova regola di conversione verrà assegnata a tale raccolta di impostazioni. Il comando tuttavia avrà esito negativo se il sito Redmond non esiste.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsOutboundCallingNumberTranslationRule"}

**Pannello di controllo di Lync Server:** per rimuovere una regola di conversione dei numeri in uscita utilizzando il Pannello di controllo di Lync Server, fare clic su Routing vocale e quindi su Configurazione trunk. Fare doppio clic sull'elemento appropriato nella colonna Nome e quindi nella finestra di dialogo Modifica configurazione trunk scorrere fino alla sezione Regole di conversione per il numero del chiamante. Selezionare la regola da eliminare e quindi fare clic su Rimuovi.

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
<td><p>Identificatore univoco della regola di conversione in uscita che si desidera rimuovere. L'identità è costituita dall'ambito seguito da un nome univoco per ogni ambito, ad esempio:</p>
<p>-Identity &quot;site:Redmond/OutboundRule1&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Remove-CsOutboundCallingNumberTranslationRule** accetta le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.CallingNumberTranslationRule\#Decorated inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsOutboundCallingNumberTranslationRule** invece elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.CallingNumberTranslationRule\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsOutboundCallingNumberTranslationRule](get-csoutboundcallingnumbertranslationrule.md)  
[New-CsOutboundCallingNumberTranslationRule](new-csoutboundcallingnumbertranslationrule.md)  
[Set-CsOutboundCallingNumberTranslationRule](set-csoutboundcallingnumbertranslationrule.md)

