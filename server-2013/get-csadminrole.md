---
title: Get-CsAdminRole
TOCTitle: Get-CsAdminRole
ms:assetid: ea15ee37-f7a1-4e67-afe8-08e63e8ca765
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399050(v=OCS.15)
ms:contentKeyID: 49302364
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAdminRole

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui ruoli RBAC (Role-Based Access Control, controllo di accesso basato sui ruoli) utilizzati nell'organizzazione. I ruoli RBAC vengono utilizzati per definire le attività di gestione che gli utenti sono autorizzati a svolgere e l'ambito in cui sono autorizzati a operare. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsAdminRole [-Identity <String>] <COMMON PARAMETERS>

    Get-CsAdminRole [-Sid <String>] <COMMON PARAMETERS>

    Get-CsAdminRole [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 restituisce informazioni su tutti i ruoli RBAC configurati per l'utilizzo nell'organizzazione. A tale scopo, viene chiamato il cmdlet **Get-CsAdminRole** senza alcun parametro.

    Get-CsAdminRole

## ESEMPIO 2

Nell'esempio 2 viene restituito un unico ruolo RBAC, ovvero il ruolo con parametro Identity CsHelpDesk.

    Get-CsAdminRole -Identity "CsHelpDesk"

## ESEMPIO 3

Nell'esempio 3 vengono restituiti tutti i ruoli RBAC con valore stringa "Voice" in un punto qualsiasi del parametro Identity, ad esempio CsVoiceAdministrator o RedmondVoiceAdministrators. A tale scopo, viene chiamato **Get-CsAdminRole** con il parametro Filter. Il valore di filtro "\*Voice\*" limita i dati restituiti ai ruoli RBAC con valore stringa "Voice" in un punto qualsiasi del parametro Identity.

    Get-CsAdminRole -Filter "*Voice*"

## ESEMPIO 4

Nell'esempio 4 vengono restituiti tutti i ruoli RBAC personalizzati creati per l'utilizzo nell'organizzazione. Per eseguire questa attività, il comando utilizza innanzitutto il cmdlet **Get-CsAdminRole** per restituire una raccolta di tutti i ruoli RBAC attualmente in uso. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i ruoli in cui la proprietà IsStandardRole è uguale a False. Per definizione, ogni ruolo che soddisfa tale criterio è un ruolo RBAC personalizzato.

    Get-CsAdminRole | Where-Object {$_.IsStandardRole -eq $False}

## ESEMPIO 5

Con il comando mostrato nell'esempio 5 vengono restituiti tutti i ruoli RBAC che includono il cmdlet **Set-CsUser**. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsAdminRole** senza alcun parametro per restituire una raccolta di tutti i ruoli RBAC configurati nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona qualsiasi ruolo in cui la proprietà Cmdlets include il valore stringa "Set-CsUser\\b". \\b è un marcatore di confine di parola che segnala che "Set-CsUser" rappresenta l'intero valore stringa.

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Set-CsUser\b"}

## ESEMPIO 6

Nell'esempio 6 vengono restituite informazioni su tutti i ruoli RBAC che includono l'unità organizzativa specificata (ou=Redmond, dc=litwareinc, dc=com) nella proprietà UserScopes. Per eseguire questa attività, nel comando viene innanzitutto chiamato il cmdlet **Get-CsAdminRole** per restituire una raccolta di tutti i ruoli RBAC attualmente configurati per l'utilizzo. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona tutti i ruoli che includono il valore stringa "OU:ou=Redmond,dc=litwareinc,dc=com" nella proprietà UserScopes.

    Get-CsAdminRole | Where-Object {$_.UserScopes -match "OU: ou=Redmond,dc=litwareinc,dc=com"}

## ESEMPIO 7

Il comando riportato nell'esempio 7 restituisce un elenco di tutti i cmdlet inclusi nel ruolo CsVoiceAdministrator. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsAdminRole** per restituire tutte le proprietà e i relativi valori per CsVoiceAdministrator. Le informazioni vengono quindi inviate tramite pipe al cmdlet **Select-Object** che utilizza il parametro ExpandProperty per visualizzare tutti gli elementi contenuti nella proprietà Cmdlets.

    Get-CsAdminRole -Identity "CsVoiceAdministrator" | Select-Object -ExpandProperty Cmdlets

## Descrizione dettagliata

Il controllo di accesso basato sui ruoli (RBAC) consente agli amministratori di delegare il controllo di specifiche attività di gestione in Lync Server. Ad esempio, invece di concedere privilegi di amministrazione completi agli addetti al supporto tecnico dell'organizzazione, è possibile assegnare a tali dipendenti diritti molto specifici, tra cui il diritto di gestire solo gli account utente, solo i componenti di VoIP aziendale e solo l'archiviazione e il server di archiviazione. Inoltre, tali diritti possono essere limitati nell'ambito: ad alcuni dipendenti può essere concesso il diritto di gestire VoIP aziendale, ma solo nel sito di Redmond, mentre ad altri può essere concesso il diritto di gestire gli utenti, ma solo se tali account utente sono nell'unità organizzativa Finante.

L'implementazione del controllo di accesso basato sui ruoli in Lync Server è incentrata su due elementi chiave, i gruppi di sicurezza di Active Directory e i cmdlet di Windows PowerShell. Quando si installa Lync Server, vengono creati automaticamente diversi gruppi di sicurezza universali, tra cui CsAdministrator, CsArchivingAdministrator e CsViewOnlyAdministrator. Questi gruppi di sicurezza universali presentano una corrispondenza uno-a-uno con i ruoli RBAC, pertanto ogni utente presente nel gruppo di sicurezza CsArchivingAdministrator possiede tutti i diritti concessi al ruolo RBAC di CsArchivingAdministrator. A loro volta, i diritti concessi ad un ruolo RBAC si basano sui cmdlet assegnati a tale ruolo (i cmdlet possono essere assegnati a ruoli RBAC multipli). Si supponga, ad esempio, che un ruolo sia stato assegnato ai seguenti cmdlet:

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

Nell'elenco precedente sono riportati solo i cmdlet che possono essere eseguiti in una sessione remota dell'interfaccia della riga di comando Windows PowerShell da un utente a cui è stato assegnato un ipotetico ruolo RBAC. Se l'utente tenta di eseguire il cmdlet **Disable-CsUser**, il comando avrà esito negativo. Ciò accade perché gli utenti a cui è stato assegnato il ruolo ipotetico non dispongono del diritto di eseguire il cmdlet **Disable-CsUser**. Questa regola si applica anche al Pannello di controllo di Lync Server. Ad esempio, un amministratore dell'archiviazione non può disabilitare un utente utilizzando il Pannello di controllo di Lync Server, in quanto il Pannello di controllo di Lync Server si attiene ai ruoli RBAC. Ogni volta che si esegue un comando nel Pannello di controllo di Lync Server si esegue in effetti una chiamata del cmdlet di Windows PowerShell. Se non si è autorizzati a eseguire il cmdlet **Disable-CsUser**, non avrà alcuna importanza se si esegue direttamente il cmdlet da una sessione remota di Windows PowerShell o indirettamente nel Pannello di controllo di Lync Server. Il comando avrà comunque esito negativo.

RBAC si applica solo alla gestione remota. Se si è connessi a un computer in cui è in esecuzione Lync Server e si apre Lync Server Management Shell, i ruoli RBAC non verranno applicati. La protezione viene invece garantita principalmente tramite i gruppi di sicurezza RTCUniversalServerAdmins, RTCUniversalUserAdmins e RTCUniversalReadOnlyAdmins.

Quando si installa Lync Server, vengono creati diversi ruoli RBAC predefiniti. Tali ruoli riguardano aree amministrative comuni quali l'amministrazione vocale, la gestione degli utenti e l'amministrazione di Response Group. Questi ruoli predefiniti non possono essere in alcun modo modificati: non è possibile aggiungere o rimuovere cmdlet dai ruoli e non è possibile eliminare tali ruoli. Qualsiasi tentativo di eliminare un ruolo predefinito genererà un messaggio di errore. Tuttavia, è possibile utilizzare i ruoli predefiniti per creare ruoli RBAC personalizzati. Questi ruoli personalizzati possono quindi essere modificati cambiando gli ambiti amministrativi. Ad esempio, è possibile limitare il ruolo alla gestione degli account utente con una determinata unità organizzativa di Attive Directory.

Il cmdlet **Get-CsAdminRole** restituisce informazioni su tutti i ruoli RBAC disponibili per l'utilizzo nell'organizzazione.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsAdminRole** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Per restituire un elenco di tutti i ruoli RBAC ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAdminRole\\b"}

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare caratteri jolly per specificare il ruolo o i ruoli RBAC da restituire. Ad esempio, per restituire tutti i ruoli che includono il valore stringa &quot;Redmond&quot; nel parametro Identity, è possibile utilizzare la seguente sintassi: -Filter &quot;*Redmond*&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Identificatore univoco per il ruolo RBAC da restituire. L'identità per un ruolo RBAC deve corrispondere a quella di SamAccountName per il gruppo di sicurezza universale di Active Directory associato a tale ruolo. Ad esempio, il ruolo Help Desk ha un valore Identity uguale a CsHelpDesk e CsHelpDesk è anche il valore SamAccountName del gruppo di sicurezza di Active Directory associato a tale ruolo.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati RBAC dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
<tr class="even">
<td><p><em>Sid</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare un ID di sicurezza (SID) per specificare il ruolo RBAC da recuperare. I SID vengono assegnati da Lync Server al momento della creazione del ruolo RBAC e sono simili a quello riportato di seguito: S-1-5-21-1573807623-1597889489-1765977225-1145.</p>
<p>Lo stesso SID è disponibile anche nel gruppo di sicurezza di Active Directory.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet **Get-CsAdminRole** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Roles.Role.

