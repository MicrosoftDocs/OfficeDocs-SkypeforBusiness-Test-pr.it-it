---
title: New-CsOutboundCallingNumberTranslationRule
TOCTitle: New-CsOutboundCallingNumberTranslationRule
ms:assetid: 959591bb-4a6b-4b7f-9666-da1fa0f9cd43
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205097(v=OCS.15)
ms:contentKeyID: 49301390
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsOutboundCallingNumberTranslationRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova regola di conversione dei numeri in uscita. Una regola di questo tipo converte i numeri di telefono E.164 utilizzati da Lync Server 2013 in un formato utilizzabile dai peer di trunking che non supportano tali numeri. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    New-CsOutboundCallingNumberTranslationRule -Name <String> -Parent <String> <COMMON PARAMETERS>

    New-CsOutboundCallingNumberTranslationRule -Identity <XdsIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Pattern <String>] [-Priority <Int32>] [-Translation <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 crea una nuova regola di conversione dei numeri chiamanti in uscita che converte un numero E.164 che inizia con il valore stringa +1206 (ad esempio, +12065551219) in un valore a sette cifre (ad esempio, 5551219, eliminando +1206).

    New-CsOutboundCallingNumberTranslationRule -Parent "site:Redmond" -Name SevenDigit -Description "Converts a dialed number to seven digits" -Pattern '^\+1206(\d{7})$' -Translation '$1'

## Descrizione dettagliata

Le regole di conversione dei numeri in uscita convertono i numeri di telefono E.164 utilizzati da Lync 2013 in un formato utilizzabile dai peer di trunking che non supportano i numeri E.164. Quando si crea una regola di conversione, si fornisce un'espressione regolare che rappresenta il numero E.164 in uscita (formato) e un'espressione regolare che rappresenta il numero convertito (conversione).

Le regole di conversione dei numeri in uscita devono essere associate a una raccolta di impostazioni di configurazione trunk. Quando si crea una nuova regola di conversione, è necessario specificare sia l'identità delle impostazioni di configurazione del trunking che il nome della nuova regola, ad esempio site:Redmond/RedmondTranslationRule. Si noti che le impostazioni di configurazione del trunking non devono necessariamente essere già presenti quando si crea una nuova regola. Si supponga ad esempio di creare la regola site:Redmond/RedmondTranslationRule e che non siano state create impostazioni di configurazione trunk per il sito Redmond. Se Redmond è un sito valido, le impostazioni di configurazione trunk verranno create automaticamente per il sito e la nuova regola di conversione verrà assegnata a tale raccolta di impostazioni. Il comando tuttavia avrà esito negativo se il sito Redmond non esiste.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsOutboundCallingNumberTranslationRule"}

**Pannello di controllo di Lync Server:** per creare una nuova regola di conversione dei numeri chiamanti in uscita utilizzando il Pannello di controllo di Lync Server, fare clic su Routing vocale, su Configurazione trunk e quindi fare doppio clic sull'elemento appropriato nella colonna Nome. Nella finestra di dialogo Modifica configurazione trunk scorrere verso il basso fino alla sezione Regole di conversione per il numero del chiamante e quindi fare clic su Nuovo.

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
<td><p>Identificatore univoco della nuova regola di conversione. I nomi sono costituiti dall'ambito (padre), da un carattere &quot;/&quot; e da un nome univoco all'interno di tale ambito. Ad esempio, una regola denominata RedmondDialing creata per il sito Redmond avrà un'identità simile alla seguente:</p>
<p>-Identity &quot;site:Redmond/RedmondDialing&quot;</p>
<p>Se si utilizza il parametro Identity, il comando non potrà includere il parametro Parent o Name.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome della nuova regola di conversione (i nomi devono essere univoci per l'ambito in questione). Ad esempio:</p>
<p>-Name &quot;RedmondDialing&quot;</p>
<p>Ogni volta che si utilizza il parametro Name, è necessario utilizzare anche il parametro Parent. Non è possibile utilizzare il parametro Name nello stesso comando del parametro Identity.</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Ambito in cui verrà configurata la nuova regola di conversione. Per configurare una regola nell'ambito globale, utilizzare la sintassi seguente:</p>
<p>-Parent &quot;global&quot;</p>
<p>Per configurare una regola nell'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Parent &quot;site:Redmond&quot;</p>
<p>Per configurare una regola nell'ambito del servizio (solo per il servizio PstnGateway), utilizzare una sintassi simile alla seguente:</p>
<p>-Parent &quot;service:PstnGateway:192.168.0.100&quot;</p>
<p>Ogni volta che si utilizza il parametro Parent, è necessario utilizzare anche il parametro Name. Non è possibile utilizzare il parametro Parent nello stesso comando del parametro Identity.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire un testo aggiuntivo da associare a una regola di conversione. Questa descrizione può essere utilizzata per aiutare gli amministratori a identificare con facilità lo scopo della regola.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, verrebbe visualizzata prima dell'esecuzione di modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>Pattern</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Espressione regolare che rappresenta il formato del numero a cui verrà applicata la conversione.</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Priorità assegnata alla regola. Se un numero corrisponde al formato di più regole di conversione in uscita, le regole vengono applicate in ordine di priorità. Le regole vengono elaborate in base alla priorità loro assegnata, ovvero la prima regola a essere elaborata ha la priorità 0, la seconda ha la priorità 1 e così via.</p></td>
</tr>
<tr class="even">
<td><p><em>Translation</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Espressione regolare che verrà applicata al numero corrispondente al formato per preparare tale numero per le chiamate in uscita.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsOutboundCallingNumberTranslationRule** non accetta dati inviati tramite pipeline.

## Tipi restituiti

Il cmdlet **New-CsOutboundCallingNumberTranslationRule** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.CallingNumberTranslationRule\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsOutboundCallingNumberTranslationRule](get-csoutboundcallingnumbertranslationrule.md)  
[Remove-CsOutboundCallingNumberTranslationRule](remove-csoutboundcallingnumbertranslationrule.md)  
[Set-CsOutboundCallingNumberTranslationRule](set-csoutboundcallingnumbertranslationrule.md)

