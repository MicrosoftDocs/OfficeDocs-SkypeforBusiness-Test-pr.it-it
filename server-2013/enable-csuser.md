---
title: Enable-CsUser
TOCTitle: Enable-CsUser
ms:assetid: 8ceed97b-e802-4844-b509-c6ca9619ec55
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398711(v=OCS.15)
ms:contentKeyID: 49301262
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Enable-CsUser

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Abilita uno o più utenti per Lync Server. Gli utenti non possono utilizzare Lync 2013 o altri client Lync Server finché i relativi account utente non vengono abilitati per Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Enable-CsUser -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-HostingProviderProxyFqdn <Fqdn>] [-PassThru <SwitchParameter>] [-ProxyPool <Fqdn>] [-RegistrarPool <Fqdn>] [-SipAddress <String>] [-SipAddressType <FirstLastName | EmailAddress | UserPrincipalName | SAMAccountName | None>] [-SipDomain <Fqdn>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 il cmdlet **Enable-CsUser** abilita l'account utente con il nome visualizzato Pilar Ackerman. In questo esempio l'utente viene assegnato al pool di registrazione atl-cs-001.litwareinc.com e in Lync Server viene generato automaticamente l'indirizzo SIP utilizzando il valore di SamAccountName (pilar) dell'utente seguito dal dominio SIP litwareinc.com.

    Enable-CsUser -Identity "Pilar Ackerman" -RegistrarPool "atl-cs-001.litwareinc.com" -SipAddressType SamAccountName  -SipDomain litwareinc.com

## ESEMPIO 2

Nell'esempio 2 l'account utente Active Directory appartenente a Pilar Ackerman viene abilitato per l'utilizzo con Lync Server. Per configurare l'account per Lync Server, vengono utilizzati i parametri seguenti insieme al cmdlet **Enable-CsUser**: Identity, che identifica l'account da abilitare, RegistrarPool, che indica il server Standard Edition o il pool Enterprise Edition Front End in cui deve trovarsi l'utente, e SipAddress, che specifica l'indirizzo SIP del nuovo utente. In questo caso, l'indirizzo SIP viene assegnato in modo esplicito anziché utilizzando Lync Server per generare automaticamente l'indirizzo.

    Enable-CsUser -Identity "Pilar Ackerman" -RegistrarPool "atl-cs-001.litwareinc.com" -SipAddress "sip:pilar@litwareinc.com"

## ESEMPIO 3

Nell'esempio 3 gli account di tutti gli utenti che lavorano nel reparto Finance vengono abilitati per Lync Server. A tale scopo, viene utilizzato il cmdlet **Get-CsAdUser** insieme al parametro LdapFilter per restituire una raccolta di tutti gli utenti che lavorano nel reparto Finance. Tali informazioni vengono quindi inviate tramite pipe al cmdlet **Enable-CsUser**, che abilita ogni account della raccolta per Lync Server.

Per abilitare un account è necessario specificare il pool di registrazione e l'indirizzo SIP dell'utente. In questo esempio il pool di registrazione viene specificato utilizzando il parametro RegistrarPool. L'indirizzo SIP non viene però assegnato direttamente. Vengono infatti aggiunti al comando due parametri, SipAddressType e SipDomain. Questo significa che un nuovo indirizzo SIP viene generato automaticamente per ogni account, costituito dal SamAccountName dell'utente e dal nome di dominio SIP. Ad esempio, un utente con SAMAccountName davidegarghentini otterrà l'indirizzo SIP sip:davidegarghentini@litwareinc.com.

    Get-CsAdUser -LdapFilter "department=Finance" | Enable-CsUser -RegistrarPool "atl-cs-001.litwareinc.com" -SipAddressType SamAccountName  -SipDomain litwareinc.com

## ESEMPIO 4

Nell'esempio 4 vengono abilitati tutti gli utenti di Active Directory che non sono ancora stati abilitati per Lync Server. A tale scopo, viene richiamato il cmdlet **Get-CsAdUser** con il parametro Filter. Il filtro {Enabled -ne $True} restituisce una raccolta di tutti gli utenti che non sono stati abilitati per Lync Server. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Enable-CsUser**, che abilita ogni account assegnando l'utente al pool di registrazione atl-cs-001.litwareinc.com e generando automaticamente un indirizzo SIP per i singoli utenti.

    Get-CsAdUser -Filter {Enabled -ne $True} | Enable-CsUser -RegistrarPool "atl-cs-001.litwareinc.com" -SipAddressType SamAccountName  -SipDomain litwareinc.com

## Descrizione dettagliata

Prima di poter accedere a Lync Server, un utente deve soddisfare due requisiti: deve essere in possesso di un account di Active Directory valido e questo account deve essere abilitato per Lync Server. Un modo per abilitare un account utente per Lync Server è l'utilizzo del cmdlet **Enable-CsUser**. Per utilizzare questo cmdlet per abilitare un account per Lync Server è necessario: 1) Selezionare un account (o più account) da abilitare; 2) Selezionare un pool di registrazione per l'account; 3) Assegnare all'account un indirizzo SIP. Con Lync Server gli amministratori possono scegliere se assegnare all'utente uno specifico indirizzo SIP oppure lasciare che Lync Server lo crei automaticamente.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Enable-CsUser** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Enable-CsUser"}

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
<td><p>Indica l'identità dell'account utente da abilitare per Lync Server. Le identità utente possono essere specificate con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP dell'utente; 2) il nome dell'entità utente (UPN); 3) il nome del dominio e il nome di accesso dell'utente nel formato dominio\accesso (ad esempio, litwareinc\davidegarghentini); 4) il nome visualizzato Active Directory dell'utente (ad esempio, Davide Garghentini). È anche possibile fare riferimento a un account utente utilizzando il nome distinto Active Directory dell'utente.</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come identità utente. Ad esempio, il parametro Identity &quot;* Smith&quot; restituirà tutti gli utenti con un nome visualizzato che termina con il valore di stringa &quot; Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di eseguire la connessione al controller di dominio specificato per abilitare un account utente. Per la connessione a un controller di dominio specifico, includere il parametro DomainController seguito dal nome computer (ad esempio, atl-cs-001) o dal nome di dominio completo (FQDN) (ad esempio, atl-cs-001.litwareinc.com).</p></td>
</tr>
<tr class="even">
<td><p><em>HostingProviderProxyFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Questo parametro viene utilizzato solo per Lync Online. Non deve essere utilizzato con un'implementazione locale di Lync Server.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di specificare attraverso la pipeline un oggetto utente che rappresenta l'account utente che si sta abilitando per Lync Server. Per impostazione predefinita, il cmdlet <strong>Enable-CsUser</strong> non fornisce alcun oggetto attraverso la pipeline.</p></td>
</tr>
<tr class="even">
<td><p><em>ProxyPool</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Questo parametro viene utilizzato solo per Lync Online. Non deve essere utilizzato con un'implementazione locale di Lync Server.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPool</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Indica il pool di registrazione in cui sarà inserito l'account Lync Server dell'utente.</p></td>
</tr>
<tr class="even">
<td><p><em>SipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di assegnare all'utente uno specifico indirizzo SIP. Quando si specifica l'indirizzo SIP, è necessario farlo precedere da &quot;sip:&quot;. In pratica, il valore fornito al parametro SipAddress deve essere simile al seguente:</p>
<p>sip:davidegarghentini@litwareinc.com</p>
<p>Il parametro SipAddress non deve essere utilizzato con il cmdlet SipAddressType per fare in modo che Lync Server generi automaticamente un indirizzo SIP per l'utente.</p>
<p>Il parametro The SipAddress non può essere utilizzato se vogliono abilitare più utenti nello stesso momento. Invece è possibile generare automaticamente gli indirizzi SIP per quegli utenti utilizzando il parametro SipAddressType.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddressType</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.Cmdlets.AddressType</p></td>
<td><p>Indica a Lync Server di generare automaticamente un indirizzo SIP per il nuovo utente. Affinché Lync Server generi automaticamente l'indirizzo SIP, è necessario includere il parametro SipAddressType e utilizzare uno dei seguenti valori di parametro:</p>
<p>FirstLastName. L'indirizzo SIP corrisponde al nome dell'utente, seguito da un punto, dal cognome dell'utente e dal dominio SIP. Ad esempio, per l'utente Davide Garghentini l'indirizzo SIP diventa: Ken.Myer@litwareinc.com. Se si utilizza questo tipo di indirizzo è necessario includere anche il parametro SipDomain.</p>
<p>EmailAddress Come indirizzo SIP viene utilizzato l'indirizzo di posta elettronica dell'utente (definito in Active Directory).</p>
<p>UserPrincipalName. L'UPN dell'utente viene utilizzato come indirizzo SIP.</p>
<p>SamAccountName. L'indirizzo SIP corrisponde al SamAccountName (nome di accesso) dell'utente seguito dal dominio SIP. Ad esempio, per l'utente con SamAccountName kmyer l'indirizzo SIP diventa: kmyer@litwareinc.com. Se si utilizza questo tipo di indirizzo è necessario includere anche il parametro SipDomain.</p>
<p>Il parametro SipAddressType non è richiesto se si utilizza il parametro SIPAddress e si assegna esplicitamente all'utente un indirizzo SIP.</p></td>
</tr>
<tr class="even">
<td><p><em>SipDomain</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Il dominio SIP per l'account utente in fase di abilitazione. Questo parametro è obbligatorio se si utilizza il parametro SIPAddressType per far sì che Lync Server generi automaticamente un indirizzo SIP per l'utente e se gli indirizzi SIP sono basati sul SamAccountName o sul nome e cognome dell'utente. Questo parametro non è necessario se l'indirizzo SIP viene basato sull'indirizzo di posta elettronica dell'utente o sull'UPN; dato che il nome del dominio è già incluso nei valori di questi attributi.</p></td>
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

Stringa oppure oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Enable-CsUser** accetta gli input tramite pipeline dei valori stringa che rappresentano l'identità di un account utente abilitato per Lync Server. Il cmdlet accetta anche istanze di oggetti utente di Active Directory inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Enable-CsUser** non restituisce alcun oggetto o valore. Configura invece le istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser.

## Vedere anche

#### Ulteriori risorse

[Disable-CsUser](disable-csuser.md)  
[Get-CsUser](get-csuser.md)

