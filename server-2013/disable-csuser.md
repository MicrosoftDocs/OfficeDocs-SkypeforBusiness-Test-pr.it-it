---
title: Disable-CsUser
TOCTitle: Disable-CsUser
ms:assetid: 92e7e29e-2620-4852-9e4a-2fd3569bb095
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398747(v=OCS.15)
ms:contentKeyID: 49301346
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disable-CsUser

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica l'account Active Directory dell'utente o degli utenti specificati. Questa modifica impedisce agli utenti di utilizzare i client Lync Server, ad esempio Lync 2013. Il cmdlet **Disable-CsUser** limita solo l'attività relativa a Lync Server. Non disabilita né rimuove l'account Active Directory di un utente. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Disable-CsUser -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene disabilitato l'account di Lync Server per l'utente Ken Myer. In questo esempio viene utilizzato il nome visualizzato dell'utente per indicarne l'identità.

    Disable-CsUser -Identity "Ken Myer"

## ESEMPIO 2

Nell'esempio 2 gli account di Lync Server di tutti gli utenti del reparto Finance vengono disabilitati. A tale scopo, nel comando vengono innanzitutto utilizzati il cmdlet **Get-CsUser** e il parametro LdapFilter per restituire una raccolta di tutti gli utenti che appartengono al reparto Finance. La raccolta viene quindi inviata tramite pipe al cmdlet **Disable-CsUser**, che disabilita ogni account della raccolta.

    Get-CsUser -LdapFilter "Department=Finance" | Disable-CsUser

## ESEMPIO 3

In questo esempio vengono disabilitati tutti gli account utente che attualmente non sono assegnati a un pool di registrazione. A tale scopo, viene chiamato il cmdlet **Get-CsUser** con il parametro UnassignedUser. Questo parametro restituisce solo gli utenti che dispongono di account utente validi, ma che non sono assegnati a un pool di registrazione. La raccolta viene quindi inviata tramite pipe al cmdlet Disable-CsUser, che disabilita ogni account della raccolta.

    Get-CsUser -UnassignedUser | Disable-CsUser

## Descrizione dettagliata

Il cmdlet **Disable-CsUser** elimina tutte le informazioni sugli attributi correlate a Lync Server da un account utente Active Directory. In questo modo si impedisce all'utente di accedere a Lync Server. Quando si esegue il cmdlet **Disable-CsUser**, tutti gli attributi correlati a Lync Server vengono rimossi da un account, incluse le identità di eventuali criteri per utente assegnati a tale account. In seguito è possibile riabilitare l'account utilizzando il cmdlet **Enable-CsUser**. Tuttavia, tutte le informazioni correlate a Lync Server ( ad esempio le assegnazioni dei criteri) precedentemente associate all'account dovranno essere ricreate. Per impedire a un utente di accedere a Lync Server senza perdere le informazioni dell'account, utilizzare il cmdlet **Set-CsUser**. Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet [Set-CsUser](set-csuser.md).

Dopo aver disabilitato un account con il cmdlet **Disable-CsUser**, l'utente interessato non verrà più restituito dal cmdlet **Get-CsUser**, poiché non disporrà più di un account Lync Server valido. Per recuperare le informazioni per l'account utente disabilitato, utilizzare il cmdlet **Get-CsAdUser**.

Inoltre, i dati utente appartenenti all'account utente eliminato saranno rimossi dai database di back-end; ad esempio, l'utente sarà rimosso dall'elenco Contatti nell'organizzazione e le eventuali conferenze pianificate dall'utente saranno eliminate.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Disable-CsUser** in locale: RTCUniversalUserAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Disable-CsUser"}

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
<td><p>Indica l'identità dell'account utente da disabilitare. Le identità utente possono essere specificate con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP dell'utente; 2) l'UPN (User Principal Name) dell'utente; 3) il nome di dominio e il nome di accesso dell'utente, nel formato dominio\accesso (ad esempio, litwareinc\davidegarghentini); 4) il nome visualizzato Active Directory dell'utente (ad esempio, Davide Garghentini). L'account utente può essere referenziati anche utilizzando il nome distinto in Active Directory.</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come identità utente. Ad esempio, l'identità &quot;* Smith&quot; restituisce tutti gli utenti il cui nome visualizzato termina con il valore stringa &quot; Smith&quot;.</p></td>
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
<td><p>Consente la connessione al controller di dominio specificato per disabilitare un account utente. Per la connessione a uno specifico controller di dominio, includere il parametro DomainController seguito dal nome computer (ad esempio atl-cs-001) o dal suo nome di dominio completo (ad esempio atl-cs-001.litwareinc.com).</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di passare attraverso la pipeline un oggetto utente che rappresenta l'account utente da disabilitare. Per impostazione predefinita, il cmdlet <strong>Disable-CsUser</strong> non passa alcun oggetto attraverso la pipeline.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa oppure oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Disable-CsUser** accetta gli input tramite pipeline dei valori stringa che rappresentano l'identità di un account utente abilitato per Lync Server. Il cmdlet accetta anche istanze di oggetti utente di Active Directory inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Disable-CsUser** non restituisce alcun oggetto o valore. Configura invece le istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser.

## Vedere anche

#### Ulteriori risorse

[Enable-CsUser](enable-csuser.md)  
[Get-CsUser](get-csuser.md)

