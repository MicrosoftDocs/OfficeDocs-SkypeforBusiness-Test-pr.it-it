---
title: Get-CsAdContact
TOCTitle: Get-CsAdContact
ms:assetid: a5f599fb-8ede-432d-a6bf-c850c68fc71e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412776(v=OCS.15)
ms:contentKeyID: 49301557
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAdContact

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In una topologia a più foreste restituisce informazioni sugli account utente di foreste diverse dalla propria. Si tratta di utenti che sono stati replicati come oggetti contatto da Microsoft Forefront Identity Manager 2010 o da una versione precedente del prodotto. Il cmdlet **Get-CsAdContact** restituisce tutti gli utenti per cui è configurato un valore per l'attributo msRTCSIP-OriginatorSid. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsAdContact [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-LDAPFilter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 restituisce una raccolta dei contatti di tutte le altre foreste rilevati in Servizi di dominio Active Directory. Se si chiama il cmdlet **Get-CsAdContact** senza alcun parametro, vengono restituiti tutti i valori delle proprietà di tutti i contatti Active Directory.

    Get-CsAdContact

## ESEMPIO 2

Anche nell'esempio 2 viene restituita una raccolta di tutti i contatti Active Directory. In questo caso, tuttavia, la raccolta viene inviata tramite pipe al cmdlet **Select-Object**, che consente di specificare gli unici due attributi che verranno visualizzati sullo schermo: DisplayName e SipAddress.

    Get-CsAdContact | Select-Object DisplayName, SipAddress

## ESEMPIO 3

Nell'esempio 3 vengono restituite le informazioni su un unico contatto di Active Directory, ovvero il contatto con l'identità "Ken Myer".

    Get-CsAdContact -Identity "Ken Myer"

## ESEMPIO 4

Nell'esempio 4 il comando restituisce tutti i contatti Active Directory che lavorano per Fabrikam. A tale scopo, viene chiamato il cmdlet **Get-CsAdContact** con il parametro LdapFilter. In questo esempio i dati restituiti si limitano ai contatti con attributo Organization impostato su "Fabrikam".

    Get-CsAdContact -LdapFilter "Organization=Fabrikam"

## ESEMPIO 5

Con i due comandi mostrati nell'esempio 5 viene illustrato l'utilizzo del parametro Credential, che consente di eseguire il cmdlet **Get-CsAdContact** utilizzando credenziali alternative. Nel primo comando viene chiamato il cmdlet **Get-Credential** per creare un oggetto PSCredential per l'account litwareinc\\administrator. Questo comando visualizza una finestra di dialogo di richiesta credenziali per l'utente litwareinc\\administrator. Dopo aver specificato la password dell'account, le credenziali vengono archiviate nella variabile $x. Con il secondo comando viene chiamato il cmdlet **Get-CsAdContact** insieme al parametro Credential. Il valore di parametro $x indica che il cmdlet **Get-CsAdContact** deve essere eseguito con l'account litwareinc\\administrator.

    $x = Get-Credential -Credential "litwareinc\administrator"
    Get-CsAdContact -Credential $x

## Descrizione dettagliata

