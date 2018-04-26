---
title: Remove-CsAdminRole
TOCTitle: Remove-CsAdminRole
ms:assetid: f676d3d5-2d4c-4095-a174-9278bc0852df
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413036(v=OCS.15)
ms:contentKeyID: 49302486
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsAdminRole

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un ruolo RBAC (Role-Based Access Control, controllo di accesso basato sui ruoli) esistente. I ruoli RBAC vengono utilizzati per definire le attività di gestione che gli utenti sono autorizzati a svolgere e l'ambito in cui sono autorizzati a operare. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsAdminRole -Identity <String> <COMMON PARAMETERS>

    Remove-CsAdminRole -Sid <String> <COMMON PARAMETERS>

    Remove-CsAdminRole [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando indicato nell'esempio 1 consente di eliminare il ruolo RBAC con il parametro Identity RedmondHelpDesk.

    Remove-CsAdminRole -Identity "RedmondHelpDesk"

## ESEMPIO 2

Nell'esempio 2 vengono eliminati tutti i ruoli RBAC con valore stringa "Redmond" all'interno del loro parametro Identity.

    Remove-CsAdminRole -Filter "*Redmond*"

## ESEMPIO 3

Nell'esempio 3 il comando consente di eliminare tutti i ruoli RBAC personalizzati che sono stati creati per essere utilizzati all'interno dell'organizzazione. A tale scopo, il comando effettua per prima cosa la chiamata del cmdlet **Get-CsAdminRole** senza alcun parametro. In questo modo viene restituita la raccolta dei ruoli RBAC. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo quei ruoli in cui la proprietà IsStandardRole è uguale a False. Per definizione, qualsiasi ruolo che soddisfa tale criterio è un ruolo personalizzato. A loro volta, i ruoli personalizzati vengono inviati tramite pipe al cmdlet **Remove-CsAdminRole**, che ne esegue l'eliminazione.

    Get-CsAdminRole | Where-Object {$_.IsStandardRole -eq $False} | Remove-CsAdminRole

## Descrizione dettagliata

RBAC consente agli amministratori di delegare il controllo di specifiche attività di gestione in Lync Server. Ad esempio, invece di concedere i privilegi completi di amministratore al personale dell'assistenza tecnica dell'organizzazione, è possibile fornire a questi dipendenti diritti molto specifici: il diritto di gestire solo i componenti di VoIP aziendale e il diritto di gestire esclusivamente l'archiviazione e server di archiviazione. Inoltre, tali diritti possono essere limitati nell'ambito: ad alcuni dipendenti può essere concesso il diritto di gestire VoIP aziendale, ma solo nel sito di Redmond, mentre ad altri può essere concesso il diritto di gestire gli utenti, ma solo se tali account utente sono nell'unità organizzativa Finance.

L'implementazione di RBAC in Lync Server si basa su due elementi chiave: i gruppi di sicurezza di Active Directory e i cmdlet di Windows PowerShell. Quando si installa Lync Server, viene creato automaticamente un certo numero di gruppi di sicurezza universali, quali CsAdministrator, CsArchivingAdministrator e CsBranchOfficeTechnician. Questi gruppi di sicurezza universali presentano una corrispondenza uno-a-uno con i ruoli RBAC, pertanto ogni utente presente nel gruppo di sicurezza CsArchivingAdministrator possiede tutti i diritti concessi al ruolo RBAC di CsArchivingAdministrator. A loro volta, i diritti concessi ad un ruolo RBAC si basano sui cmdlet assegnati a tale ruolo (i cmdlet possono essere assegnati a ruoli RBAC multipli). Si supponga, ad esempio, che un ruolo sia stato assegnato ai seguenti cmdlet:

Get-ArchivingPolicy

Grant-ArchivingPolicy

New-ArchivingPolicy

Remove-ArchivingPolicy

Set-ArchivingPolicy

Get-ArchivingConfiguration

New-ArchivingConfiguration

Remove-ArchivingConfiguration

Set-ArchivingConfiguration

Get-CsUser

Export-CsArchivingData

Get-CsComputer

Get-CsPool

Get-CsService

Get-CsSite

Nell'elenco precedente sono riportati i soli cmdlet che possono essere eseguiti da un utente con un ipotetico ruolo RBAC assegnato in una sessione remota dell'interfaccia della riga di comando Windows PowerShell. Se l'utente tenta di eseguire il cmdlet **Disable-CsUser**, il comando avrà esito negativo. Ciò accade perché gli utenti a cui è stato assegnato il ruolo ipotetico non dispongono del diritto di eseguire il cmdlet **Disable-CsUser**. Questa regola si applica anche al Pannello di controllo di Lync Server. Ad esempio, un amministratore dell'archiviazione non può disabilitare un utente utilizzando il Pannello di controllo di Lync Server, in quanto il Pannello di controllo di Lync Server si attiene ai ruoli RBAC. Ogni volta che si esegue un comando nel Pannello di controllo di Lync Server si effettua effettivamente una chiamata del cmdlet di Windows PowerShell. Se non si è autorizzati a eseguire il cmdlet **Disable-CsUser**, non avrà alcuna importanza se il cmdlet viene eseguito direttamente da Windows PowerShell o indirettamente dal Pannello di controllo di Lync Server: il comando avrà comunque esito negativo.

RBAC si applica solo alla gestione remota. Se si è effettuato l'accesso ad un computer che esegue Lync Server e si apre Lync Server Management Shell, i ruoli RBAC non verranno applicati. La protezione viene invece garantita principalmente tramite i gruppi di sicurezza RTCUniversalServerAdmins, RTCUniversalUserAdmins e RTCUniversalReadOnlyAdmins.

Quando si installa Lync Server, il programma di installazione crea vari ruoli RBAC predefiniti che coprono le aree di amministrazione comuni quali l'amministrazione vocale, la gestione degli utenti e l'amministrazione di Response Group. Questi ruoli predefiniti non possono essere in alcun modo modificati: non è possibile aggiungere o rimuovere i cmdlet assegnati ai ruoli e non è possibile eliminare tali ruoli. Qualsiasi tentativo di eliminare un ruolo predefinito genererà un messaggio di errore. Tuttavia, è possibile utilizzare i ruoli predefiniti per creare ruoli RBAC personalizzati. I ruoli personalizzati possono quindi essere modificati variando gli ambiti amministrativi. Ad esempio, è possibile limitare il ruolo per gestire gli account utente con una particolare unità organizzativa di Active Directory.

I ruoli personalizzati creati possono essere eliminati utilizzando il cmdlet **Remove-CsAdminRole**. Il cmdlet **Remove-CsAdminRole** non eliminerà il gruppo di sicurezza di Active Directory che corrisponde al ruolo personalizzato né consentirà la rimozione dei membri assegnati a tale gruppo. Il cmdlet assicurerà invece semplicemente che tale ruolo personalizzato non possa essere utilizzato per delegare il controllo di Lync Server.

Quando si elimina un ruolo RBAC, Windows PowerShell chiederà se si è sicuri di voler eliminare tale ruolo. Se non si risponde a questo prompt (o non si risponde con Sì), il ruolo non verrà eliminato. Per evitare queste richieste di conferma, utilizzare il parametro Confirm e impostare il valore del parametro su $False:

Remove-CsAdminRole RedmondAdministrators –Confirm:$False

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet Remove-CsAdminRole in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsAdminRole"}

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
<td><p>System.String</p></td>
<td><p>L'identificatore univoco per il ruolo RBAC da eliminare. L'identità per un ruolo RBAC deve corrispondere a quella di SamAccountName per il gruppo di sicurezza universale di Active Directory associato a tale ruolo. Ad esempio, il ruolo Help Desk ha il parametro Identity uguale a CsHelpDesk e CsHelpDesk è anche il valore SamAccountName del gruppo di sicurezza di Active Directory associato a tale ruolo.</p></td>
</tr>
<tr class="even">
<td><p><em>Sid</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare un identificatore di protezione (SID) per specificare il ruolo RBAC da eliminare. I SID, assegnati da Lync Server al momento della creazione del ruolo RBAC, sono simili a quello riportato di seguito: S-1-5-21-1573807623-1597889489-1765977225-1145. Il SID per un dato ruolo RBAC può essere recuperato utilizzando il cmdlet <strong>Get-CsAdminRole</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di ignorare la richiesta di conferma che viene visualizzata quando si tenta di eliminare un ruolo RBAC. Per ignorare la richiesta di conferma, utilizzare il parametro Confirm e impostare il valore del parametro su $False:</p>
<p>Remove-CsAdminRole RedmondAdministrators –Confirm:$False</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare i caratteri jolly per specificare i ruoli RBAC personalizzati da rimuovere. Ad esempio, per rimuovere tutti i ruoli personalizzati che includono il valore stringa &quot;Redmond&quot; nel loro parametro Identity, è possibile utilizzare la seguente sintassi: -Filter &quot;*Redmond*&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
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

Oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Remove-CsAdminRole** accetta input inviato tramite pipeline di oggetti utente.

## Tipi restituiti

Il cmdlet **Remove-CsAdminRole** elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Roles.Role.

