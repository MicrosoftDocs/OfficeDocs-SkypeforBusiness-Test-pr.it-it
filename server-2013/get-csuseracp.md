---
title: Get-CsUserAcp
TOCTitle: Get-CsUserAcp
ms:assetid: de65eafe-e306-4ada-8509-9688e81491f9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398978(v=OCS.15)
ms:contentKeyID: 49302196
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsUserAcp

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui provider di servizi di audioconferenza assegnati a un utente oppure a un gruppo di utenti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsUserAcp [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-Filter <String>] [-LdapFilter <String>] [-ResultSize <Unlimited>]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 restituisce informazioni sui provider di servizi di audioconferenza per tutti gli utenti presenti nell'organizzazione.

    Get-CsUserAcp

## ESEMPIO 2

Nell'esempio 2 vengono restituite informazioni sui provider di servizi di audioconferenza per un singolo utente, ovvero l'utente con l'identità Ken Myer. In questo caso, l'identità viene specificata utilizzando il nome visualizzato dell'utente in Active Directory.

    Get-CsUserAcp -Identity "Ken Myer"

## ESEMPIO 3

Nell'esempio 3 vengono restituite informazioni per tutti gli utenti a cui è stato assegnato almeno un provider di servizi di audioconferenza. A tale scopo, il parametro Filter viene incluso con il valore di filtro {AcpInfo –ne $Null}. Questo valore di filtro limita i dati restituiti agli utenti per i quali il valore della proprietà AcpInfo non è uguale a un valore null. Per restituire informazioni sugli utenti ai quali non è stato assegnato un provider di servizi di audioconferenza, utilizzare il seguente valore di filtro:

{AcpInfo –eq $Null}

    Get-CsUserAcp -Filter {AcpInfo -ne $Null}

## ESEMPIO 4

Nell'esempio 4 vengono restituite informazioni sui provider di servizi di audioconferenza per qualsiasi utente a cui sia stato assegnato il provider di servizi di audioconferenza Fabrikam ACP. Per eseguire questa attività, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsUserAcp** senza alcun parametro per restituire informazioni sui provider di servizi di audioconferenza per tutti gli utenti presenti nell'organizzazione. Queste informazioni vengono quindi inviate tramite pipe al cmdlet **Where-Object**, che seleziona qualsiasi utente la cui proprietà AcpInfo includa (-match) il valore stringa "Fabrikam ACP".

    Get-CsUserAcp | Where-Object {$_.AcpInfo -match "Fabrikam ACP"}

## ESEMPIO 5

Nell'esempio 5 vengono visualizzate informazioni dettagliate sui provider di servizi di audioconferenza assegnati all'utente Ken Myer. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsUserAcp** per restituire le informazioni sui provider di servizi di audioconferenza per Ken Myer. Tali dati vengono quindi inviati tramite pipe al cmdlet **Select-Object**, che utilizza il parametro ExpandProperty per espandere il valore della proprietà AcpInfo. Quando il valore di una proprietà è espanso, tutte le informazioni archiviate in quel valore vengono visualizzate in un formato più leggibile.

    Get-CsUserAcp -Identity "Ken Myer" | Select-Object -ExpandProperty AcpInfo

## Descrizione dettagliata

Un provider di servizi di audioconferenza è una società terza che fornisce servizi di conferenza alle organizzazioni. Tra l'altro, i provider di servizi di audioconferenza consentono agli utenti in trasferta non connessi alla rete aziendale o a Internet di accedere ai contenuti audio di una conferenza o di una riunione. Tali provider offrono spesso servizi di qualità elevata quali traduzione immediata, trascrizione e assistenza diretta di un operatore durante la conferenza.

Lync Server non consente l'integrazione completa con i provider di servizi di audioconferenza. I cmdlet **CsUserAcp** consentono agli amministratori di impostare un numero telefonico e un passcode, nonché di configurare altre informazioni utilizzabili per l'integrazione dei provider di servizi di audioconferenza ogni volta che un utente pianifica una riunione. Poiché tuttavia tali cmdlet non sono specifici per la versione locale di Lync Server ma devono essere utilizzati principalmente con Lync Online, non verrà garantita ulteriore integrazione con i provider di servizi di audioconferenza oltre all'assegnazione dei valori delle proprietà.

Il cmdlet **Get-CsUserAcp** consente di restituire informazioni sui provider di servizi di audioconferenza che sono stati assegnati a un utente oppure a un gruppo di utenti. Per restituire informazioni su tali provider per un singolo utente, è sufficiente includere il parametro Identity seguito dall'identità dell'utente le cui informazioni si desidera vengano restituite. Per restituire informazioni per più utenti, utilizzare il parametro LdapFilter o Filter. Il parametro LdapFilter consente di utilizzare attributi generici di Active Directory, quali ad esempio il reparto o la qualifica, quando si specificano le informazioni sull'account utente. Il valore "Title=Accountant" ad esempio fa sì che vengano restituite esclusivamente le informazioni relative agli utenti con la qualifica (Title) di contabile (Accountant). Il parametro Filter consente di utilizzare attributi specifici di Lync Server (ad esempio, VoicePolicy o EnterpriseVoiceEnabled) per filtrare i dati restituiti. Ad esempio, il valore di filtro {EnterpriseVoiceEnabled –eq $True} limita gli account utente restituiti dal cmdlet **Get-CsUserAcp** agli utenti che sono stati abilitati per VoIP aziendale.

