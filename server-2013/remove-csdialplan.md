---
title: Remove-CsDialPlan
TOCTitle: Remove-CsDialPlan
ms:assetid: 99845b82-1730-494a-8f47-2dec5ef177c1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398791(v=OCS.15)
ms:contentKeyID: 49301417
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsDialPlan

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove il dial plan specificato. Questo cmdlet può essere utilizzato anche per rimuovere il dial plan globale. Se si rimuove il dial plan globale, questo però non viene effettivamente rimosso. In realtà, le impostazioni vengono semplicemente riconfigurate sui rispettivi valori predefiniti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsDialPlan -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene utilizzato il cmdlet **Remove-CsDialPlan** per eliminare il dial plan per utente con identità (Identity) RedmondDialPlan. Si noti che quando si elimina un dial plan, non è necessario assegnare un nuovo dial plan agli utenti in precedenza assegnati al dial plan eliminato. Questi utenti utilizzeranno il dial plan assegnato al relativo servizio o sito oppure il dial plan globale.

    Remove-CsDialPlan -Identity RedmondDialPlan

## ESEMPIO 2

Con l'esempio 2 vengono eliminati tutti i dial plan che includono la parola Redmond nella descrizione. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsDialPlan** per restituire una raccolta di tutti i dial plan configurati per l'utilizzo nell'organizzazione. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che applica un filtro per circoscrivere i dati restituiti limitandoli ai profili che includono la parola Redmond nella descrizione. Successivamente, la raccolta filtrata viene passata al cmdlet **Remove-CsDialPlan**, che procede all'eliminazione di tutti i dial plan della raccolta.

    Get-CsDialPlan | Where-Object {$_.Description -match "Redmond"} | Remove-CsDialPlan

## Descrizione dettagliata

Questo cmdlet consente di rimuovere un dial plan esistente (detto anche profilo di numerazione locale). I dial plan forniscono informazioni necessarie per consentire agli utenti di VoIP aziendale di effettuare telefonate. I dial plan sono utilizzati anche da applicazione Operatore Conferenza per le conferenze telefoniche con accesso esterno. Un dial plan determina le regole di normalizzazione applicate e se è necessario comporre un prefisso per le chiamate esterne.

Nota: La rimozione di un dial plan comporta anche la rimozione di eventuali regole di normalizzazione associate. Se viene rimosso il dial plan globale vengono rimosse anche eventuali regole di normalizzazione associate, ma viene creata una regola di normalizzazione globale predefinita.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Remove-CsDialPlan** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsDialPlan"}

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
<td><p>L'identificatore univoco del dial plan che si desidera rimuovere.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile. Il cmdlet **Remove-CsDialPlan** accetta l'input da pipeline di oggetti dial plan.

## Tipi restituiti

Il cmdlet rimuove le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile.

## Vedere anche

#### Ulteriori risorse

[New-CsDialPlan](new-csdialplan.md)  
[Set-CsDialPlan](set-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Grant-CsDialPlan](grant-csdialplan.md)  
[Test-CsDialPlan](test-csdialplan.md)  
[Remove-CsVoiceNormalizationRule](remove-csvoicenormalizationrule.md)  
[Get-CsVoiceNormalizationRule](get-csvoicenormalizationrule.md)