In una topologia a più foreste gli utenti delle altre foreste vengono rappresentati come contatti. Tali contatti sono diversi dai contatti Active Directory. Se si utilizza Utenti e computer di Active Directory per creare un nuovo contatto, l'utente in questione non verrà restituito chiamando il cmdlet **Get-CsAdContact**. Il cmdlet **Get-CsAdContact** restituirà invece solo le informazioni sugli utenti di foreste diverse dalla propria. Se non si dispone di una topologia a più foreste, non sarà necessario chiamare il cmdlet **Get-CsAdContact**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsAdContact** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAdContact"}

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
<td><p>Consente di eseguire il cmdlet <strong>Get-CsAdContact</strong> utilizzando credenziali alternative. Può essere necessario se l'account utilizzato per accedere a Windows non dispone dei privilegi necessari richiesti per lavorare con gli oggetti contatto.</p>
<p>Per utilizzare il parametro Credential è necessario creare per prima cosa un oggetto PSCredential utilizzando il cmdlet <strong>Get-Credential</strong>. Per informazioni dettagliate, vedere l'argomento della Guida Get-Credential.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente la connessione al controller di dominio specificato per recuperare le informazioni di contatto. Per connettersi a un controller di dominio particolare, includere il parametro DomainController, seguito dal nome di dominio completo, ad esempio atl-cs-001.litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro in base ad attributi specifici di Lync Server.</p>
<p>Il parametro Filter utilizza la stessa sintassi di filtro Windows PowerShell impiegata dal cmdlet <strong>Where-Object</strong>. Un filtro che restituisce solamente i contatti con indirizzo SIP che termina con &quot;fabrikam.com&quot; ad esempio potrebbe essere simile al seguente: {SipAddress -like &quot;*@fabrikam.com&quot;}, dove SipAddress rappresenta l'attributo Active Directory, -like rappresenta l'operatore di confronto e &quot;*@fabrikam.com&quot; rappresenta il valore di filtro.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Indica l'identità del contatto da restituire. Le identità dei contatti possono essere specificate con uno dei tre formati seguenti: 1) l'indirizzo SIP del contatto, 2) il nome distinto Active Directory del contatto e 3) il nome visualizzato Active Directory del contatto, ad esempio Davide Garghentini.</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come identità del contatto. L'identità &quot;* Smith&quot; ad esempio restituisce tutti i contatti il cui nome visualizzato termina con il valore stringa &quot;Smith&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>LDAPFilter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro in base ad attributi generici di Active Directory. Ad esempio, è possibile limitare i dati restituiti ai contatti che lavorano in un determinato reparto o ai contatti che hanno un responsabile o una qualifica specifica.</p>
<p>Il parametro LdapFilter utilizza il linguaggio di query LDAP per la creazione di filtri. Un filtro che restituisce il contatto con numero di telefono 1-425-555-1298 ad esempio potrebbe essere simile al seguente: &quot;telephoneNumber=1-425-555-1298&quot;, dove &quot;telephoneNumber&quot; rappresenta l'attributo Active Directory, &quot;=&quot; rappresenta l'operatore di confronto (uguale a) e &quot;1-425-555-1298&quot; rappresenta il valore di filtro.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Consente di limitare le informazioni recuperate da una specifica unità organizzativa o contenitore di Active Directory. Questo parametro restituisce i dati dell'unità organizzativa specificata e delle unità organizzative figlio. Ad esempio, se l'unità organizzativa Finance dispone di due unità organizzative figlio: AccountsPayable e AccountsReceivable, verranno restituiti i contatti di ciascuna di queste unità organizzative.</p>
<p>Per specificare un'unità organizzativa occorre utilizzare il nome distinto del contenitore, ad esempio: OU=Finance,dc=litwareinc,dc=com.</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>Consente di limitare il numero di record restituiti dal cmdlet. Per restituire ad esempio sette contatti (indipendentemente dal numero di contatti presenti nella foresta), includere il parametro ResultSize e impostarne il valore su 7. Non è possibile stabilire quali dei sette utenti verranno restituiti.</p>
<p>La dimensione del risultato può essere impostata su qualsiasi numero intero compreso tra 0 e 2147483647 (compresi). Se l'impostazione è 0 il comando viene eseguito ma non restituisce dati. Se si imposta ResultSize su 7 ma nella foresta sono contenuti solo tre contatti, il comando restituirà i tre contatti e quindi verrà completato senza errori.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa. Il cmdlet **Get-CsAdContact** accetta un valore stringa da pipeline che rappresenta l'identità di un account utente.

## Tipi restituiti

Il cmdlet **Get-CsAdContact** restituisce istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADContact.

## Vedere anche

#### Ulteriori risorse

[Get-CsAdUser](get-csaduser.md)  
[Get-CsUser](get-csuser.md)

