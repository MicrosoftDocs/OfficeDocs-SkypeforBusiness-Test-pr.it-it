---
title: Grant-CsExternalAccessPolicy
TOCTitle: Grant-CsExternalAccessPolicy
ms:assetid: 451fef34-3021-4261-8494-b36420b04c82
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425942(v=OCS.15)
ms:contentKeyID: 49300375
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsExternalAccessPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di assegnare un criterio di accesso esterno a un utente o a un gruppo di utenti. I criteri di accesso esterno determinano se gli utenti possono eseguire le operazioni seguenti: 1) comunicare con utenti che dispongono di account SIP (Session Initiation Protocol) con un'organizzazione federata, 2) comunicare con utenti che dispongono di account SIP con un provider di servizi di messaggistica istantanea pubblico come MSN e 3) accedere a Lync Server tramite Internet, senza dover effettuare l'accesso alla rete interna. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Grant-CsExternalAccessPolicy -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-PolicyName <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene assegnato il criterio di accesso esterno RedmondAccessPolicy all'utente con il nome visualizzato di Active Directory Ken Myer.

    Grant-CsExternalAccessPolicy -Identity "Ken Myer" -PolicyName RedmondAccessPolicy

## ESEMPIO 2

Il comando riportato nell'esempio 2 assegna il criterio di accesso esterno RedmondAccessPolicy a tutti gli utenti che lavorano nella città di Redmond. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsUser** e il parametro LdapFilter per restituire una raccolta di tutti gli utenti che lavorano a Redmond. Il valore di filtro "l=Redmond" garantisce che vengano restituiti solo i dati relativi agli utenti che lavorano nella città di Redmond (la L minuscola nel filtro rappresenta la località). La raccolta viene quindi inviata tramite pipe al cmdlet **Grant-CsExternalAccessPolicy**, che assegna il criterio RedmondAccessPolicy a ogni utente della raccolta.

    Get-CsUser -LdapFilter "l=Redmond" | Grant-CsExternalAccessPolicy -PolicyName RedmondAccessPolicy

## ESEMPIO 3

Nell'esempio 3 a tutti gli utenti con posizione professionale "Sales Representative" viene assegnato il criterio di accesso esterno SalesAccessPolicy. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsUser** e il parametro LdapFilter per restituire una raccolta di tutti gli utenti Sales Representative. Il valore di filtro "Title=Sales Representative" garantisce che nella raccolta restituita siano inclusi solo gli utenti con posizione professionale "Sales Representative". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Grant-CsExternalAccessPolicy**, che assegna il criterio SalesAccessPolicy a ogni utente della raccolta.

    Get-CsUser -LdapFilter "Title=Sales Representative" | Grant-CsExternalAccessPolicy -PolicyName SalesAccessPolicy

## ESEMPIO 4

Il comando riportato nell'esempio 4 assegna il criterio di accesso esterno BasicAccessPolicy a tutti gli utenti a cui non è stato assegnato esplicitamente un criterio per utente, ovvero agli utenti attualmente controllati da un criterio del sito o dal criterio globale. A tale scopo, vengono utilizzati il cmdlet **Get-CsUser** e il parametro Filter per restituire il set di utenti appropriato. Il valore di filtro {ExternalAccessPolicy -eq $Null} garantisce che vengano restituiti solo i dati relativi agli account utente la cui proprietà ExternalAccessPolicy è uguale a (-eq) un valore Null ($Null). Per definizione, ExternalAccessPolicy sarà Null solo se agli utenti non è stato assegnato un criterio per utente.

    Get-CsUser -Filter {ExternalAccessPolicy -eq $Null} | Grant-CsExternalAccessPolicy -PolicyName BasicAccessPolicy

## ESEMPIO 5

Nell'esempio 5 viene assegnato il criterio di accesso esterno USAccessPolicy a tutti gli utenti che dispongono di account nell'unità organizzativa (OU) US. Il comando chiama innanzitutto il cmdlet **Get-CsUser** e il parametro OU. Il valore "ou=US,dc=litwareinc,dc=com" del parametro garantisce che vengano restituiti solo i dati relativi agli account utente presenti nell'unità organizzativa US. La raccolta restituita viene quindi inviata tramite pipe al cmdlet **Grant-CsExternalAccessPolicy**, che assegna il criterio USAccessPolicy a ogni utente della raccolta.

    Get-CsUser -OU "ou=US,dc=litwareinc,dc=com" | Grant-CsExternalAccessPolicy -PolicyName USAccessPolicy

## ESEMPIO 6

Nell'esempio 6 viene annullata l'assegnazione dei criteri di accesso esterno per utente precedentemente assegnati a qualsiasi utente abilitato per Lync Server. A tale scopo, il comando chiama il cmdlet **Get-CsUser** (senza parametri aggiuntivi) per restituire una raccolta di tutti gli utenti abilitati per Lync Server. La raccolta viene inviata tramite pipe al cmdlet **Grant-CsExternalAccessPolicy**, che utilizza la sintassi "-PolicyName $Null" per rimuovere eventuali criteri di accesso esterno per utente precedentemente assegnati a questi utenti.

    Get-CsUser | Grant-CsExternalAccessPolicy -PolicyName $Null

## Descrizione dettagliata

Quando si installa Lync Server, agli utenti è consentito unicamente lo scambio reciproco di messaggi istantanei e di informazioni sulla presenza: per impostazione predefinita, è possibile comunicare solo con altri utenti che dispongono di account SIP in Servizi di dominio Active Directory. Gli utenti non possono inoltre accedere a Lync Server tramite Internet, ma devono effettuare l'accesso alla rete interna per poter quindi accedere a Lync Server.

