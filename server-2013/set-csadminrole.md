---
title: Set-CsAdminRole
TOCTitle: Set-CsAdminRole
ms:assetid: ec927ce6-a37b-4876-a6df-a347404f4e84
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399066(v=OCS.15)
ms:contentKeyID: 49302394
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAdminRole

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un ruolo RBAC (Role-Based Access Control, controllo di accesso basato sui ruoli) esistente. I ruoli RBAC vengono utilizzati per definire le attività di gestione che gli utenti sono autorizzati a svolgere e l'ambito in cui sono autorizzati a operare. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsAdminRole -Identity <String> [-Cmdlets <PSListModifier>] [-ConfigScopes <PSListModifier>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-ScriptModules <PSListModifier>] [-UserScopes <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene aggiunta una nuova unità organizzativa (Portland) alla proprietà UserScopes del ruolo RBAC RedmondVoiceAdministrators. A tale scopo, nel comando sono inclusi il parametro UserScopes e il seguente valore per il parametro: @{Add="OU:ou=Portland,dc=litwareinc,dc=com"}. Questa sintassi consente di aggiungere l'unità organizzativa con il nome distinto "ou=Portland,dc=litwareinc,dc=com" alle unità organizzative già esistenti nella proprietà UserScopes.

    Set-CsAdminRole -Identity "RedmondVoiceAdministrators" -UserScopes @{Add="OU:ou=Portland,dc=litwareinc,dc=com"}

## ESEMPIO 2

Il comando mostrato nell'esempio 2 consente di rimuovere l'unità organizzativa Portland dal ruolo RBAC RedmondVoiceAdministrators. A tale scopo, nel comando sono inclusi il parametro UserScopes e il seguente valore per il parametro: @{Remove="OU:ou=Portland,dc=litwareinc,dc=com"}. Questa sintassi consente di eliminare l'unità organizzativa con il nome distinto "ou=Portland,dc=litwareinc,dc=com" dalla raccolta di unità organizzative già presenti nella proprietà UserScopes.

    Set-CsAdminRole -Identity "RedmondVoiceAdministrators" -UserScopes @{Remove="OU:ou=Portland,dc=litwareinc,dc=com"}

## ESEMPIO 3

Nell'esempio 3 viene aggiunto un nuovo sito (con SiteId Redmond) alla proprietà ConfigScopes per il ruolo RBAC RedmondVoiceAdministrators. A tale scopo, nel comando sono inclusi il parametro ConfigScopes e il seguente valore per il parametro: @{Add="OU:ou=Portland,dc=litwareinc,dc=com"}. Questa sintassi consente di aggiungere il sito Redmond a qualsiasi elemento già presente nella proprietà ConfigScopes.

    Set-CsAdminRole -Identity "RedmondVoiceAdministrators" -ConfigScopes @{Add="site:Redmond"}

## ESEMPIO 4

Il comando mostrato nell'esempio 4 rimuove il sito Redmond dal ruolo RBAC RedmondVoiceAdministrators. A tale scopo, nel comando sono inclusi il parametro ConfigScopes e il seguente valore per il parametro: @{Remove="site:Redmond"}. Questo parametro elimina il sito Redmond dalla raccolta di elementi già presenti nella proprietà ConfigScopes. Tale comando avrà esito negativo se il sito Redmond è l'unico sito presente nella proprietà ConfigScopes. Se si ha necessità di rimuovere l'unico sito della proprietà ConfigScopes, è consigliabile utilizzare un comando analogo al seguente, che sostituisce tutti gli elementi di ConfigScopes con la proprietà Global:

Set-CsAdminRole -Identity "RedmondVoiceAdministrators" -ConfigScopes @{Replace="Global"}

    Set-CsAdminRole -Identity "RedmondVoiceAdministrators" -ConfigScopes @{Remove="siteRedmond"}

## Descrizione dettagliata

Il controllo di accesso basato sui ruoli (RBAC) consente agli amministratori di delegare il controllo di attività di gestione specifiche in Lync Server. Ad esempio, invece di concedere privilegi di amministrazione completi agli addetti al supporto tecnico dell'organizzazione, è possibile assegnare a tali dipendenti diritti molto specifici, ovvero il diritto di gestire solo gli account utente, il diritto di gestire solo i componenti di VoIP aziendale e il diritto di gestire solo l'archiviazione e il server di archiviazione. Inoltre, tali diritti possono essere limitati nell'ambito: ad alcuni dipendenti può essere concesso il diritto di gestire VoIP aziendale, ma solo nel sito Redmond, mentre ad altri può essere concesso il diritto di gestire gli utenti, ma solo se tali account utente sono nell'unità organizzativa Finante.

