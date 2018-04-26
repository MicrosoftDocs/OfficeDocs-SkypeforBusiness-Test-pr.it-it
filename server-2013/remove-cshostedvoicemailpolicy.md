---
title: Remove-CsHostedVoicemailPolicy
TOCTitle: Remove-CsHostedVoicemailPolicy
ms:assetid: 13968bbe-1403-46de-b02a-ed61e712d1b3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398211(v=OCS.15)
ms:contentKeyID: 49299758
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsHostedVoicemailPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un criterio di segreteria telefonica ospitata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsHostedVoicemailPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con questo comando viene rimosso il criterio di segreteria telefonica ospitata per il criterio per utente ExRedmond.

    Remove-CsHostedVoicemailPolicy -Identity ExRedmond

## ESEMPIO 2

Il comando riportato nell'esempio 2 rimuove tutti i criteri di segreteria telefonica ospitata per utente. Il comando inizia con una chiamata al cmdlet **Get-CsHostedVoicemailPolicy** con il filtro tag\*, che recupera tutti i criteri definiti come criteri per utente. Il set di criteri viene quindi inviato tramite pipe al cmdlet **Remove-CsHostedVoicemailPolicy**, che elimina ogni criterio.

    Get-CsHostedVoicemailPolicy -Filter tag* | Remove-CsHostedVoicemailPolicy

## Descrizione dettagliata

Questo cmdlet consente di rimuovere un criterio che specifica come instradare le chiamate senza risposta a un utente a un servizio Messaggistica unificata di Exchange ospitato.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Remove-CsHostedVoicemailPolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsHostedVoicemailPolicy"}

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
<td><p>Un identificatore univoco per il criterio di segreteria telefonica ospitata che si desidera rimuovere. Questo identificatore include l'ambito (nel caso di un ambito globale), l'ambito e il sito (per un criterio di sito, come site:Redmond) oppure il nome del criterio (nel caso di un criterio per utente, come HVUserPolicy).</p></td>
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
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Skype for Business online per il criterio di segreteria telefonica ospitata da eliminare. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.HostedVoicemailPolicy. Consente di accettare l'input da pipeline di oggetti criterio di segreteria telefonica ospitata.

## Tipi restituiti

Questo cmdlet non restituisce un oggetto. Consente di rimuovere un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Policy.Voice.HostedVoicemailPolicy.

## Vedere anche

#### Ulteriori risorse

[New-CsHostedVoicemailPolicy](new-cshostedvoicemailpolicy.md)  
[Set-CsHostedVoicemailPolicy](set-cshostedvoicemailpolicy.md)  
[Get-CsHostedVoicemailPolicy](get-cshostedvoicemailpolicy.md)  
[Grant-CsHostedVoicemailPolicy](grant-cshostedvoicemailpolicy.md)

