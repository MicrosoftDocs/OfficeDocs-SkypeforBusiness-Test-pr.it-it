---
title: Grant-CsUserServicesPolicy
TOCTitle: Grant-CsUserServicesPolicy
ms:assetid: f68b5c61-9820-4b49-954a-2dd61156bc02
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205388(v=OCS.15)
ms:contentKeyID: 49302490
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsUserServicesPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Assegna a uno o più utenti un criterio servizi utente per utente. I criteri servizi utente determinano se i contatti di un utente vengono o meno archiviati in Lync Server 2013 o nell'archivio contatti unificato. L'archivio contatti unificato consente agli utenti di gestire un unico insieme di contatti accessibili tramite Lync 2013, Microsoft Outlook e/o Microsoft Outlook Web Access. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Grant-CsUserServicesPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 assegna i criteri Servizi utente con ambito per utente RedmondUserServicesPolicy all'utente con l'identità (in questo esempio, il nome visualizzato di Active Directory) Ken Myer.

    Grant-CsUserServicesPolicy -Identity "Ken Myer" -PolicyName "RedmondUserServicesPolicy"

## Esempio 2

Nell'esempio 2 viene annullata l'assegnazione di tutti i criteri Servizi utente con ambito per utente precedentemente assegnati a Ken Myer. L'assegnazione dei criteri per utente viene annullata impostando il parametro PolicyName su un valore Null ($Null).

    Grant-CsUserServicesPolicy -Identity "Ken Myer" -PolicyName $Null

## Esempio 3

Nell'esempio 3 a tutti gli utenti nel pool di registrazione atl-cs-001.litwareinc.com vengono assegnati i criteri Servizi utente RedmondUserServicesPolicy. A tal fine, viene innanzitutto chiamato il cmdlet **Get-CsUser** con il parametro Filter. Il valore di filtro {RegistrarPool –eq "atl-cs-001.litwareinc.com" limita i dati restituiti agli utenti che sono stati ospitati nel pool di registrazione atl-cs-001.litwareinc.com. Questa raccolta di utenti viene quindi inviata tramite pipe al cmdlet **Grant-CsUserServicesPolicy** che, a sua volta, assegna i criteri RedmondUserServicesPolicy a ogni utente nella raccolta.

    Get-CsUser -Filter {RegistrarPool -eq "atl-cs-001.litwareinc.com"} | Grant-CsUserServicesPolicy -PolicyName "RedmondUserServicesPolicy"

## Descrizione dettagliata

L'archivio contatti unificato, introdotto in Lync Server 2013, consente agli amministratori di archiviare i contatti di un utente in Microsoft Exchange Server 2013 anziché in Lync Server. In questo modo l'utente può accedere allo stesso insieme di contatti in Microsoft Outlook e Outlook Web Access e in Lync 2013. In alternativa, è possibile continuare ad archiviare i contatti in Lync Server 2013. In tal caso gli utenti dovranno gestire due insiemi separati di contatti: uno da utilizzare con Outlook e Outlook Web Access e un altro da utilizzare con Lync 2013.

Per usufruire dell'archivio contatti unificato, è inoltre necessario assegnare all'utente un criterio servizi utente che consenta l'utilizzo dell'archivio contatti unificato. I criteri servizi utente, che possono essere configurati nell'ambito globale, del sito o per utente, includono solo una proprietà: UcsAllowed. Se questa proprietà è impostata su True e vengono soddisfatti tutti gli altri prerequisiti, al successivo accesso di un utente a Lync Server 2013 viene eseguita automaticamente la migrazione dei relativi contatti nell'archivio contatti unificato.

Se questa proprietà è impostata su False, la migrazione automatica non viene eseguita. La sola impostazione di UcsAllowed tuttavia non determina lo spostamento dei contatti di un utente dall'archivio contatti unificato in Lync Server. Per ottenere questo risultato, è necessario innanzitutto assegnare all'utente un criterio servizi utente che non consenta l'utilizzo dell'archivio contatti unificato. Utilizzare quindi il cmdlet I**nvoke-UcsRollback** per eseguire "manualmente" la migrazione dei contatti dall'archivio contatti unificato in Lync Server.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi eventuali ruoli RBAC personalizzati creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsUserServicesPolicy"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Grant-CsUserServicesPolicy** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Indica l'identità dell'account utente a cui assegnare i criteri di esperienza utente con ambito per utente. Le identità utente sono in genere specificate utilizzando uno dei quattro formati seguenti: 1) indirizzo SIP dell'utente; 2) nome entità utente (UPN) dell'utente; 3) nome di dominio e nome di accesso dell'utente, nel formato dominio\nome di accesso (ad esempio, litwareinc\kenmyer); 4) nome visualizzato di Active Directory dell'utente (ad esempio, Ken Myer).</p>
<p>È inoltre possibile specificare le identità utente utilizzando il nome distinto di Active Directory dell'utente.</p>
<p>Quando si utilizza il nome visualizzato come identità utente è anche possibile utilizzare il carattere jolly asterisco (*). Ad esempio, l'identità &quot;* Smith&quot; restituisce tutti gli utenti che hanno un nome visualizzato che termina con il valore di stringa &quot; Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>&quot;Nome&quot; dei criteri da assegnare. PolicyName è costituito semplicemente dall'identità dei criteri meno l'ambito dei criteri (prefisso &quot;tag:&quot;). Ad esempio, i criteri con identità tag:Redmond presentano un valore PolicyName uguale a Redmond. Analogamente, i criteri con identità tag:RedmondUserExperiencePolicy presentano un valore PolicyName uguale a RedmondUserExperiencePolicy.</p>
<p>Per annullare l'assegnazione di criteri per utente precedentemente assegnati a un utente, impostare PolicyName su un valore null ($Null).</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di connettere il controller di dominio specificato per ottenere informazioni sull'utente. Per connettere un particolare controller di dominio, includere il parametro DomainController seguito dal nome del computer, ad esempio atl-dc-001, oppure il relativo nome di dominio completo (FQDN), ad esempio atl-dc-001.litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di passare tramite pipeline un oggetto utente che rappresenta l'account utente a cui sono assegnati i criteri. Per impostazione predefinita, il cmdlet <strong>Grant-CsUserServicesPolicy</strong> non passa oggetti tramite la pipeline.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive cosa accadrebbe se si eseguisse il comando senza eseguirlo effettivamente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Valore di stringa o oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Grant-CsUserServicesPolicy** accetta input da pipeline di valori di stringa che rappresentano l'identità di un account utente. Il cmdlet accetta anche input da pipeline di oggetti utente.

## Tipi restituiti

Per impostazione predefinita, il cmdlet **Grant-CsUserServicesPolicy** non restituisce un valore o un oggetto. Tuttavia, se si include il parametro PassThru, il cmdlet restituisce istanze di Microsoft.Rtc.Management.ADConnect.Schema.OCSUserOrAppContact.

## Vedere anche

#### Ulteriori risorse

[Get-CsUserServicesPolicy](get-csuserservicespolicy.md)  
[New-CsUserServicesPolicy](new-csuserservicespolicy.md)  
[Remove-CsUserServicesPolicy](remove-csuserservicespolicy.md)  
[Set-CsUserServicesPolicy](set-csuserservicespolicy.md)

