---
title: Remove-CsVoicePolicy
TOCTitle: Remove-CsVoicePolicy
ms:assetid: 4d3e67be-c094-415f-b1e6-0719dec6f3fc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398309(v=OCS.15)
ms:contentKeyID: 49300495
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsVoicePolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove il criterio vocale specificato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsVoicePolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio vengono rimosse le impostazioni del criterio vocale per utente UserVoicePolicy1.

    Remove-CsVoicePolicy -Identity UserVoicePolicy1

## ESEMPIO 2

In questo esempio vengono rimosse tutte le impostazioni dei criteri vocali che possono essere assegnate a utenti specifici. Il comando utilizza il cmdlet **Get-CsVoicePolicy** con il valore tag\* per il parametro Filter in modo da ottenere tutti i criteri vocali per utente. La raccolta di criteri viene quindi inviata tramite pipe al cmdlet **Remove-CsVoicePolicy** per la rimozione.

    Get-CsVoicePolicy -Filter tag* | Remove-CsVoicePolicy

## Descrizione dettagliata

Questo cmdlet consente di rimuovere un criterio vocale esistente. I criteri vocali sono utilizzati per gestire le funzionalità di VoIP aziendale, ad esempio lo squillo simultaneo (vale a dire la capacità di far squillare un secondo telefono ogni volta che si riceve una chiamata sul telefono dell'ufficio) e l'inoltro di chiamata. Questo cmdlet può essere utilizzato anche per rimuovere il criterio vocale globale. In questo caso, però, i criteri non vengono effettivamente rimossi, ma per tutte le proprietà dei criteri verranno ripristinati i valori predefiniti.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsVoicePolicy** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsVoicePolicy"}

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
<td><p>Un identificatore univoco che specifica l'ambito e, in alcuni casi il nome, del criterio da rimuovere.</p></td>
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
<td><p>Elimina qualsiasi richiesta di conferma che altrimenti verrebbe visualizzata prima di apportare modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Office 365 per il criterio vocale da eliminare, ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Se si usa una sessione remota di Windows PowerShell e si è connessi solo a Skype for Business online non è necessario includere il parametro Tenant. L'ID del tenant verrà infatti compilato automaticamente in base alle informazioni di connessione. Il parametro Tenant è destinato principalmente all'uso in ambienti ibridi.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoicePolicy. Accetta input tramite pipeline da oggetti criterio vocale.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Consente di rimuovere un'istanza di un oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoicePolicy.

## Vedere anche

#### Ulteriori risorse

[New-CsVoicePolicy](new-csvoicepolicy.md)  
[Set-CsVoicePolicy](set-csvoicepolicy.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Grant-CsVoicePolicy](grant-csvoicepolicy.md)  
[Test-CsVoicePolicy](test-csvoicepolicy.md)

