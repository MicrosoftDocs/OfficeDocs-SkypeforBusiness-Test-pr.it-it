---
title: Remove-CsCallParkOrbit
TOCTitle: Remove-CsCallParkOrbit
ms:assetid: b8e7c236-f8de-45bd-966b-60c815b37aed
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412901(v=OCS.15)
ms:contentKeyID: 49301780
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCallParkOrbit

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove uno specifico intervallo di codici orbit del parcheggio di chiamata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsCallParkOrbit -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio il cmdlet **Remove-CsCallParkOrbit** viene utilizzato per eliminare l'intervallo di codici orbit del parcheggio di chiamata denominato Redmond CPO 1.

    Remove-CsCallParkOrbit -Identity "Redmond CPO 1"

## ESEMPIO 2

Il comando riportato in questo esempio rimuove tutti gli intervalli degli orbit del parcheggio di chiamata definiti per un'organizzazione. Il comando chiama innanzitutto il cmdlet **Get-CsCallParkOrbit** senza parametri per recuperare tutti gli intervalli degli orbit del parcheggio di chiamata definiti. La raccolta di intervalli degli orbit del parcheggio di chiamata viene quindi inviata tramite pipe al cmdlet **Remove-CsCallParkOrbit**, che rimuove tutti gli orbit del parcheggio di chiamata.

    Get-CsCallParkOrbit | Remove-CsCallParkOrbit

## ESEMPIO 3

Il comando rimuove tutti gli intervalli di codici orbit del parcheggio di chiamata con valore Identity che include la stringa "Redmond", ad esempio "Redmond 501", "CP Redmond 1" e "ARedmond". Il comando chiama innanzitutto il cmdlet **Get-CsCallParkOrbit** con il parametro Filter per recuperare tutti gli intervalli di codici orbit del parcheggio di chiamata con valore Identity contenente la stringa Redmond. La raccolta viene inviata tramite pipe al cmdlet **Remove-CsCallParkOrbit**, che rimuove tutti gli elementi della raccolta.

    Get-CsCallParkOrbit -Filter *Redmond* | Remove-CsCallParkOrbit

## Descrizione dettagliata

Il cmdlet **Remove-CsCallParkOrbit** elimina l'intervallo dell'orbit del parcheggio di chiamata il cui nome è stato passato al parametro obbligatorio Identity. Ogni orbit del parcheggio di chiamata all'interno dell'organizzazione deve avere un intervallo di numeri univoco. La rimozione di un orbit del parcheggio di chiamata consente di liberare l'intervallo contenuto nell'orbit del parcheggio di chiamata. I numeri disponibili possono essere utilizzati in un nuovo orbit del parcheggio di chiamata definito.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsCallParkOrbit** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCallParkOrbit"}

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
<td><p>Il nome dell'intervallo dell'orbit del parcheggio di chiamata. Questo nome è stato assegnato dall'amministratore durante la definizione dell'intervallo dell'orbit del parcheggio di chiamata.</p></td>
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
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
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

Oggetto Microsoft.Rtc.Management.Voice.Helpers.DisplayCallParkOrbit. Accetta l'input da pipeline di oggetti orbit del parcheggio di chiamata.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Rimuove un oggetto di tipo Microsoft.Rtc.Management.Voice.Helpers.DisplayCallParkOrbit.

## Vedere anche

#### Ulteriori risorse

[New-CsCallParkOrbit](new-cscallparkorbit.md)  
[Set-CsCallParkOrbit](set-cscallparkorbit.md)  
[Get-CsCallParkOrbit](get-cscallparkorbit.md)