L'implementazione del controllo di accesso basato sui ruoli in Lync Server è incentrata su due elementi chiave, ovvero i gruppi di sicurezza di Attive Directory e i cmdlet di Windows PowerShell. Quando si installa Lync Server, vengono creati automaticamente diversi gruppi di sicurezza universali, tra cui CsAdministrator, CsArchivingAdministrator e CsViewOnlyAdministrator. Questi gruppi di sicurezza universali presentano una corrispondenza uno-a-uno con i ruoli RBAC, quindi qualsiasi utente incluso nel gruppo di sicurezza CsArchivingAdministrator dispone di tutti i diritti concessi al ruolo RBAC CsArchivingAdministrator. A loro volta, i diritti concessi a un ruolo RBAC si basano sui cmdlet assegnati a tale ruolo (i cmdlet possono essere assegnati a ruoli RBAC multipli). Si supponga ad esempio che a un ruolo siano stati assegnati i seguenti cmdlet:

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

Nell'elenco precedente sono riportati solo i cmdlet che possono essere eseguiti da un utente a cui è stato assegnato un ipotetico ruolo RBAC in una sessione remota di interfaccia della riga di comando Windows PowerShell. Se l'utente tenta di eseguire il cmdlet **Disable-CsUser**, il comando avrà esito negativo, in quanto gli utenti con il ruolo ipotetico non sono autorizzati a eseguire il cmdlet **Disable-CsUser**. Lo stesso vale per il Pannello di controllo di Lync Server. Ad esempio, un amministratore dell'archiviazione non può disabilitare un utente utilizzando il Pannello di controllo di Lync Server in quanto il Pannello di controllo di Lync Server si attiene ai ruoli RBAC. Ogni volta che si esegue un comando nel Pannello di controllo di Lync Server, in pratica si chiama un cmdlet di Windows PowerShell. Se non si è autorizzati a eseguire il cmdlet **Disable-CsUser**, non avrà alcuna importanza se si esegue direttamente il cmdlet da Windows PowerShell o se lo si esegue indirettamente nel Pannello di controllo di Lync Server. Il comando avrà comunque esito negativo.

RBAC si applica solo alla gestione remota. Se si è connessi a un computer in cui è in esecuzione Lync Server e si apre Lync Server Management Shell, i ruoli RBAC non verranno applicati. La sicurezza invece viene applicata principalmente tramite i gruppi di sicurezza RTCUniversalServerAdmins, RTCUniversalUserAdmins e RTCUniversalReadOnlyAdmins.

Quando si installa Lync Server, vengono creati diversi ruoli RBAC predefiniti che riguardano aree amministrative comuni quali l'amministrazione vocale, la gestione degli utenti e l'amministrazione di Response Group. Questi ruoli predefiniti non possono essere in alcun modo modificati: non è possibile aggiungere o rimuovere i cmdlet assegnati ai ruoli e non è possibile eliminare tali ruoli. Qualsiasi tentativo di eliminare un ruolo predefinito genererà un messaggio di errore. Tuttavia, è possibile utilizzare i ruoli predefiniti per creare ruoli RBAC personalizzati. Questi ruoli personalizzati possono quindi essere modificati cambiando gli ambiti amministrativi. Ad esempio, è possibile limitare il ruolo alla gestione degli account utente in una determinata unità organizzativa di Attive Directory.

