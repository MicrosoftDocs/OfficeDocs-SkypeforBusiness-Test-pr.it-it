---
title: Grant-CsPresencePolicy
TOCTitle: Grant-CsPresencePolicy
ms:assetid: 756c08a7-26b0-4ea8-816b-b33ebcac51aa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398571(v=OCS.15)
ms:contentKeyID: 49301004
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsPresencePolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Concede un criterio di presenza per utente a un utente o a un gruppo di utenti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Grant-CsPresencePolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 viene assegnato il criterio di presenza per utente RedmondPresencePolicy a un singolo utente, quello con identità Davide Garghentini.

    Grant-CsPresencePolicy -Identity "Ken Myer" -PolicyName "RedmondPresencePolicy"

## ESEMPIO 2

Nell'esempio 2 il criterio di presenza RedmondPresencePolicy viene assegnato a tutti gli utenti che dispongono di account nell'unità organizzativa Redmond in Servizi di dominio Active Directory. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsUser** e il parametro OU per restituire una raccolta di tutti gli account utente presenti nell'unità organizzativa Redmond (OU=Redmond,dc=litwareinc,dc=com). La raccolta viene quindi inviata tramite pipe al cmdlet **Grant-CsPresencePolicy**, che assegna il criterio RedmondPresencePolicy a ogni utente della raccolta.

    Get-CsUser -OU "OU=Redmond,dc=litwareinc,dc=com" | Grant-CsPresencePolicy -PolicyName "RedmondPresencePolicy"

## ESEMPIO 3

Nell'esempio 3 viene assegnato il criterio RedmondPresencePolicy a tutti gli utenti che lavorano nella città di Redmond. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsUser** e il parametro LdapFilter per restituire una raccolta di tutti gli utenti che lavorano a Redmond. Il valore di filtro "l=Redmond" limita i dati restituiti agli utenti di Redmond. Nel linguaggio di query LDAP l (elle minuscola) è l'abbreviazione di "località" e corrisponde quindi alla città. La raccolta recuperata viene quindi inviata tramite pipe al cmdlet **Grant-CsPresencePolicy**, che assegna il criterio RedmondPresencePolicy a ogni utente incluso nella raccolta.

    Get-CsUser -LdapFilter "l=Redmond" | Grant-CsPresencePolicy -PolicyName "RedmondPresencePolicy"

## ESEMPIO 4

Con il comando mostrato nell'esempio 4 viene annullata l'assegnazione di tutti i criteri di presenza per utente precedentemente assegnati agli utenti che lavorano a Redmond. Con una chiamata al cmdlet **Grant-CsPresencePolicy** con il parametro PolicyName impostato su un valore Null ($Null), il cmdlet rimuove qualsiasi criterio di presenza per utente assegnato agli utenti interessati dal comando.

    Get-CsUser -LdapFilter "l=Redmond" | Grant-CsPresencePolicy -PolicyName $Null

## Descrizione dettagliata

