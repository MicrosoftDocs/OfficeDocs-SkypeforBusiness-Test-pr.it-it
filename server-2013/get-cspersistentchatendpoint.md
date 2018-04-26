---
title: Get-CsPersistentChatEndpoint
TOCTitle: Get-CsPersistentChatEndpoint
ms:assetid: 2c37edd6-6892-4b2d-8586-6f59ab668d4b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204764(v=OCS.15)
ms:contentKeyID: 49300035
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPersistentChatEndpoint

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sugli endpoint di Chat persistente configurati per l'utilizzo nell'organizzazione. Un endpoint di Chat persistente è un oggetto contatto Active Directory che fornisce un URL descrittivo per un pool di Chat persistente di Lync Server 2013. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsPersistentChatEndpoint [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-LdapFilter <String>] [-OU <OUIdParameter>] [-PersistentChatPoolFqdn <Fqdn>] [-ResultSize <Unlimited>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce informazioni su tutti gli endpoint di Chat persistente configurati per l'utilizzo nell'organizzazione.

    Get-CsPersistentChatEndpoint

## Esempio 2

Nell'esempio 2 viene utilizzato il parametro Filter per restituire informazioni sull'endpoint di Chat persistente con identità (Identity) "sip:pce@litwareinc.com". In questo caso viene utilizzato l'indirizzo SIP per l'identità.

    Get-CsPersistentChatEndpoint -Identity "sip:pce@litwareinc.com"

## Esempio 3

Nell'esempio 3 vengono restituite informazioni su tutti gli endpoint di Chat persistente configurati per l'utilizzo nel pool di Chat persistente atl-pcpool-001.litwareinc.com. Per ottenere questo risultato, viene incluso il parametro PoolFqdn seguito dal nome di dominio completo del pool di Chat persistente.

    Get-CsPersistentChatEndpoint -PersistentChatPoolFqdn atl-pcpool-001.litwareinc.com

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Quando si installa il servizio Chat persistente, viene creato automaticamente un endpoint per ogni pool di Chat persistente. Questo endpoint è un oggetto contatto di Active Directory che gestisce l'URI del pool. Se tutti gli utenti eseguono Lync 2013, questo dovrebbe essere sufficiente.

Se tuttavia sono presenti utenti che eseguono client legacy, ad esempio Microsoft Lync 2010, è possibile che per tali utenti gli URI di Chat persistente predefiniti siano difficili da gestire e utilizzare per far puntare il client legacy al pool. Per questo motivo gli amministratori possono utilizzare il cmdlet [New-CsPersistentChatEndpoint](new-cspersistentchatendpoint.md) per creare per il pool un oggetto contatto aggiuntivo che fornisca un URI più descrittivo e più facile da utilizzare. Il cmdlet **Get-CsPersistentChatEndpoint** consente di restituire informazioni su tutti gli endpoint di Chat persistente configurati per l'utilizzo nell'organizzazione.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPersistentChatEndpoint"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsPersistentChatEndpoint** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Consente di eseguire il cmdlet <strong>Get-CsPersistentChatEndpoint</strong> utilizzando credenziali alternative. Questo può essere necessario se l'account utilizzato per eseguire l'accesso a Windows non dispone dei privilegi richiesti per gestire gli oggetti utente.</p>
<p>Per utilizzare il parametro Credential, è necessario creare innanzitutto un oggetto PSCredential utilizzando il cmdlet <strong>Get-Credential</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di eseguire la connessione al controller di dominio specificato per recuperare le informazioni sull'utente. Per la connessione a un controller di dominio specifico, includere il parametro DomainController seguito dal nome di dominio completo (FQDN), ad esempio:</p>
<p>-DomainController &quot;atl-dc-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro basato su attributi specifici di Lync Server. È ad esempio possibile limitare i dati restituiti agli endpoint di Chat persistente a cui è stato assegnato un criterio vocale specifico o agli endpoint a cui non è stato assegnato un criterio vocale specifico.</p>
<p>Il parametro Filter utilizza la stessa sintassi di filtro di Windows PowerShell utilizzata dal cmdlet <strong>Where-Object</strong>. Ad esempio, un filtro che restituisce solo gli endpoint a cui è stato assegnato un criterio di conferenza per utente sarà simile al seguente, dove ConferencingPolicy rappresenta l'attributo di Active Directory, -ne rappresenta l'operatore di confronto (diverso da) e $Null (una variabile incorporata di Windows PowerShell) rappresenta il valore di filtro:</p>
<p>-Filter {ConferencingPolicy -ne $Null}</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Identificatore univoco dell'endpoint di Chat persistente da restituire. Le identità (Identity) degli endpoint in genere vengono specificate utilizzando l'indirizzo SIP o il nome visualizzato dell'endpoint, ad esempio:</p>
<p>-Identity &quot;sip:pcEndpoint1@litwareinc.com&quot;</p>
<p>È tuttavia possibile utilizzare anche l'identità completa dell'endpoint, ad esempio:</p>
<p>-Identity &quot;CN={33e5014b-dcba-46b5-9bf7-48f4d5fca69d}, CN=Application Contacts,CN=RTC Service,CN=Services,CN=Configuration,DC=litwareinc,DC=com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>LdapFilter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro basato su attributi generici di Active Directory, ovvero attributi non specifici di Lync Server. Poiché gli endpoint di Chat persistente dispongono di pochi attributi non Lync Server, questo parametro riveste un'importanza minima.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Consente di ottenere solo gli account utente di una specifica unità organizzativa o di un contenitore. Poiché i nuovi endpoint di Chat persistente vengono tutti creati nello stesso contenitore di Active Directory (ApplicationContacts/RTC Service/Services/Configuration), questo parametro riveste un'importanza minima.</p></td>
</tr>
<tr class="odd">
<td><p><em>PersistentChatPoolFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del pool di Chat persistente associato all'endpoint di Chat persistente.</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>Consente di limitare il numero di record restituiti dal cmdlet. Per restituire ad esempio sette contatti (indipendentemente dal numero di utenti contenuti nella foresta), includere il parametro ResultSize e impostare il relativo valore su 7. Si noti che non è possibile stabilire quali saranno i sette utenti restituiti.</p>
<p>La dimensione del risultato può essere impostata su un numero intero compreso tra 0 e 2147483647, estremi inclusi. Se si imposta il parametro su 0, il comando verrà eseguito ma non restituirà dati. Se si imposta ResultSize su 7 ma la foresta include solo tre contatti, il comando restituirà i tre contatti e verrà completato senza errori.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Valore stringa. Il cmdlet **Get-CsPersistentChatEndpoint** può accettare un valore stringa che rappresenta l'identità o l'indirizzo SIP di un endpoint di Chat persistente.

## Tipi restituiti

Il cmdlet **Get-CsPersistentChatEndpoint** restituisce istanze della classe Microsoft.Rtc.Management.ADConnect.Schema.OCSPersistentChatContact.

## Vedere anche

#### Ulteriori risorse

[New-CsPersistentChatEndpoint](new-cspersistentchatendpoint.md)  
[Remove-CsPersistentChatEndpoint](remove-cspersistentchatendpoint.md)