Tutto ciò potrebbe soddisfare le esigenze di comunicazione. In caso contrario, è possibile utilizzare i criteri di accesso esterno per estendere la possibilità degli utenti di comunicare e collaborare. Con i criteri di accesso esterno è possibile concedere (o revocare) agli utenti la possibilità di eseguire una o tutte le operazioni seguenti:

1\. Comunicare con persone che dispongono di account SIP con un'organizzazione federata. La sola abilitazione della federazione non offrirà automaticamente agli utenti questa funzionalità. È invece necessario abilitare la federazione, quindi assegnare agli utenti il criterio di accesso esterno che concede il diritto di comunicare con utenti federati.

2\. Comunicare con persone che dispongono di account SIP con un servizio di messaggistica istantanea pubblico come MSN.

3\. Accedere a Lync Server tramite Internet, senza dover prima effettuare l'accesso alla rete interna. Ciò consente agli utenti di utilizzare Lync e di accedere a Lync Server da un Internet café o da un'altra postazione remota.

Quando si installa Lync Server, viene creato automaticamente un criterio di accesso esterno globale. Oltre a questo criterio globale, è possibile utilizzare il cmdlet **New-CsExternalAccessPolicy** per creare criteri di accesso esterno aggiuntivi configurati nell'ambito del sito o per utente.

Quando un criterio viene creato nell'ambito del sito, tale criterio viene automaticamente assegnato al sito in questione; ad esempio, un criterio di accesso esterno con identità site:Redmond viene automaticamente assegnato al sito Redmond. Al contrario, i criteri creati nell'ambito per utente non vengono assegnati automaticamente agli utenti. Questi criteri devono essere assegnati esplicitamente a un utente o a un gruppo di utenti. L'assegnazione di criteri per utente è il compito del cmdlet **Grant-CsExternalAccessPolicy**.

I criteri per utente hanno sempre la precedenza sui criteri del sito e sul criterio globale. Ad esempio, si supponga di aver creato un criterio per utente che consente la comunicazione con gli utenti federati e di assegnare tale criterio a Ken Myer. Finché il criterio rimane valido, Ken potrà comunicare con gli utenti federati, anche se questo tipo di comunicazione non è consentito dal criterio del sito di Ken o dal criterio globale, perché le impostazioni nel criterio per utente hanno la precedenza.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Grant-CsExternalAccessPolicy** in locale: RTCUniversalUserAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsExternalAccessPolicy"}

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
<td><p>Identità dell'account utente a cui assegnare il criterio. Le identità utente possono essere specificate con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP dell'utente; 2) l'UPN (User Principal Name) dell'utente; 3) il nome di dominio e il nome di accesso dell'utente, nel formato dominio\accesso (ad esempio, litwareinc\kenmyer); 4) il nome visualizzato Active Directory dell'utente (ad esempio, Ken Myer). Le identità utente possono essere referenziate anche utilizzando il nome distinto dell'utente in Active Directory.</p>
<p>Inoltre, è possibile utilizzare l'asterisco (*) per specificare l'identità dell'utente. Ad esempio, l'identità &quot;* Smith&quot; restituisce tutti gli utenti con un nome visualizzato che termina con il valore stringa &quot; Smith&quot;.</p></td>
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
<td><p>Consente di specificare il nome di dominio completo (FQDN) di un controller di dominio da contattare durante l'assegnazione del nuovo criterio. Se questo parametro non viene specificato, il cmdlet <strong>Grant-CsExternalAccessPolicy</strong> contatterà il primo controller di dominio disponibile.</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di passare un oggetto utente attraverso la pipeline che rappresenta l'utente a cui viene assegnato il criterio. Per impostazione predefinita, il cmdlet <strong>Grant-CsExternalAccessPolicy</strong> non passa alcun oggetto attraverso la pipeline.</p></td>
</tr>
<tr class="odd">
<td><p><em>PolicyName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il &quot;Nome&quot; del criterio da assegnare. PolicyName corrisponde all'identità del criterio meno l'ambito del criterio (il prefisso &quot;tag:&quot; ). Ad esempio, un criterio con Identity tag:Redmond dispone di un PolicyName uguale a Redmond; un criterio con Identity tag:RedmondAccessPolicy dispone di un PolicyName uguale a RedmondAccessPolicy.</p>
<p>Per annullare l'assegnazione di un criterio per utente precedentemente assegnato a un utente, impostare il parametro PolicyName su $Null.</p></td>
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

Valore stringa oppure oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Grant-CsExternalAccessPolicy** accetta l'input da pipeline di valori stringa che rappresentano l'identità di un account utente. Il cmdlet accetta inoltre l'input da pipeline di oggetti utente.

## Tipi restituiti

Per impostazione predefinita, il cmdlet **Grant-CsExternalAccessPolicy** non restituisce oggetti o valori. Se però si include il parametro PassThru, il cmdlet restituirà istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSUserOrAppContact.

## Vedere anche

#### Ulteriori risorse

[Get-CsExternalAccessPolicy](get-csexternalaccesspolicy.md)  
[New-CsExternalAccessPolicy](new-csexternalaccesspolicy.md)  
[Remove-CsExternalAccessPolicy](remove-csexternalaccesspolicy.md)  
[Set-CsExternalAccessPolicy](set-csexternalaccesspolicy.md)

