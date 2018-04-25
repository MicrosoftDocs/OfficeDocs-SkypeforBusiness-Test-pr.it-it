---
title: Remove-CsOutboundTranslationRule
TOCTitle: Remove-CsOutboundTranslationRule
ms:assetid: 73e0bd0d-2458-464a-9e6e-1868143aadc8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398556(v=OCS.15)
ms:contentKeyID: 49300980
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsOutboundTranslationRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una regola di conversione in uscita esistente. Una regola di conversione in uscita converte i numeri di telefono nel formato di composizione locale per agevolare l'interazione con i sistemi PBX (Private Branch Exchange). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsOutboundTranslationRule -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Questo esempio consente di rimuovere una regola di conversione in uscita esistente per il sito Redmond denominata Prefix Redmond. Le identità sono univoche, per cui questo comando eliminerà una sola regola.

    Remove-CsOutboundTranslationRule -Identity "site:Redmond/Prefix Redmond"

## ESEMPIO 2

In questo esempio vengono rimosse tutte le regole di conversione in uscita a livello di sito. La prima parte del comando prevede una chiamata al cmdlet **Get-CsOutboundTranslationRule** con un valore di filtro site:\* che restituisce una raccolta di tutte le regole la cui identità (Identity) inizia con site:. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsOutboundTranslationRule**, che rimuove ogni singola regola della raccolta.

    Get-CsOutboundTranslationRule -Filter site:* | Remove-CsOutboundTranslationRule

## Descrizione dettagliata

Chiamare questo cmdlet per rimuovere una regola di conversione in uscita esistente. Lync Server normalizza i numeri di telefono nel formato E.164. Molti sistemi PBX non sono tuttavia in grado di utilizzare questo formato. Le regole di conversione in uscita convertono il numero nel formato di composizione locale prima di inviarlo al Mediation Server o al gateway.

Ciascuna regola di conversione in uscita è associata a una configurazione trunk. Ciò significa che l'utilizzo di questo cmdlet per rimuovere una regola comporterà la rimozione di questa regola dalla configurazione trunk dell'ambito corrispondente.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Remove-CsOutboundTranslationRule** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsOutboundTranslationRule"}

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
<td><p>L'identificatore univoco della regola di conversione in uscita che si desidera rimuovere. L'identità è costituita dall'ambito seguito da un nome che deve essere univoco all'interno di ciascun ambito. Ad esempio, site:Redmond/OutboundRule1.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule. Accetta input tramite pipeline di oggetti regola di conversione in uscita.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Consente di rimuovere un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule.

## Vedere anche

#### Ulteriori risorse

[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)  
[Set-CsOutboundTranslationRule](set-csoutboundtranslationrule.md)  
[Get-CsOutboundTranslationRule](get-csoutboundtranslationrule.md)

