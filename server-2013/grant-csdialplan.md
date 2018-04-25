---
title: Grant-CsDialPlan
TOCTitle: Grant-CsDialPlan
ms:assetid: 730ad014-b1e8-4f0a-be78-32b1b5488b78
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398547(v=OCS.15)
ms:contentKeyID: 49300967
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsDialPlan

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Assegna un dial plan a uno o più utenti o gruppi. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Grant-CsDialPlan -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio viene utilizzato il cmdlet **Grant-CsDialPlan** per assegnare il dial plan RedmondDialPlan all'utente con identità (in questo caso il nome visualizzato) Ken Myer.

    Grant-CsDialPlan -Identity "Ken Myer" -PolicyName RedmondDialPlan

## ESEMPIO 2

Nell'esempio 2 il dial plan RedmondDialPlan viene assegnato a tutti gli utenti i cui uffici si trovano nella città di Redmond. A tale scopo, viene richiamato il cmdlet **Get-CsUser** per recuperare una raccolta di tutti gli utenti il cui ufficio si trova nella città di Redmond. L'operazione viene eseguita con il parametro LdapFilter e la query LDAP l=Redmond. Nel linguaggio di query LDAP utilizzato da Servizi di dominio Active Directory l (elle minuscola) indica la località o la città di un utente. La raccolta viene quindi inviata tramite pipe al cmdlet **Grant-CsDialPlan**, che assegna il dial plan Redmond a ogni utente nella raccolta.

    Get-CsUser -LDAPFilter "l=Redmond" | Grant-CsDialPlan -PolicyName RedmondDialPlan

## Descrizione dettagliata

Questo cmdlet assegna a un utente un dial plan per utente già esistente. I dial plan forniscono informazioni necessarie per consentire agli utenti di VoIP aziendale di effettuare telefonate. Gli utenti che non dispongono di un dial plan valido non potranno effettuare chiamate con VoIP aziendale. Un dial plan determina le regole di normalizzazione applicate e se è necessario comporre un prefisso per le chiamate esterne.

È possibile controllare se a un utente è stato concesso un dial plan per utente chiamando un comando in questo formato: Get-CsUser "\<nome utente\>" | Select-Object DialPlan. Ad esempio:

Get-CsUser "Davide Garghentini" | Select-Object DialPlan

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Grant-CsDialPlan** in locale: RTCUniversalUserAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsDialPlan"}

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
<td><p>L'identità (identificatore univoco) dell'utente a cui è stato assegnato il dial plan.</p>
<p>Le identità utente possono essere specificate con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP dell'utente; 2) l'UPN (User Principal Name) dell'utente; 3) il nome di dominio e il nome di accesso dell'utente, nel formato dominio\accesso (ad esempio, litwareinc\davidegarghentini); 4) il nome visualizzato Active Directory dell'utente (ad esempio, Davide Garghentini).</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il valore di Display Name per il parametro Identity per l'utente. Ad esempio, il parametro Identity &quot;* Smith&quot; restituisce tutti gli utenti con cognome Smith.</p>
<p>Tipo di dati completi: Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il valore Identity del dial plan da assegnare all'utente. (Il nome include solo la porzione del nome dell'Identity. Le identità dei dial plan per utente includono un prefisso tag: che non può essere incluso nel parametro PolicyName.)</p></td>
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

Stringa. Accetta un valore stringa da pipeline che rappresenta l'identità di un account utente a cui viene assegnato il dial plan.

## Tipi restituiti

Se utilizzato con il parametro PassThru, restituisce un oggetto di tipo Microsoft.Rtc.Management.ADConnect.Schema.OCSADUserOrAppContact.

## Vedere anche

#### Ulteriori risorse

[New-CsDialPlan](new-csdialplan.md)  
[Remove-CsDialPlan](remove-csdialplan.md)  
[Set-CsDialPlan](set-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Test-CsDialPlan](test-csdialplan.md)  
[Get-CsUser](get-csuser.md)

