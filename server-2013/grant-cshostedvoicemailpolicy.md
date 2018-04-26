---
title: Grant-CsHostedVoicemailPolicy
TOCTitle: Grant-CsHostedVoicemailPolicy
ms:assetid: ae69358f-1618-4a08-9ec2-225ded3f301f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412829(v=OCS.15)
ms:contentKeyID: 49301664
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsHostedVoicemailPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Assegna un criterio di segreteria telefonica ospitata nell'ambito per utente. Tale ambito consente di assegnare criteri a singoli utenti o a gruppi. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Grant-CsHostedVoicemailPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene assegnato il criterio di segreteria telefonica ospitata con valore Identity ExRedmond all'utente con nome visualizzato Davide Garghentini.

    Grant-CsHostedVoicemailPolicy -Identity "Ken Myer" -PolicyName ExRedmond

## ESEMPIO 2

In questo esempio viene assegnato il criterio di segreteria telefonica ospitata con l'identità ExRedmond a tutti gli utenti dell'unità organizzativa (OU) Finance: OU=Finance,OU=NorthAmerica,DC=litwareinc,DC=com. Nella prima parte del comando viene chiamato il cmdlet **Get-CsUser** per recuperare tutti gli utenti abilitati per Lync Server o Office Communications Server dall'unità organizzativa specificata. Questa raccolta di utenti viene quindi inviata tramite pipe al cmdlet **Grant-CsHostedVoicemailPolicy**, che assegna il criterio ExRedmond a ognuno di questi utenti.

    Get-CsUser -OU "ou=Finance,ou=North America,dc=litwareinc,dc=com" | Grant-CsHostedVoicemailPolicy -PolicyName ExRedmond

## Descrizione dettagliata

Questo cmdlet assegna un criterio di segreteria telefonica ospitato a un utente. Un criterio di segreteria telefonica ospitata specifica come instradare le chiamate senza risposta a un servizio Messaggistica unificata di Exchange ospitato.

È possibile controllare se a un utente sono stati assegnati criteri di segreteria telefonica ospitata per utente chiamando un comando nel formato seguente: Get-CsUser "\<nome utente\>" | Select-Object HostedVoicemailPolicy. Ad esempio:

Get-CsUser "Davide Garghentini" | Select-Object HostedVoicemailPolicy

Se si assegna a un utente un criterio di segreteria telefonica ospitata senza destinazione, non sarà possibile abilitare tale utente per la segreteria telefonica ospitata.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Grant-CsHostedVoicemailPolicy** i membri dei seguenti gruppi: RTCUniversalUserAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsHostedVoicemailPolicy"}

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
<td><p>Identità (identificatore univoco) dell'utente a cui viene assegnato il criterio di segreteria telefonica ospitata.</p>
<p>Le identità utente possono essere specificate con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP dell'utente, 2) il nome dell'entità utente (UPN, User Principal Name), 3) il nome di dominio e il nome di accesso dell'utente nel formato dominio\accesso (ad esempio, litwareinc\davidegarghentini) e infine 4) il nome visualizzato Active Directory dell'utente (ad esempio, Davide Garghentini).</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il valore di Display Name per il parametro Identity per l'utente. Ad esempio, il parametro Identity &quot;* Smith&quot; restituisce tutti gli utenti con cognome Smith.</p>
<p>Tipo di dati completi: Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome (identità) del criterio di segreteria telefonica ospitata da assegnare all'utente. (Il nome include solo la porzione del nome dell'Identity. Le identità criterio di segreteria telefonica ospitata per utente includono un prefisso di tag: che non può essere incluso nel parametro PolicyName.)</p></td>
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

Stringa. Accetta un valore stringa da pipeline che rappresenta l'identità dell'account utente a cui viene assegnato il criterio di segreteria telefonica ospitata.

## Tipi restituiti

Se viene utilizzato con il parametro PassThru, restituisce un oggetto di tipo Microsoft.Rtc.Management.ADConnect.Schema.OCSADUserOrAppContact.

## Vedere anche

#### Ulteriori risorse

[New-CsHostedVoicemailPolicy](new-cshostedvoicemailpolicy.md)  
[Remove-CsHostedVoicemailPolicy](remove-cshostedvoicemailpolicy.md)  
[Set-CsHostedVoicemailPolicy](set-cshostedvoicemailpolicy.md)  
[Get-CsHostedVoicemailPolicy](get-cshostedvoicemailpolicy.md)  
[Get-CsUser](get-csuser.md)

