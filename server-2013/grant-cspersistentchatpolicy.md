---
title: Grant-CsPersistentChatPolicy
TOCTitle: Grant-CsPersistentChatPolicy
ms:assetid: 58889550-167a-4267-9f3d-0f244e898599
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204907(v=OCS.15)
ms:contentKeyID: 49300635
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsPersistentChatPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Assegna a un utente un criterio di Chat persistente per utente. I criteri di questo tipo determinano se gli utenti sono autorizzati o meno ad accedere alle chat room di Chat persistente. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Grant-CsPersistentChatPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 assegna il criterio per utente RedmondUsersPersistentChatPolicy all'utente con nome visualizzato di Active Directory "Ken Myer".

    Grant-CsPersistentChatPolicy -Identity "Ken Myer" -PolicyName "RedmondUsersPersistentChatPolicy"

## Esempio 2

Nell'esempio 2 viene assegnato il criterio per utente RedmondUsersPersistentChatPolicy a tutti gli utenti che lavorano nel reparto IT. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsUser** con la proprietà LdapFilter. Il valore di filtro "Department=IT" restituisce solo i dati relativi agli utenti che lavorano nel reparto IT. La raccolta di utenti viene quindi inviata tramite pipe al cmdlet **Grant-CsPersistentChatPolicy**, che assegna il criterio RedmondUsersPersistentChatPolicy a ogni utente della raccolta.

    Get-CsUser -LdapFilter "Department=IT" | Grant-CsPersistentChatPolicy -PolicyName "RedmondUsersPersistentChatPolicy"

## Esempio 3

Nell'esempio 3 viene assegnato il criterio di Chat persistente per utente RedmondUsersPersistentChatPolicy a tutti gli utenti a cui attualmente non è assegnato un criterio di Chat persistente per utente. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsUser** e il parametro Filter. Il valore di filtro {PersistentChatPolicy –eq $Null} restituisce solo i dati relativi agli account utente in cui la proprietà PersistentChatPolicy è attualmente impostata su un valore Null ($Null). La raccolta di utenti viene quindi inviata tramite pipe al cmdlet **Grant-CsPersistentChatPolicy**, che assegna a ogni utente della raccolta il criterio RedmondUsersPersistentChatPolicy.

    Get-CsUser -Filter {PersistentChatPolicy -eq $Null} | Grant-CsPersistentChatPolicy -PolicyName "RedmondUsersPersistentChatPolicy"

## Esempio 4

Il comando riportato nell'esempio 4 annulla l'assegnazione del criterio di Chat persistente per utente RedmondUsersPersistentChatPolicy per gli utenti a cui è attualmente assegnato tale criterio. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsUser** e il parametro Filter per restituire una raccolta di utenti a cui è attualmente assegnato il criterio RedmondUsersPersistentChatPolicy. Il valore di filtro {PersistentChatPolicy –eq "RedmondUsersPersistentChatPolicy"} restituisce solo gli account utente in cui la proprietà PersistentChatPolicy è uguale a RedmondUsersPersistentChatPolicy. La raccolta viene quindi inviata tramite pipe al cmdlet **Grant-CsPersistentChatPolicy**, che annulla l'assegnazione del criterio per utente impostando la proprietà PersistentChatPolicy su un valore Null ($Null).

Dopo l'annullamento dell'assegnazione del criterio per utente, le funzionalità di Chat persistente degli utenti verranno gestite dal relativo criterio sito di Chat persistente, se definito, o dal criterio globale di Chat persistente.

    Get-CsUser -Filter {PersistentChatPolicy -eq "RedmondUsersPersistentChatPolicy"} | Grant-CsPersistentChatPolicy -PolicyName $Null

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Per impostazione predefinita, agli utenti non è concesso l'accesso al servizio Chat persistente. Questo accesso può essere concesso solo se l'utente è gestito da un criterio di Chat persistente che consente l'utilizzo del servizio. Quando si installa Lync 2013, tutti gli utenti sono gestiti da un criterio di Chat persistente globale in cui l'utilizzo di Chat persistente è disabilitato. Se si desidera concedere a tutti gli utenti l'accesso al servizio, è possibile impostare semplicemente la proprietà EnablePersistentChat di questo criterio globale su True. In alternativa, è possibile creare criteri aggiuntivi nell'ambito del sito o per utente e concedere così l'accesso a Chat persistente ad alcuni utenti negandolo invece ad altri.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsPersistentChatPolicy"}

