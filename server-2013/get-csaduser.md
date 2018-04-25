---
title: Get-CsAdUser
TOCTitle: Get-CsAdUser
ms:assetid: 787f0ccf-3ac3-4a2b-8407-cff5e988b9b4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398592(v=OCS.15)
ms:contentKeyID: 49301045
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAdUser

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni su tutti gli account utente in Servizi di dominio Active Directory. Sono inclusi gli account utente abilitati per Lync Server e gli account non abilitati per Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsAdUser [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-LDAPFilter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 viene restituita una raccolta di tutti gli account utente nel dominio di Active Directory.

    Get-CsAdUser

## ESEMPIO 2

Nell'esempio 2 il cmdlet **Get-CsAdUser** restituisce le informazioni sull'account utente di Pilar Ackerman. In questo esempio viene utilizzato il nome visualizzato dell'utente per specificarne l'identità (Identity).

    Get-CsAdUser -Identity "Pilar Ackerman"

## ESEMPIO 3

Con l'esempio 3 vengono restituite le informazioni sull'account utente per tutti gli utenti nell'unità organizzativa Finance. Per eseguire questa operazione, al parametro OU deve essere passato il nome distinto dell'unità organizzativa.

    Get-CsAdUser -OU "ou=Finance,dc=litwareinc,dc=com"

## ESEMPIO 4

Nell'esempio 4 vengono restituiti tutti gli utenti che non sono stati abilitati per Lync Server oppure Office Communications Server. A tale scopo, viene utilizzato il parametro Filter con il cmdlet **Get-CsAdUser** per limitare i dati restituiti agli account utente la cui proprietà Enabled non è uguale a True. Questo filtro indica al cmdlet **Get-CsAdUser** di restituire solo gli account utente non abilitati per l'utilizzo con Lync Server oppure Office Communications Server. Dopo il recupero dei dati, le informazioni vengono inviate tramite pipe al cmdlet **Select-Object**, che quindi identifica l'unica proprietà (in questo caso DisplayName) che verrà effettivamente visualizzata.

    Get-CsAdUser -Filter {Enabled -ne $True} | Select-Object DisplayName

## ESEMPIO 5

Con l'esempio 5 viene utilizzato il parametro LdapFilter per limitare i dati restituiti agli utenti che lavorano nel reparto Finance. Questa operazione viene eseguita utilizzando il valore del filtro LDAP "Department=Finance".

    Get-CsAdUser -LdapFilter "Department=Finance"

## Descrizione dettagliata

Il cmdlet **Get-CsAdUser** restituisce informazioni su tutti gli account utente in Active Directory, inclusi gli account utente abilitati e non abilitati per Lync Server. Il comportamento è diverso da quello del cmdlet **Get-CsUser**, che restituisce informazioni solo per gli utenti i cui account sono stati abilitati per Lync Server o per una versione precedente del software, ad esempio Microsoft Office Communications Server 2007 R2.

Sebbene esista una certa sovrapposizione tra i due cmdlet, i cmdlet **Get-CsAdUser** e **Get-CsUser** differiscono anche a livello del tipo di informazioni restituite. Il cmdlet **Get-CsUser** in genere restituisce valori per gli attributi di Active Directory correlati a Lync Server. Ad esempio, il cmdlet **Get-CsUser** può comunicare quali criteri di Lync Server sono stati assegnati a un utente, l'URI di linea assegnato all'utente, nonché se l'utente è stato abilitato per VoIP aziendale. Questi attributi non saranno parte di un account utente se tale utente non è stato abilitato per Lync Server.

Al contrario, il cmdlet **Get-CsAdUser** restituisce valori di attributo Active Directory generici. In pratica, restituisce informazioni sugli attributi che sono parte dell'account utente Active Directory di base e che sono presenti anche se un utente non è stato abilitato per Lync Server. Ad esempio, il cmdlet **Get-CsAdUser** restituisce informazioni quali il reparto e l'organizzazione per cui lavora l'utente, insieme alla posizione, al numero di telefono e all'indirizzo dell'ufficio. Per visualizzare un elenco completo dei valori di attributo restituiti dal cmdlet **Get-CsAdUser**, al prompt di Windows PowerShell digitare il comando seguente:

Get-CsAdUser | Get-Member

Il cmdlet **Get-CsAdUser** offre diversi modi per filtrare la raccolta di utenti restituita quando si esegue il cmdlet. Se ad esempio non si desidera restituire tutti gli account utente Active Directory, è possibile applicare il parametro facoltativo Filter o LdapFilter. Questi parametri si escludono reciprocamente. Se pertanto si utilizza Filter in un comando, non sarà possibile utilizzare LdapFilter nello stesso comando e viceversa. Il parametro Filter consente di circoscrivere i dati restituiti limitandosi agli utenti che soddisfano i criteri specificati per gli attributi specifici di Lync Server. È ad esempio possibile utilizzare il parametro Filter per restituire una raccolta degli utenti che sono stati abilitati o che non sono stati abilitati per Lync Server. Il parametro LdapFilter consente di circoscrivere i dati restituiti limitandosi agli utenti che soddisfano altri criteri basati su attributi generici Active Directory, ad esempio gli utenti che lavorano in una provincia o in uno stato specifico, gli utenti che possiedono o meno un cercapersone oppure gli utenti con una determinata posizione professionale.

Un aspetto importante da considerare per quando riguarda il cmdlet **Get-CsAdUser** è il seguente: sebbene l'attributo Enabled, che determina se un utente è stato o meno abilitato per Lync Server, sia un valore booleano, questa proprietà dispone in realtà di tre valori validi:

True. L'utente è stato abilitato per Lync Server.

False. L'account di Lync Server dell'utente è stato temporaneamente disabilitato. Questo risultato si ottiene in genere utilizzando il cmdlet **Set-CsUser** e impostando il parametro Enabled su $False.

Null. L'utente non è stato abilitato per Lync Server.

Questo significa che, se si desidera restituire un elenco di utenti non abilitati per Lync Server, è necessario utilizzare un comando che restituisca tutti gli utenti per i quali l'attributo Enabled è Null:

Get-CsAdUser –Filter {Enabled –eq $Null}

Il comando seguente restituisce invece solo gli utenti i cui account di Lync Server sono stati temporaneamente disabilitati:

Get-CsAdUser –Filter {Enabled –eq $False}

Gli utenti che non sono stati abilitati per Lync Server non verranno restituiti quando si esegue il comando precedente.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Get-CsAdUser** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAdUser"}

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
<td><p>Consente di eseguire il cmdlet <strong>Get-CsAdUser</strong> utilizzando credenziali alternative. Può essere necessario se l'account utilizzato per accedere a Windows non dispone dei privilegi necessari richiesti per lavorare con gli oggetti utente.</p>
<p>Per utilizzare il parametro Credential, è necessario creare innanzitutto un oggetto PSCredential utilizzando il cmdlet <strong>Get-Credential</strong>. Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet <strong>Get-Credential</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente la connessione al controller di dominio specificato per recuperare le informazioni sull'utente. Per connettersi a un controller di dominio particolare, includere il parametro DomainController seguito dal nome di dominio completo, ad esempio atl-cs-001.litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro in base ad attributi specifici per Lync Server.</p>
<p>Il parametro Filter utilizza la stessa sintassi di filtro Windows PowerShell impiegata dal cmdlet <strong>Where-Object</strong>. Ad esempio, un filtro che restituisce solamente gli utenti non abilitati per Lync Server potrebbe essere simile al seguente: {Enabled -ne $True}, dove Enabled rappresenta l'attributo di Active Directory, -ne rappresenta l'operatore di confronto (diverso da) e $True (una variabile predefinita di Windows PowerShell) rappresenta il valore True.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Indica l'identità dell'account utente da recuperare. Le identità utente possono essere specificate con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP dell'utente; 2) l'UPN (User Principal Name) dell'utente; 3) il nome di dominio e il nome di accesso dell'utente, nel formato dominio\accesso (ad esempio, litwareinc\davidegarghentini); 4) il nome visualizzato Active Directory dell'utente (ad esempio, Davide Garghentini). L'account utente può essere referenziati anche utilizzando il nome distinto dell'utente in Active Directory.</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come identità utente. Ad esempio, il parametro Identity &quot;* Smith&quot; restituirà tutti gli utenti con un nome visualizzato che termina con &quot; Smith&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>LDAPFilter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro in base ad attributi generici di Active Directory (ovvero attributi non specifici di Lync Server). Ad esempio, è possibile limitare i dati restituiti agli utenti che lavorano in un reparto specifico o agli utenti che possiedono un manager o un titolo professionale specifico.</p>
<p>Il parametro LDAPFilter utilizza il linguaggio di query LDAP per la creazione dei filtri. Ad esempio, un filtro che restituisce solo gli utenti che lavorano a Redmond sarà simile al seguente: &quot;l=Redmond&quot;, dove &quot;l&quot; (elle minuscola) rappresenta l'attributo di Active Directory (località), &quot;=&quot; rappresenta l'operatore di confronto (uguale a) e &quot;Redmond&quot; rappresenta il valore di filtro.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Consente di restituire gli utenti da una specifica unità organizzativa o contenitore di Active Directory. Questo parametro restituisce i dati dell'unità organizzativa specificata e delle unità organizzative figlio. Ad esempio, se l'unità organizzativa Finance contiene due unità organizzative figlio, AccountsPayable e AccountsReceivable, saranno restituiti gli utenti di tutte e tre le unità organizzative.</p>
<p>Per specificare un'unità organizzativa occorre utilizzare il nome distinto del contenitore, ad esempio: OU=Finance,dc=litwareinc,dc=com. Per restituire gli utenti del contenitore Users, utilizzare la seguente sintassi: cn=Users,dc=litwareinc,dc=com.</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>Consente di limitare il numero di record restituiti dal cmdlet. Ad esempio, per restituire sette utenti (indipendentemente dal numero di utenti nella foresta), includere il parametro ResultSize e impostarne il valore su 7. Non c'è modo di stabilire quali sette utenti saranno restituiti.</p>
<p>La dimensione del risultato può essere impostata su qualsiasi numero intero compreso tra 0 e 2147483647 (compresi). Se l'impostazione è 0 il comando viene eseguito ma non restituisce dati. Se si imposta ResultSize su 7 ma la foresta contiene solo tre utenti, il comando restituisce tali tre utenti e viene completato senza errori.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa. Il cmdlet **Get-CsAdUser** accetta un valore stringa inviato tramite pipeline che rappresenta l'identità (Identity) di un account utente Active Directory.

## Tipi restituiti

Il cmdlet **Get-CsAdUser** restituisce istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.CSADUser.

## Vedere anche

#### Ulteriori risorse

[Get-CsUser](get-csuser.md)

