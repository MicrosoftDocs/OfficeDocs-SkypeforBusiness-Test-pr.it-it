---
title: Invoke-CsUcsRollback
TOCTitle: Invoke-CsUcsRollback
ms:assetid: 0aed0286-e552-4d47-93bc-3375cab48a03
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204661(v=OCS.15)
ms:contentKeyID: 49299635
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Invoke-CsUcsRollback

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove i contatti di un utente dall'archivio contatti unificato e archivia le informazioni dei contatti in Lync Server 2013. L'archivio contatti unificato consente agli utenti di gestire un unico insieme di contatti accessibili tramite Lync 2013, Microsoft Outlook e/o Microsoft Outlook Web Access. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Invoke-CsUcsRollback -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 rimuove l'utente Ken Myer dall'archivio contatti unificato.

    Invoke-CsUcsRollback -Identity "Ken Myer"

## Esempio 2

Nell'esempio 2 vengono rimossi dall'archivio contatti unificato tutti gli utenti situati nel pool di registrazione atl-cs-001.litwareinc.com. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsUser** con il parametro Filter. Il valore di filtro {RegistrarPool –eq "atl-cs-001.litwareinc.com"} restituisce solo gli utenti situati nel pool atl-cs-001.litwareinc.com. Questi account utente vengono quindi inviati tramite pipe al cmdlet **Invoke-CsUcsRollback**, che rimuove ogni utente dall'archivio contatti unificato. Per evitare di visualizzare la richiesta di conferma che verrebbe altrimenti visualizzata ogni volta che il cmdlet esegue il rollback di un account utente, viene incluso il parametro Confirm utilizzando la sintassi seguente: -Confirm:$False

    Get-CsUser -Filter {RegistrarPool -eq "atl-cs-001.litwareinc.com"} | Invoke-CsUcsRollback -Confirm:$False

## Descrizione dettagliata

L'archivio contatti unificato, introdotto in Lync Server 2013, consente agli amministratori di archiviare i contatti di un utente in Microsoft Exchange Server 2013 anziché in Lync Server. In questo modo l'utente può accedere allo stesso insieme di contatti in Microsoft Outlook e Outlook Web Access e in Lync 2013. In alternativa, è possibile continuare ad archiviare i contatti in Lync Server. In tal caso gli utenti dovranno gestire due insiemi separati di contatti: uno da utilizzare con Outlook e Outlook Web Access e un altro da utilizzare con Lync 2013.

Per usufruire dell'archivio contatti unificato, è inoltre necessario assegnare all'utente un criterio servizi utente che consenta l'utilizzo dell'archivio contatti unificato. Se vengono soddisfatti tutti gli altri prerequisiti, al successivo accesso dell'utente tramite Lync Server 2013 i relativi contatti verranno spostati automaticamente da Lync Server nell'archivio contatti unificato. Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet Set-CsUserServicesPolicy.

Se successivamente si decide di spostare di nuovo i contatti in Lync Server e pertanto all'esterno dell'archivio contatti unificato, sarà necessario eseguire due operazioni. Assegnare innanzitutto all'utente un nuovo criterio servizi utente che impedisca l'utilizzo dell'archivio contatti unificato. Utilizzare quindi il cmdlet **Invoke-CsUcsRollback** per eseguire "manualmente" la migrazione dei contatti dall'archivio contatti unificato a Lync Server. La sola modifica del criterio servizi utente non comporta la rimozione dei contatti dell'utente dall'archivio contatti unificato. Questo risultato si ottiene solo chiamando il cmdlet **Invoke-CsUcsRollback**.

Nota: da un punto di vista tecnico, chiamando il cmdlet **Invoke-CsUcsRollback** senza modificare il criterio servizi utente, i contatti dell'utente vengono rimossi dall'archivio contatti unificato. Questa modifica tuttavia sarà solo temporanea. Se infatti non si modifica il criterio servizi utente, dopo un periodo di attesa di sette giorni i contatti dell'utente verranno automaticamente spostati di nuovo nell'archivio contatti unificato.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Invoke-CsUcsRollback"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Invoke-CsUcsRollback** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Indica l'identità dell'account utente di cui eseguire il rollback. Le identità utente vengono in genere specificate utilizzando uno dei quattro formati seguenti: 1) l'indirizzo SIP dell'utente, 2) il nome dell'entità utente (UPN), 3) il nome di dominio e il nome di accesso dell'utente nel formato dominio\accesso (ad esempio litwareinc\kenmyer) e 4) il nome visualizzato di Active Directory dell'utente (ad esempio Ken Myer).</p>
<p>È inoltre possibile fare riferimento all'account utente utilizzando il nome distinto dell'utente in Active Directory.</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come identità utente. Ad esempio, l'identità &quot;* Smith&quot; restituisce tutti gli utenti il cui nome visualizzato termina con il valore stringa &quot; Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando. Per evitare di visualizzare una richiesta di conferma ogni volta che si esegue il rollback di un account utente, utilizzare la sintassi seguente:</p>
<p>-Confirm:$False</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di eseguire la connessione al controller di dominio specificato per recuperare le informazioni sugli utenti. Per la connessione a un controller di dominio specifico, includere il parametro DomainController seguito dal nome computer, ad esempio atl-dc-001, o dal nome di dominio completo (FQDN), ad esempio atl-cd-001.litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di passare tramite la pipeline un oggetto utente che rappresenta l'account utente da rimuovere dall'archivio contatti unificato. Per impostazione predefinita, il cmdlet <strong>Invoke-CsUcsRollback</strong> non passa oggetti tramite pipeline.</p></td>
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

Valore stringa oppure oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Invoke-CsUcsRollback** accetta l'input da pipeline di valori stringa che rappresentano l'identità di un account utente. Il cmdlet accetta inoltre l'input da pipeline di oggetti utente.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[New-CsUserServicesPolicy](new-csuserservicespolicy.md)  
[Set-CsUserServicesPolicy](set-csuserservicespolicy.md)  
[Test-CsUnifiedContactStore](test-csunifiedcontactstore.md)

