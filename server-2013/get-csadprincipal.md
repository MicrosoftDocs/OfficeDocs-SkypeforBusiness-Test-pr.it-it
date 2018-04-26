---
title: Get-CsAdPrincipal
TOCTitle: Get-CsAdPrincipal
ms:assetid: df2c3714-4064-4113-861f-95ce0ae8da81
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205326(v=OCS.15)
ms:contentKeyID: 49302218
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAdPrincipal

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle entità di Active Directory. Queste entità includono oggetti Active Directory quali utenti, gruppi, contatti, contenitori e unità organizzative. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsAdPrincipal [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-LDAPFilter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce tutte le entità di Active Directory presenti nell'organizzazione.

    Get-CsAdPrincipal

## Esempio 2

Nell'esempio 2 vengono restituite informazioni per una sola entità di Active Directory: l'entità con l'indirizzo SIP "sip:RedmondMeetingRoom@litwareinc.com". A tal fine viene incluso il parametro Filter e un valore di filtro che cerca le entità in cui la proprietà SipAddress è uguale a (-eq) "sip:RedmondMeetingRoom@litwareinc.com".

    Get-CsAdPrincipal -Filter {SipAddress -eq "sip:RedmondMeetingRoom@litwareinc.com"}

## Esempio 3

Nell'esempio precedente vengono restituite informazioni per tutti gli oggetti Active Directory. Per eseguire questa attività, il comando chiama innanzitutto il cmdlet **Get-CsAdPrincipal** senza alcun parametro. In questo modo viene restituita una raccolta di tutte le entità di Active Directory. Questa raccolta viene quindi inviata al cmdlet **Where-Object** che seleziona solo le entità in cui la proprietà ObjectClass contiene il valore stringa "contact".

    Get-CsAdPrincipal | Where-Object {$_.ObjectClass -contains "contact"}

## Descrizione dettagliata

Il cmdlet **Get-CsAdPrincipa**l restituisce una raccolta di entità di Active Directory che possono essere utilizzate per la creazione di elenchi di appartenenze di Chat persistente. Per ulteriori dettagli, vedere nella Guida le informazioni sui parametri AllowedMembers e DeniedMembers del cmdlet **Set-CsPersistentChatCategory**. **Get-CsPrincipal** restituisce informazioni su oggetti Active Directory quali:

  - **Utenti** (object class = {top, person, organizationalPerson, user})

  - **Gruppi** (object class = {top, group})

  - **Contatti** (object class = {top, person, organizationalPerson, contact})

  - **Contenitori** (object class = {top, container})

  - **Unità organizzative** (object class = {top, organizationalUnit})

  - **Domini** (object class = {top, domain, domainDNS})

Questo significa, tra l'altro, che è possibile utilizzare il cmdlet **Get-CsAdPrincipal** e la proprietà objectClass per restituire rapidamente informazioni su oggetti Active Directory quali unità organizzative o gruppi. Il comando seguente, ad esempio, restituisce i nomi di tutte le unità organizzative di Active Directory:

Get-CsAdPrincipal | Where-Object {$\_.ObjectClass –match "organizationalUnit"} | Select-Object Name

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAdPrincipal"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet Get-CsAdPrincipal non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Consente di eseguire il cmdlet <strong>Get-CsAdPrincipal</strong> utilizzando credenziali alternative. Può essere necessario se l'account utilizzato per accedere a Windows non dispone dei privilegi necessari richiesti per lavorare con gli oggetti utente.</p>
<p>Per utilizzare il parametro Credential è necessario creare per prima cosa un oggetto PSCredential utilizzando il cmdlet <strong>Get-Credential</strong>. Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet <strong>Get-Credential</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di connettere il controller di dominio specificato per ottenere informazioni sull'entità di Active Directory. Per connettere un particolare controller di dominio, includere il parametro DomainController seguito dal nome del computer, ad esempio atl-dc-001, oppure il relativo nome di dominio completo (FQDN), ad esempio atl-dc-001.litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro basato su attributi specifici di Lync Server.</p>
<p>Il parametro Filter utilizza in gran parte la stessa sintassi di filtro Windows PowerShell impiegata dal cmdlet <strong>Where-Object</strong>. Ad esempio, un filtro che restituisce solo entità che non sono abilitate per Lync Server sarebbe analogo al seguente:</p>
<p>-Filter {Enabled -ne $True}</p>
<p>In questo esempio Enabled rappresenta l'attributo Active Directory, -ne rappresenta l'operatore di confronto (non uguale a) e $True (una variabile di Windows PowerShell incorporata) rappresenta il valore True.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Indica l'identità dell'account dell'entità da recuperare. Le identità vengono in genere specificate utilizzando uno dei quattro formati seguenti: 1) l'indirizzo SIP dell'account, 2) il nome dell'entità utente (UPN, User Principal Name), 3) il nome di dominio e il nome di accesso dell'account nel formato dominio\accesso (ad esempio litwareinc\kenmyer), 4) il nome visualizzato Active Directory dell'account (ad esempio Ken Myer).</p>
<p>È anche possibile fare riferimento a un account utente utilizzando il nome distinto Active Directory dell'utente.</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come identità. Ad esempio, l'identità &quot;* Smith&quot; restituisce tutti gli utenti il cui nome visualizzato termina con il valore stringa &quot; Smith&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>LDAPFilter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro in base ad attributi generici di Active Directory (ovvero attributi non specifici di Lync Server). Ad esempio, è possibile limitare i dati restituiti alle entità che appartengono a in un reparto specifico o che possiedono un manager o un titolo professionale specifico.</p>
<p>Il parametro LdapFilter utilizza il linguaggio di query LDAP per la creazione dei filtri. Ad esempio, un filtro che restituisce solamente entità collocate nella città di Redmond potrebbe essere simile al seguente:</p>
<p>-LdapFilter &quot;l=Redmond&quot;</p>
<p>In questo esempio la lettera elle minuscola &quot;l&quot; rappresenta l'attributo di Active Directory (località), &quot;=&quot; rappresenta l'operatore di confronto (uguale a) e &quot;Redmond&quot; rappresenta il valore di filtro.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Consente di restituire informazioni su entità in una specifica unità organizzativa o in un contenitore. Il parametro OU restituisce i dati dell'unità organizzativa specificata e delle unità organizzative figlio. Ad esempio, se l'unità organizzativa Finance contiene due unità organizzative figlio, AccountsPayable e AccountsReceivable, saranno restituite le entità di tutte e tre le unità organizzative.</p>
<p>Per specificare un'unità organizzativa occorre utilizzare il nome distinto del contenitore, ad esempio:</p>
<p>-OU &quot;OU=Finance,dc=litwareinc,dc=com&quot;</p>
<p>Per restituire le entità del contenitore Users, utilizzare la seguente sintassi:</p>
<p>-OU &quot;cn=Users,dc=litwareinc,dc=com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>Consente di limitare il numero di record restituiti dal cmdlet. Ad esempio, per restituire sette entità (indipendentemente dal numero di entità nella foresta), includere il parametro -ResultSize e impostarne il valore su 7. Non c'è modo di stabilire quali sette entità saranno restituite.</p>
<p>La dimensione del risultato può essere impostata su qualsiasi numero intero compreso tra 0 e 2147483647 (compresi). Se l'impostazione è 0 il comando viene eseguito ma non restituisce dati. Se si imposta ResultSize su 7 ma nella foresta sono contenute solo tre entità, il comando restituirà le tre entità e quindi verrà completato senza errori.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Valore di stringa o oggetto che rappresenta un utente, un gruppo, un contenitore e un'unità organizzativa di Active Directory. Ad esempio, la sintassi seguente restituisce informazioni sulle entità di Active Directory per le unità organizzative di Redmond e Dublino:

"OU=Redmond,DC=litwareinc,DC=com", "OU=Dublin,DC=litwareinc,DC=com" | Get-CsAdPrincipal

## Tipi restituiti

Il cmdlet **Get-CsAdPrincipal** restituisce istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADPrincipal.

## Vedere anche

#### Ulteriori risorse

[New-CsPersistentChatCategory](new-cspersistentchatcategory.md)  
[Set-CsPersistentChatCategory](set-cspersistentchatcategory.md)

