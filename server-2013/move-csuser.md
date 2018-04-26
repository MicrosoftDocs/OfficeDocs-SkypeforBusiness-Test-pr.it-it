---
title: Move-CsUser
TOCTitle: Move-CsUser
ms:assetid: 6fbdbab6-8a8c-421c-b16c-2319be4b8915
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398528(v=OCS.15)
ms:contentKeyID: 49300926
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsUser

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Sposta uno o più account utente abilitati per Lync Server in un nuovo pool di registrazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Move-CsUser -Identity <UserIdParameter> -Target <Fqdn> [-Confirm [<SwitchParameter>]] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-HostedMigrationOverrideUrl <String>] [-IgnoreBackendStoreException <SwitchParameter>] [-MoveConferenceData <SwitchParameter>] [-PassThru <SwitchParameter>] [-ProxyPool <Fqdn>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 il cmdlet **Move-CsUser** è utilizzato per spostare l'account utente con identità (Identity) Pilar Ackerman nel pool di registrazione atl-cs-001.litwareinc.

    Move-CsUser -Identity "Pilar Ackerman" -Target "atl-cs-001.litwareinc.com"

## ESEMPIO 2

Nell'esempio 2 tutti gli account utente nell'unità organizzativa Finance vengono spostati nel pool di registrazione atl-cs-001.litwareinc.com. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsUser** e il parametro OU per recuperare una raccolta di tutti gli account utente nell'unità organizzativa Finance. Dopo aver recuperato i dati, le informazioni vengono inviate tramite pipe al cmdlet **Move-CsUser**, che sposta ogni account della raccolta nel pool di registrazione atl-cs-001.litwareinc.com.

    Get-CsUser -OU "ou=Finance,dc=litwareinc,dc=com" | Move-CsUser -Target "atl-cs-001.litwareinc.com"

## ESEMPIO 3

Nell'esempio 3 il cmdlet **Move-CsUser** è utilizzato per spostare l'account utente con identità (Identity) Pilar Ackerman nel pool di registrazione atl-cs-001.litwareinc. Viene utilizzato inoltre il parametro Force per garantire che venga spostato solo l'account. I dati associati all'account, ad esempio le conferenze pianificate da Pilar Ackerman, non verranno spostati ma ignorati. Il parametro Force dovrebbe essere utilizzato solo se si è tentato di eseguire il cmdlet **Move-CsUser** senza parametri e lo spostamento ha avuto esito negativo.

    Move-CsUser -Identity "Pilar Ackerman" -Target "atl-cs-001.litwareinc.com" -Force

## Descrizione dettagliata

Il cmdlet **Move-CsUser** consente di spostare un account utente abilitato per Lync Server da un pool di registrazione all'altro. Il cmdlet **Move-CsUser** influisce solamente sulla posizione dell'account utente in Lync Server e non determina lo spostamento dell'account Active Directory dell'utente in una nuova unità organizzativa o in un'altra posizione.

Se Lync Server coesiste con Office Communications Server 2007 R2 o Office Communications Server 2007, il cmdlet **Move-CsUser** può essere utilizzato per riportare un utente da Lync Server all'installazione legacy di Office Communications Server. Per riportare un utente a Office Communications Server, assegnare al parametro Target il nome di dominio completo (FQDN) del precedente pool. Si tenga presente che l'utente che viene riportato in Office Communications Server probabilmente sperimenterà perdite di funzionalità e di dati, questo poiché Lync Server è dotato di molte più funzionalità sia di Office Communications Server 2007 che di Office Communications Server 2007 R2. Gli utenti che vengono riportati ad una versione legacy potrebbero avere la necessità di reinstallare le versioni precedenti dei propri software client e potrebbe essere necessario ripianificare riunioni create quando quell'account utente era domiciliato su Lync Server.

Per spostare utenti da Communications Server 2007 oppure Communications Server 2007 R2 in Lync Server, utilizzare il cmdlet **Move-CsLegacyUser**. Il cmdlet **Move-CsUser** è progettato per spostare utenti da un pool di Lync Server a un altro pool di Lync Server o per spostare un utente da un pool di Lync Server a un pool di Office Communications Server. Move-CsLegacyUser sposta utenti da Office Communications Server a Lync Server.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Move-CsUser** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Move-CsUser"}

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
<td><p>Indica l'identità dell'account utente da spostare. Le identità dell'utente possono essere specificate utilizzando uno dei seguenti quattro formati: 1) l'indirizzo SIP dell'utente; 2) il nome dell'entità utente (UPN); 3) il nome del dominio e il nome di accesso dell'utente nella forma dominio\accesso (ad esempio, litwareinc\kenmyer); 4) il nome visualizzato Active Directory dell'utente (ad esempio, Ken Myer). Alle identità utente è anche possibile fare riferimento utilizzando il nome distinto Active Directory dell'utente.</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come identità utente. Ad esempio, il parametro Identity &quot;* Smith&quot; restituirà tutti gli utenti con un nome visualizzato che termina con il valore di stringa &quot; Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Target</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Il nome di dominio completo (ad esempio, atl-cs-001.litwareinc.com) del pool di registrazione in cui deve essere spostato l'account utente. In aggiunta al pool di registrazione il parametro Target può essere costituito dal FQDN di un Front End ServerOffice Communications Server legacy o di un provider di hosting. Qualunque account spostato verso un provider di hosting (ad esempio, Microsoft Lync Online 2010) perderà i propri dati utente associati. Ad esempio, qualsiasi conferenza che l'utente ha pianificato verrà eliminata e non sarà disponibile in Lync Online 2010.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di ignorare il prompt di conferma che comunque si vuol far apparire quando si tenta di spostare un utente. Per ignorare il prompt di conferma, includere il parametro Confirm utilizzando questa sintassi:</p>
<p>-Confirm:$False</p>
<p>Se invece si preferisce avere il prompt di conferma utilizzare questa sintassi:</p>
<p>-Confirm</p></td>
</tr>
<tr class="even">
<td><p><em>Credential</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Consente di eseguire il cmdlet Move-CsUser utilizzando credenziali alternative. Può essere necessario se l'account utilizzato per accedere a Windows non dispone dei privilegi necessari per utilizzare oggetti contatto.</p>
<p>Per utilizzare il parametro Credential, è necessario innanzitutto creare un oggetto PSCredential utilizzando il cmdlet <strong>Get-Credential</strong>. Per informazioni dettagliate, vedere nella Guida l'argomento relativo al cmdlet <strong>Get-Credential</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di eseguire la connessione al controller di dominio specificato per recuperare le informazioni sul contatto. Per la connessione a un controller di dominio specifico, includere il parametro DomainController seguito dal nome computer (ad esempio, atl-cs-001) o dal suo FQDN (ad esempio, atl-cs-001.litwareinc.com).</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, consente di spostare l'account utente e di eliminare eventuali dati associati (ad esempio, le conferenze pianificate dall'utente). Se non è presente verranno spostati sia l'account che i dati associati.</p></td>
</tr>
<tr class="odd">
<td><p><em>HostedMigrationOverrideUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL del servizio di migrazione ospitato utilizzato per lo spostamento di un utente in Skype for Business online.</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreBackendStoreException</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, questo parametro indica al computer di ignorare gli eventuali errori che possono verificarsi con il database back-end e di tentare comunque di spostare l'utente.</p></td>
</tr>
<tr class="odd">
<td><p><em>MoveConferenceData</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, sposta i dati relativi a riunioni e conferenze per gli utenti che vengono trasferiti in un altro pool di registrazione. Non utilizzare il parametro MoveConferenceData se si spostano gli utenti nel corso di una procedura di ripristino di emergenza. In questo caso infatti i dati delle conferenze devono essere spostati utilizzando il servizio di backup.</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di specificare attraverso la pipeline un oggetto utente che rappresenta l'account utente che si sta spostando. Per impostazione predefinita, il cmdlet <strong>Move-CsUser</strong> non fornisce alcun oggetto tramite la pipeline.</p></td>
</tr>
<tr class="odd">
<td><p><em>ProxyPool</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Questo parametro è utilizzato solo per Lync Online. Non deve essere utilizzato con un'implementazione locale di Lync Server.</p></td>
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

Stringa oppure oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Move-CsUser** accetta gli input tramite pipeline dei valori stringa che rappresentano l'identità di un account utente abilitato per Lync Server. Il cmdlet accetta anche le istanze di oggetti utente di Active Directory inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Move-CsUser** non restituisce alcun oggetto o valore. Modifica invece le istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser.

## Vedere anche

#### Ulteriori risorse

[Get-CsUser](get-csuser.md)  
[Move-CsLegacyUser](move-cslegacyuser.md)