Le informazioni sulla presenza (che, tra l'altro, indicano se un contatto è disponibile a partecipare a una conversazione di messaggistica istantanea) sono di estrema importanza. Allo stesso tempo, tuttavia, le informazioni sulla presenza comportano un costo: maggiore è il numero delle sottoscrizioni di presenza, maggiore sarà la larghezza di banda da dedicare all'aggiornamento delle informazioni sulla presenza. Se la larghezza di banda rappresenta un problema, è possibile limitare il numero di sottoscrizioni di presenza disponibili per ciascun utente.

I cmdlet CsPresencePolicy consentono la gestione di due aspetti importanti delle sottoscrizioni di presenza, ovvero le richieste di sottoscrizione e le sottoscrizioni alle categorie. Quando si viene aggiunti all'elenco contatti di Lync di un'altra persona, il comportamento predefinito prevede la ricezione di una notifica popup in cui si viene informati di essere stati aggiunti a tale elenco. Fino alla chiusura della finestra popup visualizzata, ogni notifica viene considerata una richiesta di sottoscrizione. La proprietà MaxPromptedSubscriber del criterio di presenza consente di specificare il numero massimo di finestre di dialogo di notifica non risolte per ogni utente. Se un utente raggiunge il numero massimo consentito, non riceverà nuove notifiche di contatto, almeno fino alla risoluzione di alcune delle finestre di dialogo.

Le sottoscrizioni alle categorie rappresentano la richiesta di una categoria di informazioni specifica. Ad esempio, un'applicazione che richiede i dati del calendario. La proprietà MaxCategorySubscription consente agli amministratori di definire un limite per il numero di sottoscrizioni alle categorie disponibili per un utente.

Prima di Lync Server, le richieste di sottoscrizione e le sottoscrizioni alle categorie venivano gestite a livello globale. Grazie ai cmdlet **CsPresencePolicy**, attualmente è possibile gestire le sottoscrizioni di presenza nell'ambito globale, nell'ambito del sito o nell'ambito del singolo utente. In questo modo è possibile controllare l'utilizzo della larghezza di banda e, contemporaneamente, garantire per gli utenti l'accesso alle informazioni sulla presenza necessarie per le loro attività.

Quando si crea un criterio per utente, il criterio non viene automaticamente assegnato a nessuno. I criteri di presenza per utente devono invece essere assegnati esplicitamente agli utenti (o ai gruppi di utenti) eseguendo il cmdlet **Grant-CsPresencePolicy**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Grant-CsPresencePolicy** in locale: RTCUniversalUserAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsPresencePolicy"}

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
<td><p>Indica l'identità dell'account utente a cui assegnare il criterio di presenza. Le identità utente possono essere specificate utilizzando uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP dell'utente; 2) l'UPN (User Principal Name) dell'utente; 3) il nome di dominio e il nome di accesso dell'utente, nel formato dominio\accesso (ad esempio, litwareinc\davidegarghentini); 4) il nome visualizzato Active Directory dell'utente (ad esempio, Davide Garghentini). Le identità utente possono essere specificate anche utilizzando il nome distinto dell'utente in Active Directory.</p>
<p>È inoltre possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come valore Identity dell'utente. L'identità &quot;* Smith&quot; restituisce ad esempio tutti gli utenti con un nome visualizzato che termina con il valore stringa &quot;Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Identità del criterio per utente da assegnare, ad esempio: -PolicyName &quot;RedmondPresencePolicy&quot;. PolicyName corrisponde all'identità del criterio meno il prefisso &quot;tag:&quot;. Ad esempio, un criterio con identità &quot;tag:NorthAmericaPresencePolicy&quot; presenta un PolicyName uguale a &quot;NorthAmericaPresencePolicy&quot;.</p></td>
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
<td><p>Nome completo del controller di dominio da contattare durante l'assegnazione dei criteri. Ad esempio: -DomainController atl-dc-001.litwareinc.com.</p>
<p>Se non viene specificato, il cmdlet <strong>Grant-CsPresencePolicy</strong> contatterà il controller di dominio disponibile più vicino durante l'assegnazione del criterio.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di passare un oggetto utente attraverso la pipeline che rappresenta l'utente a cui viene assegnato il criterio. Per impostazione predefinita, il cmdlet <strong>Grant-CsPresencePolicy</strong> non passa alcun oggetto attraverso la pipeline.</p></td>
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

Valore stringa oppure oggetto Microsoft.Rtc.Management.WritebleConfig.Policy.Presence.PresencePolicy. Il cmdlet **Grant-CsPresencePolicy** accetta input inviato tramite pipeline di valori stringa che rappresentano l'identità (Identity) di un account utente. Il cmdlet accetta inoltre input inviato tramite pipeline di oggetti utente.

## Tipi restituiti

Per impostazione predefinita, il cmdlet **Grant-CsPresencePolicy** non restituisce oggetti o valori. Se tuttavia si include il parametro PassThru, il cmdlet restituisce istanze di Microsoft.Rtc.Management.ADConnect.Schema.OCSUserOrAppContact.

## Vedere anche

#### Ulteriori risorse

[Get-CsPresencePolicy](get-cspresencepolicy.md)  
[New-CsPresencePolicy](new-cspresencepolicy.md)  
[Remove-CsPresencePolicy](remove-cspresencepolicy.md)  
[Set-CsPresencePolicy](set-cspresencepolicy.md)

