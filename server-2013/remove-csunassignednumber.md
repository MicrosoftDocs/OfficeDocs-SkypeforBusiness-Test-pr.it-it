---
title: Remove-CsUnassignedNumber
TOCTitle: Remove-CsUnassignedNumber
ms:assetid: 13095593-92d3-4790-99a5-5df4610652cb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398209(v=OCS.15)
ms:contentKeyID: 49299751
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsUnassignedNumber

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un intervallo esistente di numeri non assegnati e le regole di routing applicate a tali numeri. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsUnassignedNumber -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio vengono rimosse le impostazioni dei numeri non assegnati con Identity UNSet1.

    Remove-CsUnassignedNumber -Identity UNSet1

## ESEMPIO 2

Nell'esempio 2 vengono rimosse tutte le impostazioni di numeri non assegnati in cui il nome dell'annuncio assegnato contiene la stringa Welcome. Il comando chiama innanzitutto il cmdlet **Get-CsUnassignedNumber**, che restituisce una raccolta di tutte le impostazioni di numeri non assegnati. La raccolta viene quindi passata al cmdlet **Where-Object**, che circoscrive la raccolta solo alle impostazioni di numeri non assegnati in cui AnnouncementName include (-match) la stringa Welcome. La raccolta circoscritta infine viene passata al cmdlet **Remove-CsUnassignedNumber**, che rimuove tutti i dati rimasti nella raccolta.

    Get-CsUnassignedNumber | Where-Object {$_.AnnouncementName -match "Welcome"} | Remove-CsUnassignedNumber

## Descrizione dettagliata

I numeri non assegnati sono numeri di telefono che sono stati assegnati a un'organizzazione ma non a utenti o telefoni specifici. È possibile configurare Lync Server in modo da instradare le chiamate a destinazioni appropriate quando viene chiamato un numero non assegnato. Questo cmdlet rimuove le impostazioni che definiscono tale routing.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsUnassignedNumber** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsUnassignedNumber"}

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
<td><p>Il nome univoco per l'intervallo di numeri non assegnati da rimuovere.</p></td>
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

Oggetto Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange. Accetta l'input da pipeline di oggetti numero non assegnato.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Rimuove un oggetto di tipo Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange.

## Vedere anche

#### Ulteriori risorse

[New-CsUnassignedNumber](new-csunassignednumber.md)  
[Set-CsUnassignedNumber](set-csunassignednumber.md)  
[Get-CsUnassignedNumber](get-csunassignednumber.md)  
[Get-CsAnnouncement](get-csannouncement.md)  
[Get-CsExUmContact](get-csexumcontact.md)