I ruoli personalizzati devono essere basati su un modello: un ruolo RBAC esistente. Ad esempio, per creare un ruolo di amministratore delle conferenze telefoniche con accesso esterno, è necessario clonare un ruolo RBAC esistente. È ad esempio possibile basare il ruolo di amministratore di tali conferenze sul ruolo di amministratore dei servizi vocali esistente. Una volta creato il ruolo personalizzato, è possibile utilizzare il cmdlet **Set-CsAdminRole** per modificarne le proprietà.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente **Set-CsAdminRole cmdlet** i membri dei gruppi seguenti: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsAdminRole"}

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
<td><p>L'identificatore univoco per il ruolo RBAC da modificare. L'identità per un ruolo RBAC deve corrispondere a quella di SamAccountName per il gruppo di sicurezza universale di Active Directory associato a tale ruolo. Ad esempio, il ruolo Help Desk ha un valore Identity uguale a CsHelpDesk e CsHelpDesk è anche il valore SamAccountName del gruppo di sicurezza di Active Directory associato a tale ruolo.</p></td>
</tr>
<tr class="even">
<td><p><em>Cmdlets</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Consente di specificare i cmdlet che saranno disponibili agli utenti che dispongono del ruolo RBAC. Ad esempio, per fornire accesso a un solo cmdlet (il cmdlet <strong>Export-CsArchivingData</strong>) utilizzare una sintassi analoga alla seguente:</p>
<p>-Cmdlets &quot;Export-CsArchivingData&quot;</p>
<p>La sintassi precedente sostituisce tutti gli elementi archiviati nella proprietà Cmdlets con l'unico elemento Export-CsArchivingData. Se si desidera aggiungere il cmdlet <strong>Export-CsArchivingData</strong> ai cmdlet già archiviati in tale proprietà, utilizzare invece la sintassi seguente:</p>
<p>-Cmdlets @{Add=&quot;Export-CsArchivingData&quot;}</p>
<p>È possibile aggiungere più cmdlet separandone i nomi mediante virgole:</p>
<p>-Cmdlets @{Add=&quot;Export-CsArchivingData&quot;,&quot;Invoke-CsArchivingDatabasePurge&quot;}</p>
<p>Per rimuovere un cmdlet da un ruolo, utilizzare la sintassi seguente:</p>
<p>-Cmdlets @{Remove=&quot;Export-CsArchivingData&quot;}</p></td>
</tr>
<tr class="odd">
<td><p><em>ConfigScopes</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Limita l'ambito del cmdlet alle impostazioni di configurazione nel sito specificato. Per limitare l'ambito del cmdlet a un singolo sito, utilizzare una sintassi analoga alla seguente: -ConfigScopes site:Redmond. Per specificare più siti, utilizzare un elenco separato da virgole: -ConfigScopes &quot;site:Redmond, &quot;site:Dublin&quot;. La proprietà ConfigScopes può anche essere impostata su &quot;global&quot;.</p>
<p>Quando si assegna un valore al parametro ConfigScopes, è necessario utilizzare il prefisso &quot;site:&quot; seguito dal valore della proprietà SiteId del sito. SiteId non corrisponde necessariamente al valore del parametro Identity o DisplayName del sito. Per stabilire il valore SiteId di un determinato sito, è possibile utilizzare un comando analogo al seguente:</p>
<p>Get-CsSite &quot;Redmond&quot; | Select-Object SiteId</p>
<p>È necessario specificare un valore per una o per entrambe le proprietà ConfigScopes e UserScopes.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>ScriptModules</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Consente di specificare una funzione all'interno di uno script di Windows PowerShell che sarà quindi disponibile agli utenti che dispongono del nuovo ruolo RBAC. Ad esempio, la sintassi seguente fornisce accesso a una funzione denominata Reset in uno script denominato UpdateDatabase.ps1 :</p>
<p>-ScriptCmdlets &quot;UpdateDatabase.ps1:Reset&quot;</p>
<p>Il comando precedente sostituisce qualsiasi script attualmente archiviato nella proprietà ScriptCmdlets con la funzione Reset e lo script UpdateDatabase.ps1. Per aggiungere questo script/funzione agli elementi attualmente archiviati nella proprietà ScriptCmdlets utilizzare la sintassi seguente:</p>
<p>-ScriptCmdlets @{Add=&quot;UpdateDatabase.ps1:Reset&quot;}</p>
<p>Per rimuovere script e funzione utilizzare la sintassi seguente:</p>
<p>-ScriptCmdlets @{Add=&quot;UpdateDatabase.ps1:Reset&quot;}</p>
<p>È possibile eliminare tutti gli elementi ScriptCmdlets assegnati a un ruolo utilizzando la sintassi seguente:</p>
<p>-ScriptCmdlets $Null</p></td>
</tr>
<tr class="odd">
<td><p><em>UserScopes</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Limita l'ambito del cmdlet alle attività di gestione degli utenti nell'unità organizzativa specificata. Per limitare l'ambito del cmdlet a una singola unità organizzativa, utilizzare una sintassi analoga alla seguente: -UserScopes &quot;OU:ou=Redmond,dc=litwareinc,dc=com&quot;. Per specificare più unità organizzative, utilizzare un elenco separato da virgole: -UserScopes &quot;OU:ou=Redmond,dc=litwareinc,dc=com&quot;, &quot;OU:ou=Dublin,dc=litwareinc,dc=com&quot;. Per aggiungere nuovi ambiti o rimuovere ambiti esistenti da un ruolo, utilizzare la sintassi dei modificatori di elenco di Windows PowerShell. Per informazioni dettagliate, vedere la sezione degli esempi in questo argomento della Guida.</p>
<p>È necessario specificare un valore per una o per entrambe le proprietà ConfigScopes e UserScopes.</p></td>
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

Nessuno.

## Tipi restituiti

Il cmdlet **Set-CsAdminRole** non restituisce alcun oggetto o valore. Il cmdlet piuttosto configura le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Roles.Role.

