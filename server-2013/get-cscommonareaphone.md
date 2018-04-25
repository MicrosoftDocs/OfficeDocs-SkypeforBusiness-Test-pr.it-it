---
title: Get-CsCommonAreaPhone
TOCTitle: Get-CsCommonAreaPhone
ms:assetid: bfb7927b-49a7-4637-a9ff-fd68897efb45
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412934(v=OCS.15)
ms:contentKeyID: 49301855
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCommonAreaPhone

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui telefoni di area comune gestiti tramite Lync Server. I telefoni di area comune sono telefoni posizionati nelle sale d'attesa degli edifici, nelle sale di ritrovo del personale o in altre posizioni in cui possono essere utilizzati da persone diverse e per usi diversi. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsCommonAreaPhone [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-LdapFilter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 restituisce le informazioni su tutti i telefoni delle aree comuni configurati per l'utilizzo all'interno dell'organizzazione. È possibile eseguire questa operazione chiamando il cmdlet **Get-CsCommonAreaPhone** senza alcun parametro.

    Get-CsCommonAreaPhone

## ESEMPIO 2

Nell'esempio 2 viene restituito il telefono delle aree comuni con nome visualizzato Active Directory "Building 14 Lobby". Questa attività viene eseguita mediante includendo il parametro Filter e il valore di filtro {DisplayName -eq "Building 14 Lobby"}. Il valore di filtro limita gli oggetti restituiti ai telefoni delle aree comuni con proprietà DisplayName uguale a "Building 14 Lobby".

    Get-CsCommonAreaPhone -Filter {DisplayName -eq "Building 14 Lobby"}

## ESEMPIO 3

Nell'esempio 3 vengono restituiti tutti i telefoni di area comune con un nome visualizzato di Active Directory che inizia con i caratteri "Building 14". A tale scopo, viene chiamato il cmdlet **Get-CsCommonAreaPhone** insieme al parametro Filter e al valore di filtro {DisplayName -like "Building 14\*"}. Il valore di filtro utilizza l'operatore -like e la stringa con carattere jolly "Building 14\*" per limitare i dati restituiti ai telefoni in cui la proprietà DisplayName inizia con "Building 14", ad esempio "Building 14 Lobby", "Building 14 Cafeteria" e così via.

    Get-CsCommonAreaPhone  -Filter {DisplayName -like "Building 14*"}

## ESEMPIO 4

Nell'esempio 4, viene restituito un telefono singolo dell'area comune: il telefono con proprietà LineUri uguale a "tel:+14255551234". Poiché le proprietà LineUri devono essere univoche, questo comando non restituisce mai più di un elemento.

    Get-CsCommonAreaPhone  -Filter {LineUri -eq "tel:+14255551234"}

## ESEMPIO 5

Il comando riportato nell'esempio 5 restituisce le informazioni su tutti i telefoni delle aree comuni a cui non è stato assegnato un dial plan. È possibile eseguire questa operazione utilizzando il parametro Filter e il valore di filtro {DialPlan -eq $Null}, in modo da limitare i dati restituiti ai telefoni con proprietà DialPlan uguale a un valore Null. Se a un telefono delle aree comuni non è stato esplicitamente assegnato un dial plan, il telefono utilizzerà automaticamente il dial plan globale o, se disponibile, il dial plan assegnato al sito.

    Get-CsCommonAreaPhone -Filter {DialPlan -eq $Null}

## ESEMPIO 6

Nell'esempio 6 viene restituita una raccolta di tutti i telefoni di area comune che dispongono di un oggetto contatto nell'unità organizzativa Telecommunications in Servizi di dominio Active Directory. A tale scopo, viene chiamato il cmdlet **Get-CsCommonAreaPhone** insieme al parametro OU. Il valore del parametro limita gli oggetti restituiti ai telefoni che hanno nell'unità organizzativa oggetti contatto con il nome distinto ou=Telecommunications,dc=litwareinc,dc=com.

    Get-CsCommonAreaPhone -OU "ou=Telecommunications,dc=litwareinc,dc=com"

## Descrizione dettagliata

I telefoni di area comune sono telefoni IP non associati a un singolo utente. Invece di essere installati in qualche ufficio, tali telefoni sono generalmente posizionati nelle sale d'attesa degli edifici, nelle mense, nelle aree riservate ai dipendenti, nelle sale riunioni e in altri luoghi in cui è probabile si ritrovino molte persone. Per gli amministratori questa è una sfida gestionale, in quanto l'utilizzo dei telefoni in Lync Server viene normalmente gestito mediante criteri vocali e dial plan assegnati a utenti singoli. Ai telefoni di area comune non viene assegnato un utente specifico.

La soluzione consiste nel creare oggetti contatto di Active Directory per tutti i telefoni delle aree comuni. Gli oggetti contatto possono essere creati tramite il cmdlet **New-CsCommonAreaPhone**. Analogamente agli account utente, è possibile assegnare criteri e piani vocali agli oggetti contatto. Di conseguenza, sarà possibile mantenere il controllo sui telefoni delle aree comuni anche se i telefoni non sono associati a un singolo utente. Per impedire ad esempio alle persone di trasferire o parcheggiare le chiamate da un telefono delle aree comuni, è possibile creare un criterio vocale che impedisca il trasferimento e il parcheggio delle chiamate e quindi assegnarlo al telefono delle aree comuni. Oppure, in modo più corretto, all'oggetto contatto che rappresenta il telefono dell'area comune. Ad esempio, con il comando seguente è possibile assegnare il criterio vocale CommonAreaPhoneVoicePolicy a tutti i telefoni delle aree comuni:

