---
title: Get-CsOutboundCallingNumberTranslationRule
TOCTitle: Get-CsOutboundCallingNumberTranslationRule
ms:assetid: 65589388-f935-4d25-ae74-362be97c8597
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204962(v=OCS.15)
ms:contentKeyID: 49300795
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsOutboundCallingNumberTranslationRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle regole di conversione dei numeri in uscita create per l'utilizzo nell'organizzazione. Una regola di questo tipo converte i numeri di telefono E.164 utilizzati da Lync Server 2013 in un formato utilizzabile dai peer di trunking che non supportano tali numeri. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsOutboundCallingNumberTranslationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsOutboundCallingNumberTranslationRule [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce informazioni su tutte le regole di conversione dei numeri in uscita configurate per l'utilizzo nell'organizzazione.

    Get-CsOutboundCallingNumberTranslationRule

## Esempio 2

Nell'esempio 2 vengono restituite informazioni solo sulla regola di conversione dei numeri in uscita con identità (Identity) "site:Redmond/SevenDigit".

    Get-CsOutboundCallingNumberTranslationRule -Identity "site:Redmond/SevenDigit"

## Esempio 3

Nell'esempio 3 vengono restituite informazioni su tutte le regole di conversione dei numeri in uscita configurate per il sito Redmond. Per ottenere questo risultato, il valore del parametro Identity viene impostato sull'identità del sito Redmond (site:Redmond).

    Get-CsOutboundCallingNumberTranslationRule -Identity "site:Redmond"

## Esempio 4

Il comando riportato nell'esempio 4 restituisce informazioni solo sulle regole di conversione dei numeri in uscita incluse nel sito Redmond e con Priority uguale 0. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsOutboundCallingNumberTranslationRule** e il parametro Identity per restituire una raccolta di tutte le regole di conversione assegnate al sito Redmond. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le regole con Priority uguale a 0.

    Get-CsOutboundCallingNumberTranslationRule -Identity "site:Redmond" | Where-Object {$_.Priority -eq 0}

## Descrizione dettagliata

Le regole di conversione dei numeri in uscita convertono i numeri di telefono E.164 utilizzati da Lync 2013 in un formato utilizzabile dai peer di trunking che non supportano i numeri E.164. Quando si crea una regola di conversione, si fornisce un'espressione regolare che rappresenta il numero E.164 in uscita (formato) e un'espressione regolare che rappresenta il numero convertito (conversione).

Le regole di conversione dei numeri in uscita devono essere associate a una raccolta di impostazioni di configurazione trunk. Quando si crea una nuova regola di conversione, è necessario specificare sia l'identità delle impostazioni di configurazione del trunking che il nome della nuova regola, ad esempio site:Redmond/RedmondTranslationRule. Si noti che le impostazioni di configurazione del trunking non devono necessariamente essere già presenti quando si crea una nuova regola. Si supponga ad esempio di creare la regola site:Redmond/RedmondTranslationRule e che non siano state create impostazioni di configurazione trunk per il sito Redmond. Se Redmond è un sito valido, le impostazioni di configurazione trunk verranno create automaticamente per il sito e la nuova regola di conversione verrà assegnata a tale raccolta di impostazioni. Il comando tuttavia avrà esito negativo se il sito Redmond non esiste.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli del controllo di accesso basato sui ruoli creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsOutboundCallingNumberTranslationRule"}

**Pannello di controllo di Lync Server:** per visualizzare le regole di conversione dei numeri in uscita nel Pannello di controllo di Lync Server, fare clic su Routing vocale e quindi su Configurazione trunk. Fare doppio clic sulla voce appropriata nella colonna Nome e quindi nella finestra di dialogo Modifica configurazione trunk scorrere fino alla sezione Regole di conversione per il numero del chiamante.

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Esegue una ricerca con caratteri jolly che consente di restituire solo le regole di conversione dei numeri in uscita le cui identità corrispondono alla stringa con caratteri jolly. La sintassi seguente ad esempio restituisce tutte le regole di conversione che includono il valore stringa &quot;Redmond&quot;:</p>
<p>-Filter &quot;*Redmond*&quot;</p>
<p>Per restituire tutte le regole di conversione configurate nell'ambito del sito, utilizzare la sintassi seguente:</p>
<p>-Filter &quot;site:*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco della regola di conversione dei numeri in uscita che si desidera recuperare. L'identità è costituita dall'ambito seguito da un nome univoco per ogni ambito, ad esempio:</p>
<p>-Identity &quot;site:Redmond/OutboundRule1&quot;</p>
<p>Per restituire tutte le regole di conversione configurate per un ambito specifico (ad esempio il sito Redmond), è sufficiente impostare il parametro Identity sul valore dell'ambito stesso:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>Se non vengono specificati né il parametro Identity né il parametro Filter, il cmdlet <strong>Get-CsOutboundCallingNumberTranslationRule</strong> restituisce informazioni su tutte le regole di conversione dei numeri in uscita.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati delle regole di conversione dei numeri in uscita dalla replica locale dell'archivio di gestione centrale anziché direttamente dall'archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsOutboundCallingNumberTranslationRule** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsOutboundCallingNumberTranslationRule** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.CallingNumberTranslationRule\#Decorated.

## Vedere anche

#### Ulteriori risorse

[New-CsOutboundCallingNumberTranslationRule](new-csoutboundcallingnumbertranslationrule.md)  
[Remove-CsOutboundCallingNumberTranslationRule](remove-csoutboundcallingnumbertranslationrule.md)  
[Set-CsOutboundCallingNumberTranslationRule](set-csoutboundcallingnumbertranslationrule.md)

