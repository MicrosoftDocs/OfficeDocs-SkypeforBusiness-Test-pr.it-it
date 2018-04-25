---
title: Grant-CsVoicePolicy
TOCTitle: Grant-CsVoicePolicy
ms:assetid: c8aa8d0f-6fb4-43f7-82b0-38d4da2d5611
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398828(v=OCS.15)
ms:contentKeyID: 49301928
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsVoicePolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Assegna un criterio vocale a uno o più utenti o gruppi. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Grant-CsVoicePolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Questo esempio assegna il criterio vocale con il valore Identity VoicePolicyRedmond all'utente con il nome di visualizzazione Davide Garghentini.

    Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName VoicePolicyRedmond

## ESEMPIO 2

In questo esempio viene assegnato il criterio vocale con valore Identity VoicePolicyRedmond a tutti gli utenti dell'unità organizzativa (OU) Finance: OU=Finance,OU=NorthAmerica,DC=litwareinc,DC=com. Nella prima parte del comando viene chiamato il cmdlet **Get-CsUser** per recuperare tutti gli utenti abilitati per Lync Server o Office Communications Server dall'unità organizzativa specificata. Questa raccolta di utenti viene quindi inviata tramite pipe al cmdlet **Grant-CsVoicePolicy**, che assegna il criterio VoicePolicyRedmond a ognuno di questi utenti.

    Get-CsUser -OU "ou=Finance,ou=North America,dc=litwareinc,dc=com" | Grant-CsVoicePolicy -PolicyName VoicePolicyRedmond

## Descrizione dettagliata

Questo cmdlet assegna a un utente criteri vocali per utente già esistenti. I criteri vocali sono utilizzati per gestire funzionalità di VoIP aziendale quali, ad esempio, lo squillo simultaneo (vale a dire la capacità di far squillare un secondo telefono ogni volta che si riceve una chiamata sul telefono dell'ufficio) e l'inoltro di chiamata. Utilizzare questo cmdlet per assegnare le impostazioni che abilitano e disabilitano queste funzionalità per un utente specifico.

È possibile controllare se a un utente sono stati concessi criteri vocali per utente chiamando un comando in questo formato: Get-CsUser "\<nome utente\>" | Select-Object VoicePolicy. Ad esempio:

Get-CsUser "Davide Garghentini" | Select-Object VoicePolicy

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Grant-CsVoicePolicy** i membri dei seguenti gruppi: RTCUniversalUserAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsVoicePolicy"}

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Il parametro Identity (identificatore univoco) dell'utente a cui è stato assegnato il criterio.</p>
<p>Le identità utente possono essere specificate con uno dei quattro formati riportati di seguito: 1) L'indirizzo SIP dell'utente; 2) il nome dell'entità utente (UPN); 3) il nome del dominio dell'utente e il nome di accesso nel formato dominio\accesso (ad esempio, litwareinc\davidegarghentini); infine, 4) il nome visualizzato in Servizi di dominio Active Directory dell'utente (ad esempio, Davide Garghentini).</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il valore di Display Name per il parametro Identity per l'utente. Ad esempio, il parametro Identity &quot;* Smith&quot; restituisce tutti gli utenti con cognome Smith.</p>
<p>Tipo di dati completi: Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il nome (Identity) del criterio vocale da assegnare all'utente. (Il nome include solo la porzione del nome dell'Identity. Le identità criterio per utente includono un prefisso di tag: che non può essere incluso nel parametro PolicyName.)</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di specificare un controller di dominio. Se non è specificato alcun controller di dominio, verrà utilizzato il primo disponibile.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce i risultati del comando. Per impostazione predefinita, il cmdlet non genera alcun output.</p></td>
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

Stringa. Accetta un valore stringa da pipeline che rappresenta l'identità dell'account utente a cui viene assegnato il criterio vocale.

## Tipi restituiti

Se viene utilizzato con il parametro PassThru, restituisce un oggetto di tipo Microsoft.Rtc.Management.ADConnect.Schema.OCSADUserOrAppContact.

## Vedere anche

#### Ulteriori risorse

[New-CsVoicePolicy](new-csvoicepolicy.md)  
[Remove-CsVoicePolicy](remove-csvoicepolicy.md)  
[Set-CsVoicePolicy](set-csvoicepolicy.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Test-CsVoicePolicy](test-csvoicepolicy.md)  
[Get-CsUser](get-csuser.md)

