---
title: Get-CsOnlineUser
TOCTitle: Get-CsOnlineUser
ms:assetid: 2bfafd70-a7d9-4308-a353-5ecf44249b53
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994026(v=OCS.15)
ms:contentKeyID: 52062119
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsOnlineUser

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sugli utenti che dispongono di account ospitati in Microsoft Lync Online. Questo cmdlet può essere usato solo con Skype for Business online.

## Sintassi

    Get-CsOnlineUser [[-Identity] <UserIdParameter>] [-Filter <String>] [-LdapFilter <String>] [-OnOfficeCommunicationServer] [-OnLyncServer] [-UnAssignedUser] [-OU <OUIdParameter>] [-DomainController <Fqdn>] [-Credential <PSCredential>] [-ResultSize <Unlimited`1>] [-Verbose]

## Esempi

## Esempio 1

Il comando illustrato nell'esempio 1 restituisce informazioni per tutti gli utenti configurati come utenti online.

    Get-CsOnlineUser

## Esempio 2

Nell'esempio 2 vengono restituite informazioni per un singolo utente online: l'utente con indirizzo SIP "sip:kenmyer@litwareinc.com".

    Get-CsOnlineUser -Identity "sip:kenmyer@litwareinc.com"

## Esempio 3

Il comando riportato nell'esempio 3 restituisce informazioni per tutti gli utenti online abilitati per Lync Online, ma non ancora assegnati a un pool di registrazione.

    Get-CsOnlineUser -UnassignedUser

## Esempio 4

L'esempio 4 usa il parametro Filter per limitare i dati restituiti agli utenti online a cui è sono stati assegnati i criteri di archiviazione per utente RedmondArchiving. A tale scopo viene usato il valore di filtro {ArchivingPolicy -eq "RedmondArchiving"}. Con questa sintassi i dati restituiti sono limitati agli utenti per i quali la proprietà ArchivingPolicy è uguale a (-eq) "RedmondArchiving".

    Get-CsOnlineUser -Filter {ArchivingPolicy -eq "RedmondArchiving"}

## Esempio 5

L'esempio 5 restituisce informazioni solo per gli account utente configurati in modo che l'account non compaia negli elenchi di indirizzi di Microsoft Exchange, ovvero l'attributo di Active Directory msExchHideFromAddressLists è True. Per eseguire questa operazione viene incluso il parametro Filter oltre al valore di filtro {HideFromAddressLists -eq $True}.

    Get-CsOnlineUser -Filter {HideFromAddressLists -eq $True}

## Esempio 6

Il comando illustrato nell'esempio 6 restituisce informazioni per tutti gli utenti online assegnati al tenant con TenantID "bf19b7db-6960-41e5-a139-2aa373474354". Per eseguire questa operazione, il comando include il parametro Filter insieme al valore di filtro {TenantId –eq "bf19b7db-6960-41e5-a139-2aa373474354"}. Questo filtro limita i dati restituiti agli utenti online assegnati al tenant "bf19b7db-6960-41e5-a139-2aa373474354".

    Get-CsOnlineUser -Filter {TenantId -eq "bf19b7db-6960-41e5-a139-2aa373474354"}

## Descrizione dettagliata

Il cmdlet **Get-CsOnlineUser** restituisce informazioni sugli utenti con account ospitati in Microsoft Lync Online. Le informazioni restituite includono informazioni standard sugli account di Active Directory, come il reparto dell'utente, l'indirizzo, il numero di telefono e così via. Il cmdlet **Get-CsOnlineUser** restituisce anche informazioni specifiche di Lync Server come l'abilitazione dell'utente per VoIP aziendale e gli eventuali criteri per utente assegnati all'utente.

Si noti che per il cmdlet **Get-CsOnlineUser** non è disponibile un parametro TenantId e questo significa che non è possibile usare un comando simile a questo per limitare i dati restituiti agli utenti con account per un tenant specifico di Lync Online:

    Get-CsOnlineUser -TenantId "bf19b7db-6960-41e5-a139-2aa373474354"

In presenza di più tenant di Lync Online, tuttavia, è possibile restituire gli utenti da un tenant specificato tramite il parametro Filter e un comando simile al seguente:

    Get-CsOnlineUser -Filter {TenantId -eq "bf19b7db-6960-41e5-a139-2aa373474354"}

Questo comando limiterà i dati restituiti agli account utente appartenenti al tenant con TenantId "bf19b7db-6960-41e5-a139-2aa373474354". Se gli ID dei tenant non sono noti, è possibile usare questo comando per restituire queste informazioni:

    Get-CsTenant

In caso di una distribuzione ibrida o con dominio diviso (ossia una distribuzione nella quale alcuni utenti sono ospitati in Lync Online mentre altri hanno account ospitati in una versione locale di Lync Server) tenere presente che il cmdlet **Get-CsOnlineUser** restituisce solo informazioni per gli utenti di Lync Online. Il cmdlet [Get-CsUser](get-csuser.md), tuttavia, restituirà informazioni sia per gli utenti di Lync Online che per gli utenti di Lync Server. Se si vogliono escludere gli utenti di Lync Online dai dati restituiti dal cmdlet **Get-CsUser**, usare il comando seguente:

    Get-CsUser -Filter {TenantId -eq "00000000-0000-0000-0000-000000000000"}

Per definizione, il TenantId degli utenti ospitati nella versione locale di Lync Server sarà sempre 00000000-0000-0000-0000-000000000000. Il TenantId degli utenti ospitati in Lync Online sarà uguale a un qualche valore diverso da 00000000-0000-0000-0000-000000000000.

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
<td><p><em>Credential</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Consente di eseguire il cmdlet <strong>Get-CsOnlineUser</strong> utilizzando credenziali alternative. Può essere obbligatorio se l'account utilizzato per accedere a Windows non dispone dei privilegi necessari, richiesti per utilizzare gli oggetti utente.</p>
<p>Per utilizzare il parametro Credential, è necessario creare innanzitutto un oggetto PSCredential utilizzando il cmdlet <strong>Get-Credential</strong>. Per informazioni dettagliate, vedere nella Guida l'argomento relativo al cmdlet <strong>Get-Credential</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di eseguire la connessione al controller di dominio specificato per recuperare le informazioni sull'utente. Per la connessione a un controller di dominio specifico, includere il parametro DomainController seguito dal nome di dominio completo (ad esempio, atl-cs-001.litwareinc.com).</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro in base ad attributi specifici di Lync Server. Ad esempio, è possibile limitare i dati restituiti agli utenti a cui è stato assegnato un criterio vocale specifico o agli utenti a cui non è stato assegnato un criterio vocale specifico.</p>
<p>Il parametro Filter usa la stessa sintassi di filtro di Windows PowerShell impiegata dal cmdlet Where-Object. Ad esempio, un filtro che restituisce solo utenti abilitati per VoIP aziendale sarà simile a quello seguente, dove EnterpriseVoiceEnabled indica l'attributo di Servizi di dominio Active Directory, -eq indica l'operatore di confronto (uguale a) e $True (una variabile incorporata di Windows PowerShell) indica il valore del filtro:</p>
<p>{EnterpriseVoiceEnabled -eq $True}</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Indica l'identità dell'account utente da recuperare. Le identità dell'utente possono essere specificate utilizzando uno dei seguenti quattro formati: 1) l'indirizzo SIP dell'utente; 2) il nome dell'entità utente (UPN); 3) il nome del dominio e il nome di accesso dell'utente nella forma dominio\accesso (ad esempio, litwareinc\kenmyer); 4) il nome visualizzato Active Directory dell'utente (ad esempio, Ken Myer). È anche possibile fare riferimento a un account utente utilizzando il nome distinto Active Directory dell'utente.</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come identità (Identity) utente. Ad esempio, il parametro Identity &quot;* Smith&quot; restituirà tutti gli utenti con un nome visualizzato che termina con &quot; Smith&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>LdapFilter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro in base ad attributi generici di Active Directory (ovvero attributi non specifici di Lync Server). Ad esempio, è possibile limitare i dati restituiti agli utenti che lavorano in un reparto specifico o agli utenti che possiedono una qualifica specifica.</p>
<p>Il parametro LdapFilter utilizza il linguaggio di query LDAP per la creazione dei filtri. Ad esempio, un filtro che restituisce solo gli utenti che lavorano a Redmond sarà simile al seguente: &quot;l=Redmond&quot;, dove &quot;l&quot; (L minuscola) rappresenta l'attributo di Active Directory (località), &quot;=&quot; rappresenta l'operatore di confronto (uguale a) e &quot;Redmond&quot; rappresenta il valore di filtro.</p></td>
</tr>
<tr class="even">
<td><p><em>OnLyncServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce una raccolta di utenti ospitati in Lync Server. Gli utenti i cui account sono associati alle versioni precedenti del software non vengono restituiti quando si utilizza questo parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>OnOfficeCommunicationServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce una raccolta di utenti ospitata su una versione precedente di Lync Server (ad esempio, Microsoft Office Communications Server 2007 R2). Gli utenti i cui account sono associati alla versione corrente del software non verranno restituiti quando si utilizza questo parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Consente di ottenere solo gli account utente di una specifica unità organizzativa o di un contenitore. Il parametro OU restituisce i dati dell'unità organizzativa specificata e delle unità organizzative figlio. Ad esempio, se l'unità organizzativa Finance contiene due unità organizzative figlio, AccountsPayable e AccountsReceivable, saranno restituiti gli utenti di tutte e tre le unità organizzative.</p>
<p>Per specificare una OU occorre usare il nome distinto (DN) del contenitore, ad esempio: -OU &quot;OU=Finance,dc=litwareinc,dc=com&quot;. Per restituire account utente dal contenitore Users, usare la sintassi seguente:</p>
<p>-OU &quot;cn=Users,dc=litwareinc,dc=com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>Consente di limitare il numero di record restituiti dal cmdlet. Ad esempio, per restituire sette utenti (indipendentemente dal numero di utenti nella foresta), includere il parametro -ResultSize e impostarne il valore su 7. Non c'è modo di stabilire quali sette utenti saranno restituiti.</p>
<p>ResultSize può essere impostato su qualsiasi numero intero compreso tra 0 e 2147483647. Se impostato su 0, il comando verrà eseguito ma i dati non verranno restituiti. Se si imposta ResultSize su 7, ma la foresta contiene solo tre utenti, il comando restituirà i tre utenti e verrà completato senza errori.</p></td>
</tr>
<tr class="even">
<td><p><em>UnassignedUser</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di restituire una raccolta di tutti gli utenti abilitati per Lync Online ma non assegnati al momento a un pool di registrazione. Agli utenti non è consentito l'accesso a meno che non vengano assegnati a un pool di registrazione.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Get-CsOnlineUser** accetta le istanze inviate tramite pipeline dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADUser, nonché i valori stringa che rappresentano un'identità di account utente valida, ad esempio "sip:kenmyer@litwareinc.com").

## Tipi restituiti

Il cmdlet **Get-CsOnlineUser** restituisce istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADOCOnlineUser.

## Vedere anche

#### Ulteriori risorse

[Get-CsUser](get-csuser.md)

