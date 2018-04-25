---
title: Remove-CsVoiceRoute
TOCTitle: Remove-CsVoiceRoute
ms:assetid: 6687e538-e8f6-4bf0-b393-2c7b4a3f2f06
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398468(v=OCS.15)
ms:contentKeyID: 49300813
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsVoiceRoute

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una route vocale. Le route vocali contengono istruzioni che comunicano a Lync Server come instradare le chiamate effettuate da utenti di VoIP aziendale ai numeri di telefono della rete PSTN (Public Switched Telephone Network) o di un centralino (PBX, Private Branch Exchange). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsVoiceRoute -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Consente di rimuovere le impostazioni per la route vocale con identità Route1.

    Remove-CsVoiceRoute -Identity Route1

## ESEMPIO 2

Questo comando rimuove tutte le route vocali dall'organizzazione. Vengono innanzitutto recuperate tutte le route vocali dal cmdlet **Get-CsVoiceRoute**. Queste route vocali vengono quindi inviate tramite pipe al cmdlet **Remove-CsVoiceRoute**, che rimuove ogni route.

    Get-CsVoiceRoute | Remove-CsVoiceRoute

## ESEMPIO 3

Questo comando rimuove tutte le route vocali la cui identità include la stringa "Redmond". Viene chiamato innanzitutto il cmdlet **Get-CsVoiceRoute** con il parametro Filter. Il valore del parametro Filter è la stringa Redmond racchiusa tra caratteri jolly (\*), che specificano che la stringa può trovarsi in qualunque posizione all'interno del valore di Identity. Dopo che sono state recuperate tutte le route vocali la cui identità include la stringa Redmond, queste route vocali vengono inviate tramite pipe al cmdlet **Remove-CsVoiceRoute**, che rimuove ogni route.

    Get-CsVoiceRoute -Filter *Redmond* | Remove-CsVoiceRoute

## Descrizione dettagliata

Utilizzare questo cmdlet per rimuovere una route vocale esistente. Le route vocali sono associate ai criteri vocali per mezzo degli utilizzi PSTN, pertanto la rimozione di una route vocale non provoca cambiamenti nei valori relativi a un criterio vocale; modifica semplicemente il routing per i numeri corrispondenti al modello della route vocale eliminata.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Remove-CsVoiceRoute** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsVoiceRoute"}

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
<td><p>Una stringa che identifica in modo univoco la route vocale da eliminare. Se il nome della route contiene uno spazio, come nel caso di Test Route, è necessario racchiudere l'intera stringa tra virgolette doppie.</p>
<p></p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route. Consente di accettare l'input da pipeline di oggetti route vocale.

## Tipi restituiti

Consente di rimuovere un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route.

## Vedere anche

#### Ulteriori risorse

[New-CsVoiceRoute](new-csvoiceroute.md)  
[Set-CsVoiceRoute](set-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)  
[Test-CsVoiceRoute](test-csvoiceroute.md)

