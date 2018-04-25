---
title: New-CsRoutingConfiguration
TOCTitle: New-CsRoutingConfiguration
ms:assetid: ead67e35-b145-4041-ba3e-4b26c47cce1d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399056(v=OCS.15)
ms:contentKeyID: 49302342
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRoutingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Questo cmdlet restituisce un oggetto contenente le impostazioni predefinite per un oggetto di configurazione di routing. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsRoutingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableLocationBasedRouting <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Route <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Questo comando crea un oggetto che contiene i valori di configurazione di routing predefiniti e assegna tale oggetto alla variabile $x. Qualsiasi altro utilizzo di questo cmdlet restituirà un errore.

    $x = New-CsRoutingConfiguration -Identity global -InMemory

## Descrizione dettagliata

Una configurazione di routing è un contenitore di tutte le route vocali definite all'interno di una distribuzione di Lync Server. Per creare una nuova route vocale, utilizzare il cmdlet **New-CsVoiceRoute**.

Una configurazione di routing può essere definita solo a livello globale. Inoltre, non è possibile denominare singolarmente le configurazioni di routing; è disponibile solo un elenco di route vocali per l'intera distribuzione di Lync Server. Nell'implementazione Lync Server di Windows PowerShell, se si tenta di creare un oggetto già esistente chiamando un cmdlet che inizia con il verbo New, verrà restituito un messaggio di errore. Ogni implementazione di Lync Server include un oggetto di configurazione di routing predefinito con valore Identity Global. Ciò significa che l'unico elenco di route vocali che potrebbe essere creato, esiste già. Di conseguenza, una chiamata al cmdlet **New-CsRoutingConfiguration** restituirà sempre un messaggio di errore e non creerà una nuova configurazione di routing.

La sola eccezione si presenta quando si specifica il parametro InMemory durante la chiamata del cmdlet. Questo comando creerà un oggetto solo in memoria che contiene un elenco predefinito di route vocali.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsRoutingConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRoutingConfiguration"}

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
<td><p>L'ambito della configurazione di routing. Questo valore deve essere Global.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableLocationBasedRouting</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se l'impostazione è True, il routing vocale verrà gestito tenendo conto della posizione sia dell'utente che effettua la chiamata che dell'utente che la riceve. Il valore predefinito è False.</p></td>
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
<td><p><em>Route</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Un elenco di tutte le route vocali (oggetti Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route) definite per la distribuzione di Lync Server.</p>
<p>È possibile creare oggetti route vocali utilizzando il cmdlet <strong>New-CsVoiceRoute</strong>. Questo è il metodo consigliato per l'aggiunta di route vocali in questo elenco.</p></td>
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

È in grado di creare un oggetto in memoria di tipo Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnRoutingSettings.

## Vedere anche

#### Ulteriori risorse

[Remove-CsRoutingConfiguration](remove-csroutingconfiguration.md)  
[Set-CsRoutingConfiguration](set-csroutingconfiguration.md)  
[Get-CsRoutingConfiguration](get-csroutingconfiguration.md)  
[New-CsVoiceRoute](new-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)

