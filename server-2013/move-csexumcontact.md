---
title: Move-CsExUmContact
TOCTitle: Move-CsExUmContact
ms:assetid: 35ed6bdc-95ea-4bf8-84ce-c4256dc2c4e5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425842(v=OCS.15)
ms:contentKeyID: 49300159
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsExUmContact

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Sposta uno o più contatti del servizio Messaggistica unificata di Exchange in un nuovo pool di registrazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Move-CsExUmContact -Identity <UserIdParameter> -Target <Fqdn> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-IgnoreBackendStoreException <SwitchParameter>] [-PassThru <SwitchParameter>] [-ProxyPool <Fqdn>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con l'esempio 1 l'oggetto contatto di Messaggistica unificata di Exchange con indirizzo SIP exum1@fabrikam.com viene spostato nel pool di registrazione con FQDN atl-cs-001.litwareinc.com. All'esecuzione del comando viene visualizzata una richiesta di conferma, nonostante non sia stato incluso il parametro Confirm. La richiesta viene visualizzata anche se si include il parametro Force.

    Move-CsExUmContact -Identity "sip:exum1@fabrikam.com" -Target atl-cs-001.litwareinc.com

## ESEMPIO 2

In questo esempio tutti gli oggetti contatto di Messaggistica unificata di Exchange che rappresentano operatori automatici vengono spostati nel pool di registrazione con FQDN atl-cs-001.litwareinc.com. L'esempio inizia con una chiamata al cmdlet **Get-CsExUmContact**, che recupera tutti i contatti di Messaggistica unificata di Exchange definiti. Questa raccolta di contatti viene quindi inviata tramite pipe al cmdlet **Where-Object**, che individua tutti i contatti della raccolta la cui proprietà AutoAttendant ha il valore True ($True), che indica che il contatto è un operatore automatico.

Infine, la raccolta di contatti per cui AutoAttendant è True viene inviata tramite pipe al cmdlet **Move-CsExUmContact**, che sposta questi contatti nel pool di registrazione specificato nel parametro Target.

Come nell'esempio 1, viene richiesta una conferma durante l'esecuzione di questo comando.

    Get-CsExUmContact | Where-Object {$_.AutoAttendant -eq $True} | Move-CsExUmContact -Target atl-cs-001.litwareinc.com

## Descrizione dettagliata

Lync Server interagisce con il servizio Messaggistica unificata di Exchange per fornire diverse funzionalità vocali, tra cui Operatore automatico e Accesso sottoscrittore. Il cmdlet **Move-CsExUmContact** consente di spostare un oggetto contatto esistente di Messaggistica unificata di Exchange in un nuovo pool di registrazione.

Quando viene spostato un oggetto contatto di Messaggistica unificata di Exchange, le proprietà AutoAttendant e IsSubscriberAccess vengono impostate in base al valore della proprietà OtherIpPhone dell'oggetto.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Move-CsExUmContact** in locale: RTCUniversalUserAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Move-CsExUmContact"}

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
<td><p>L'identificatore univoco dell'oggetto contatto che si desidera spostare. Le identità dei contatti possono essere specificate utilizzando uno dei quattro formati seguenti: 1) l'indirizzo SIP del contatto; 2) l'UPN (User Principal Name) del contatto; 3) il nome di dominio e il nome di accesso del contatto, nella forma dominio\accesso (ad esempio litwareinc\exum1); 4) il nome visualizzato in Active Directory per il contatto (ad esempio Team Auto Attendant).</p></td>
</tr>
<tr class="even">
<td><p><em>Target</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Il nome di dominio completo (FQDN) del pool di registrazione in cui deve essere spostato il contatto.</p></td>
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
<td><p>Consente di connettersi al controller di dominio specificato. Per la connessione a uno specifico controller di dominio, includere il parametro DomainController seguito dal nome computer (ad esempio atl-mcs-001) o dal suo nome di dominio completo (ad esempio atl-mcs-001.litwareinc.com).</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreBackendStoreException</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, questo parametro indica al computer di ignorare gli eventuali errori che possono verificarsi con il database back-end e di tentare comunque di spostare il contatto.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di passare un oggetto contatto attraverso la pipeline che rappresenta l'account contatto spostato. Per impostazione predefinita, il cmdlet <strong>Move-CsExUmContact</strong> non passa oggetti attraverso la pipeline.</p></td>
</tr>
<tr class="even">
<td><p><em>ProxyPool</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Questo parametro è utilizzato solo per le istanze ospitate di Lync Server. Non deve essere utilizzato con un'implementazione locale di Lync Server.</p></td>
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

Stringa. Accetta un valore stringa da pipeline che rappresenta l'identità di un oggetto Messaggistica unificata di Exchange da spostare.

## Tipi restituiti

Se chiamato con il parametro PassThru, restituisce un oggetto di tipo Microsoft.Rtc.Management.ADConnect.Schema.OCSADExUmContact.

## Vedere anche

#### Ulteriori risorse

[New-CsExUmContact](new-csexumcontact.md)  
[Remove-CsExUmContact](remove-csexumcontact.md)  
[Set-CsExUmContact](set-csexumcontact.md)  
[Get-CsExUmContact](get-csexumcontact.md)