In alternativa, è possibile chiamare il cmdlet **Get-CsUserAcp** senza alcun parametro per restituire le informazioni relative ai provider di servizi di audioconferenza per tutti gli utenti. Si noti che il cmdlet **Get-CsUserAcp** restituisce informazioni su tali provider per tutti gli utenti, inclusi quelli che non sono stati abilitati per Lync Server.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsUserAcp** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalReadOnlyAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsUserAcp"}

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
<td><p>Consente di eseguire il cmdlet <strong>Get-CsUserAcp</strong> utilizzando credenziali alternative. Può essere necessario se l'account utilizzato per accedere a Windows non dispone dei privilegi necessari richiesti per lavorare con gli oggetti contatto.</p>
<p>Per poter utilizzare il parametro Credential, è innanzitutto necessario creare un oggetto PSCredential mediante il cmdlet <strong>Get-Credential</strong>. Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet <strong>Get-Credential</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro basato su attributi specifici di Lync Server. Ad esempio, è possibile limitare i dati restituiti agli utenti a cui è assegnato uno specifico criterio vocale o agli utenti a cui tale criterio vocale specifico non è assegnato.</p>
<p>Il parametro Filter utilizza la stessa sintassi di filtro Windows PowerShell impiegata dal cmdlet <strong>Where-Object</strong>. Ad esempio, di seguito è riportato un filtro che restituisce solo gli utenti che sono stati abilitati per VoIP aziendale e dove EnterpriseVoiceEnabled rappresenta l'attributo di Servizi di dominio Active Directory, -eq rappresenta l'operatore di confronto (uguale a) e $True (una variabile di Windows PowerShell predefinita) rappresenta il valore di filtro:</p>
<p>{EnterpriseVoiceEnabled -eq $True}</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Indica l'identità dell'account utente da recuperare. L'identità di un utente può essere specificata utilizzando uno dei quattro formati seguenti: 1) l'indirizzo SIP dell'utente, 2) il nome dell'entità utente (UPN, User Principal Name), 3) il nome di dominio e il nome di accesso dell'utente nella forma dominio\accesso (ad esempio litwareinc\davidegarghentini), 4) il nome visualizzato di Servizi di dominio Active Directory dell'utente (ad esempio Davide Garghentini). È possibile fare riferimento a un account utente anche utilizzando il nome distinto Active Directory dell'utente.</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come identità utente. Ad esempio, il valore Identity &quot;* Smith&quot; restituisce tutti gli utenti con un nome visualizzato che termina con il valore stringa &quot; Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>LdapFilter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro basato su attributi generici di Active Directory, ovvero attributi non specifici di Lync Server. Ad esempio, è possibile limitare i dati restituiti agli utenti che lavorano in un determinato reparto oppure agli utenti che hanno un determinato manager o una determinata qualifica.</p>
<p>Il parametro LdapFilter utilizza il linguaggio di query LDAP per la creazione dei filtri. Ad esempio, un filtro che restituisce solamente gli utenti che lavorano nella città di Redmond potrebbe essere simile al seguente: &quot;l=Redmond&quot;, dove &quot;l&quot; (una elle minuscola) rappresenta l'attributo di Active Directory (località), &quot;=&quot; rappresenta l'operatore di confronto (uguale a) e &quot;Redmond&quot; rappresenta il valore di filtro.</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>Consente di limitare il numero di record restituiti da un comando. Ad esempio, per restituire sette utenti (indipendentemente dal numero di utenti nella foresta), includere il parametro ResultSize e impostarne il valore su 7. Non c'è modo di stabilire quali saranno i sette utenti restituiti. Se si imposta ResultSize su 7 ma la foresta contiene solo tre utenti, il comando restituisce tali tre utenti e viene completato senza errori.</p>
<p>La dimensione del risultato può essere impostata su qualsiasi numero intero compreso tra 0 e 2147483647 (compresi). Se l'impostazione è 0 il comando viene eseguito ma non restituisce dati.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa. Il cmdlet **Get-CsUserAcp** accetta un valore stringa da pipeline che rappresenta l'identità di un account utente abilitato per Lync Server.

## Tipi restituiti

Il cmdlet **Get-CsUserAcp** restituisce istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUserAcp.

## Vedere anche

#### Ulteriori risorse

[Remove-CsUserAcp](remove-csuseracp.md)  
[Set-CsUserAcp](set-csuseracp.md)