Get-CsCommonAreaPhone | Grant-CsVoicePolicy –PolicyName "CommonAreaPhoneVoicePolicy"

Il cmdlet **Get-CsCommonAreaPhone** consente di recuperare informazioni sui telefoni delle aree comuni configurati per l'utilizzo all'interno dell'organizzazione. Se si chiama il cmdlet **Get-CsCommonAreaPhone** senza alcun parametro, il cmdlet restituirà informazioni su tutti i telefoni delle aree comuni. I parametri facoltativi mettono a disposizione diversi metodi per filtrare le informazioni. È ad esempio possibile restituire tutti i telefoni delle aree comuni contenenti oggetti contatto in una specifica unità organizzativa (OU) o tutti gli oggetti contatto presenti in un determinato edificio.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsCommonAreaPhone** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Le autorizzazioni per l'esecuzione di questo cmdlet per siti o unità organizzative di Active Directory specifiche possono essere assegnate tramite il cmdlet **Grant-CsOUPermission**. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsCommonAreaPhone"}

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
<td><p>Consente di eseguire il cmdlet <strong>Get-CsCommonAreaPhone</strong> utilizzando credenziali alternative. Può essere necessario se l'account utilizzato per accedere a Windows non dispone dei privilegi necessari richiesti per utilizzare gli oggetti contatto.</p>
<p>Per utilizzare il parametro Credential, è prima di tutto necessario creare un oggetto PSCredential utilizzando il cmdlet <strong>Get-Credential</strong>. Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet <strong>Get-Credential</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente la connessione al controller di dominio specificato per recuperare le informazioni di contatto. Per connettersi a un controller di dominio specifico, includere il parametro DomainController seguito dal nome di dominio completo (FQDN) del computer, ad esempio atl-cs-001.litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro basato su attributi specifici di Lync Server. Ad esempio, è possibile limitare i dati restituiti agli oggetti contatto del telefono di area comune a cui è stato assegnato un criterio vocale specifico o ai contatti a cui non è assegnato un criterio vocale specifico.</p>
<p>Il parametro Filter utilizza la stessa sintassi di filtro Windows PowerShell su cu si basa il cmdlet <strong>Where-Object</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Identificatore univoco per il telefono dell'area comune. I telefoni delle aree comuni vengono identificati tramite il nome distinto (DN) Active Directory dell'oggetto contatto associato. Per impostazione predefinita, questi telefoni delle aree comuni utilizzano un identificatore univoco globale (GUID) come nome comune e pertanto presentano in genere un'identità simile alla seguente: CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com.</p></td>
</tr>
<tr class="odd">
<td><p><em>LdapFilter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro basato su attributi di Active Directory generici, ovvero attributi non specifici di Lync Server. Ad esempio, è possibile limitare i dati restituiti agli oggetti contatto assegnati a un reparto specifico o che si trovano in un determinato edificio.</p>
<p>Il parametro LdapFilter utilizza il linguaggio di query LDAP per la creazione dei filtri. Ad esempio, un filtro che restituisce solo gli oggetti contatto che rappresentano i telefoni delle aree comuni della città di Redmond potrebbe essere analogo al seguente:</p>
<p>-LDAPFilter &quot;l=Redmond&quot;</p>
<p>Nel filtro precedente la lettera elle minuscola &quot;l&quot; rappresenta l'attributo di Active Directory (località), &quot;=&quot; rappresenta l'operatore di confronto (uguale a) e &quot;Redmond&quot; rappresenta il valore di filtro.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Consente di restituire gli oggetti contatto di una specifica unità organizzativa di Active Directory. Il parametro OU restituisce i dati dell'unità organizzativa specificata e delle relative unità organizzative figlio. Se ad esempio l'unità organizzativa Finance contiene due unità organizzative figlio, AccountsPayable e AccountsReceivable, verranno restituite le informazioni relative ai telefoni delle aree comuni di ciascuna unità organizzativa.</p>
<p>Per specificare un'unità organizzativa occorre utilizzare il nome distinto del contenitore, ad esempio: -OU &quot;OU=Finance,dc=litwareinc,dc=com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>Consente di limitare il numero di record restituiti da un comando. Per restituire ad esempio sette telefoni delle aree comuni (indipendentemente dal numero di telefoni delle aree comuni presenti nella foresta), includere il parametro ResultSize e impostarne il valore su 7. Non esiste alcun modo per stabilire quali telefoni saranno scelti tra i sette restituiti. Se si imposta il parametro ResultSize su 7, ma la foresta in uso contiene solo tre telefoni delle aree comuni, il comando restituirà i tre telefoni e terminerà senza errori.</p>
<p>La dimensione del risultato può essere impostata su qualsiasi numero intero compreso tra 0 e 2147483647 (compresi). Se l'impostazione è 0 il comando viene eseguito ma non restituisce dati.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa. Il cmdlet **Get-CsCommonAreaPhone** accetta un valore stringa da pipeline che rappresenta l'identità del telefono delle aree comuni.

## Tipi restituiti

Il cmdlet **Get-CsCommonAreaPhone** restituisce le istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact.

## Vedere anche

#### Ulteriori risorse

[Move-CsCommonAreaPhone](move-cscommonareaphone.md)  
[New-CsCommonAreaPhone](new-cscommonareaphone.md)  
[Remove-CsCommonAreaPhone](remove-cscommonareaphone.md)  
[Set-CsCommonAreaPhone](set-cscommonareaphone.md)

