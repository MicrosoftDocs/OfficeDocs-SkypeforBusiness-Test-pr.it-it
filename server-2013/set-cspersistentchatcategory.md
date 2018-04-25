---
title: Set-CsPersistentChatCategory
TOCTitle: Set-CsPersistentChatCategory
ms:assetid: 61f44b61-c1bb-46a8-af12-8d1c543fcda5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204952(v=OCS.15)
ms:contentKeyID: 49300756
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPersistentChatCategory

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una categoria esistente di Chat persistente. Una categoria di Chat persistente rappresenta una raccolta di chat room di Chat persistente. Ogni chat room deve essere associata a una categoria. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsPersistentChatCategory -Instance <Category> <COMMON PARAMETERS>

    Set-CsPersistentChatCategory -Identity <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AllowedMembers <PSListModifier>] [-AsObject <SwitchParameter>] [-ChatHistory <$true | $false>] [-Confirm [<SwitchParameter>]] [-Creators <PSListModifier>] [-DeniedMembers <PSListModifier>] [-Description <String>] [-FileUpload <$true | $false>] [-Invitations <$true | $false>] [-Name <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Nell'esempio 1 vengono disabilitati i caricamenti dei file per la categoria di Chat persistente atl-cs-001.litwareinc.com\\helpdesk.

    Set-CsPersistentChatCategory -Identity "atl-cs-001.litwareinc.com\helpdesk" -FileUpload $False

## Esempio 2

Nell'esempio 2 vengono disabilitati i caricamenti dei file per tutte le categorie di Chat persistente in uso nell'organizzazione. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsPersistentChatCategory** senza parametri per restituire una raccolta di tutte le categorie di Chat persistente. Le categorie della raccolta vengono quindi inviate tramite pipe al cmdlet **Set-CsPersistentChatCategory** per disabilitare i caricamenti dei file per ogni categoria.

    Get-CsPersistentChatCategory | Set-CsPersistentChatCategory-FileUpload $False

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Le categorie di Chat persistente consentono agli amministratori di organizzare e gestire le chat room di Chat persistente. Utilizzando le categorie gli amministratori possono raggruppare le chat room correlate. Tutte le chat room utilizzate dal reparto amministrativo ad esempio possono essere raggruppate nella stessa categoria. Analogamente, le categorie consentono agli amministratori di gestire le autorizzazioni per le chat room, specificando gli utenti autorizzati ad accedere alle chat room, gli utenti a cui è negato l'accesso alle chat room e gli utenti a cui è consentito creare nuove chat room nella categoria.

Si noti che tutte le chat room devono appartenere a una categoria. Non è possibile creare una chat room senza assegnarla a una categoria. È necessario pertanto creare almeno una categoria prima di aggiungere una chat room all'implementazione di Chat persistente.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli del controllo di accesso basato sui ruoli creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPersistentChatCategory"}

**Pannello di controllo di Lync Server:** per modificare una categoria esistente di Chat persistente utilizzando il Pannello di controllo di Lync Server, fare clic su **Chat persistente** e su **Categoria**, quindi fare doppio clic sulla categoria da modificare.

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
<td><p>Identificatore univoco della categoria di chat room. L'identità (Identity) è costituita dal pool di Chat persistente in cui è contenuta la categoria e dal nome di categoria, ad esempio:</p>
<p>-Identity &quot;atl-gc-001.litwareinc.com\ITChat&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.Category</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowedMembers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Elenca gli utenti autorizzati ad accedere alle chat room incluse nella categoria. Per aggiungere un nuovo utente all'elenco Members, utilizzare una sintassi simile alla seguente:</p>
<p>-Members @{Add=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>È possibile aggiungere più utenti separando i relativi indirizzi SIP con le virgole:</p>
<p>-Members @{Add=&quot;sip:kenmyer@litwareinc.com&quot;, &quot;sip:pilar@litwareinc.com&quot;}</p>
<p>Per rimuovere un utente dall'elenco Members, utilizzare il metodo Remove:</p>
<p>-Members @{Remove=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>Per rimuovere tutti gli utenti dall'elenco Members, impostare il valore della proprietà Members su Null:</p>
<p>-AllowedMembers $Null</p>
<p>Oltre a utilizzare singoli utenti, è possibile utilizzare un'intera unità organizzativa. Il comando seguente ad esempio consente a tutti gli utenti dell'unità organizzativa (OU) IT di accedere alle chat room:</p>
<p>-Members @{Add=&quot;OU=IT,DC=litwareinc,DC=com&quot;}</p>
<p>Per aggiungere tutti gli utenti di una lista di distribuzione, utilizzare il nome distinto Active Directory della lista di distribuzione:</p>
<p>-Members @{Add=&quot;CN=ChatSupportGroup,OU=IT,DC=litwareinc,DC=com&quot;}</p></td>
</tr>
<tr class="even">
<td><p><em>AsObject</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se viene specificato questo parametro, vengono utilizzati i nomi visualizzati di Active Directory quando si aggiungono o si rimuovono utenti dagli elenchi AllowedMembers, DeniedMembers e Creators. Se invece il parametro non viene specificato, vengono utilizzati gli indirizzi SIP per gestire questi elenchi.</p></td>
</tr>
<tr class="odd">
<td><p><em>ChatHistory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su False ($False), verrà disabilitata per la nuova categoria la funzionalità di cronologia delle chat. La cronologia delle chat in genere è disabilitata solo per le chat room utilizzate per gli annunci che vengono inseriti una volta e che non devono più essere utilizzati come riferimento.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Creators</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Elenca gli utenti autorizzati a creare chat room incluse nella categoria. Per aggiungere un nuovo utente all'elenco Creators, utilizzare una sintassi simile alla seguente:</p>
<p>-Creators @{Add=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>È possibile aggiungere più utenti separando i relativi indirizzi SIP con le virgole:</p>
<p>-Creators @{Add=&quot;sip:kenmyer@litwareinc.com&quot;, &quot;sip:pilar@litwareinc.com&quot;}</p>
<p>Per rimuovere un utente dall'elenco Creators, utilizzare il metodo Remove:</p>
<p>-Creators @{Remove=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>Per rimuovere tutti gli utenti dall'elenco Creators, impostare il valore della proprietà Creators su Null:</p>
<p>-Creators $Null</p>
<p>Oltre a utilizzare singoli utenti, è possibile utilizzare un'intera unità organizzativa. Il comando seguente ad esempio consente a tutti gli utenti dell'unità organizzativa (OU) IT di creare chat room:</p>
<p>-Creators @{Add=&quot;OU=IT,DC=litwareinc,DC=com&quot;}</p>
<p>Per aggiungere tutti gli utenti di una lista di distribuzione, utilizzare il nome distinto Active Directory della lista di distribuzione:</p>
<p>-Creators @{Add=&quot;CN=ChatSupportGroup.OU=IT,DC=litwareinc,DC=com&quot;}</p></td>
</tr>
<tr class="even">
<td><p><em>DeniedMembers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Elenca gli utenti non autorizzati ad accedere alle chat room incluse nella categoria. Per aggiungere un nuovo utente all'elenco DeniedMembers, utilizzare una sintassi simile alla seguente:</p>
<p>-DeniedMembers @{Add=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>È possibile aggiungere più utenti separando i relativi indirizzi SIP con le virgole:</p>
<p>-DeniedMembers @{Add=&quot;sip:kenmyer@litwareinc.com&quot;, &quot;sip:pilar@litwareinc.com&quot;}</p>
<p>Per rimuovere un utente dall'elenco DeniedMembers, utilizzare il metodo Remove:</p>
<p>-DeniedMembers @{Remove=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>Per rimuovere tutti gli utenti dall'elenco DeniedMembers, impostare il valore della proprietà DeniedMembers su Null:</p>
<p>-DeniedMembers $Null</p>
<p>Oltre a utilizzare singoli utenti, è possibile utilizzare un'intera unità organizzativa. Il comando seguente ad esempio impedisce a tutti gli utenti dell'unità organizzativa (OU) IT di accedere alle chat room:</p>
<p>-DeniedMembers @{Add=&quot;OU=IT,DC=litwareinc,DC=com&quot;}</p>
<p>Per impedire l'accesso a tutti gli utenti di una lista di distribuzione, utilizzare il nome distinto Active Directory della lista di distribuzione:</p>
<p>-DeniedMembers @{Add=&quot;CN=ChatSupportGroup.OU=IT,DC=litwareinc,DC=com&quot;}</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Testo aggiuntivo per la categoria di Chat persistente. Description può ad esempio illustrare lo scopo della categoria e il tipo di chat room previste per la categoria.</p></td>
</tr>
<tr class="even">
<td><p><em>FileUpload</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True ($True), questo parametro consente i caricamenti di file nelle chat room della categoria.</p></td>
</tr>
<tr class="odd">
<td><p><em>Invitations</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su False ($False), vengono abilitati gli inviti per la categoria. In questo modo tra l'altro gli utenti inclusi nell'elenco AllowedMembers riceveranno automaticamente un invito ad accedere alla nuova chat room al momento della creazione della chat room.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome assegnato alla categoria di Chat persistente. I nomi devono essere univoci per ogni pool di Chat persistente.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Set-CsPersistentChatCategory** accetta istanze dell'oggetto Microsoft.Rtc.Management.PersistentChat.Cmdlets.CategoryObject inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsPersistentChatCategory** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.PersistentChat.Cmdlets.CategoryObject.

## Vedere anche

#### Ulteriori risorse

[Get-CsPersistentChatCategory](get-cspersistentchatcategory.md)  
[New-CsPersistentChatCategory](new-cspersistentchatcategory.md)  
[Remove-CsPersistentChatCategory](remove-cspersistentchatcategory.md)