**Pannello di controllo di Lync Server:** per assegnare un criterio di Chat persistente a un utente nel Pannello di controllo di Lync Server, fare doppio clic sull'account utente appropriato. Nella finestra di dialogo **Modifica utente di Lync Server** selezionare un criterio nell'elenco a discesa **Criteri di Chat persistente** e quindi fare clic su **Commit**.

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
<td><p>Indica l'identità dell'account utente a cui assegnare il criterio di Chat persistente per utente. Le identità utente in genere vengono specificate con uno dei quattro formati seguenti: 1) l'indirizzo SIP dell'utente, 2) il nome dell'entità utente (UPN, User Principal Name), 3) il nome di dominio e il nome di accesso dell'utente nel formato dominio\accesso (ad esempio litwareinc\kenmyer) e 4) il nome visualizzato di Active Directory dell'utente (ad esempio Ken Myer). È possibile specificare le identità utente anche utilizzando il nome distinto Active Directory dell'utente.</p>
<p>È inoltre possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il valore di Display Name come parametro Identity dell'utente. Ad esempio, l'identità &quot;* Smith&quot; restituisce tutti gli utenti il cui nome visualizzato termina con il valore stringa &quot; Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>&quot;Nome&quot; del criterio da assegnare. PolicyName corrisponde all'identità del criterio meno l'ambito del criterio (il prefisso &quot;tag:&quot;). Ad esempio, per un criterio con identità (Identity) tag:Redmond, il parametro PolicyName sarà uguale a Redmond, mentre per un criterio con identità tag:RedmondUsersPersistentChatPolicy, il parametro PolicyName sarà uguale a RedmondUsersPersistentChatPolicy. Per annullare l'assegnazione di un criterio per utente precedentemente assegnato a un utente, impostare PolicyName su un valore Null ($Null).</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di specificare il nome di dominio completo di un controller di dominio da contattare durante l'assegnazione del nuovo criterio. Se questo parametro non viene specificato, il cmdlet <strong>Grant-CsPersistentChatPolicy</strong> contatterà il primo controller di dominio disponibile.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di passare tramite la pipeline un oggetto utente che rappresenta l'utente a cui viene assegnato il criterio. Per impostazione predefinita, il cmdlet <strong>Grant-CsPersistentChatPolicy</strong> non passa oggetti tramite pipeline.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Valore stringa oppure oggetto Microsoft.Rtc.Management.WritableConfig.Policy.PersistentChat.PersistentChatPolicy. Il cmdlet **Grant-CsPersistentChatPolicy** accetta l'input da pipeline di valori stringa che rappresentano l'identità di un account utente. Il cmdlet accetta inoltre l'input da pipeline di oggetti utente.

## Tipi restituiti

Per impostazione predefinita, il cmdlet **Grant-CsPersistentChatPolicy** non restituisce oggetti o valori. Se tuttavia si include il parametro PassThru, il cmdlet restituisce istanze di Microsoft.Rtc.Management.ADConnect.Schema.OCSUserOrAppContact.

## Vedere anche

#### Ulteriori risorse

[Get-CsPersistentChatPolicy](get-cspersistentchatpolicy.md)  
[New-CsPersistentChatPolicy](new-cspersistentchatpolicy.md)  
[Remove-CsPersistentChatPolicy](remove-cspersistentchatpolicy.md)  
[Set-CsPersistentChatPolicy](set-cspersistentchatpolicy.md)

