---
title: Set-CsPersistentChatRoom
TOCTitle: Set-CsPersistentChatRoom
ms:assetid: 3774931e-74a9-4189-9dde-3baae2293138
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204801(v=OCS.15)
ms:contentKeyID: 49300204
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPersistentChatRoom

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una chat room esistente di Chat persistente. Una chat room è un forum di discussione in cui viene trattato in genere un argomento specifico. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsPersistentChatRoom -Instance <ChatRoom> <COMMON PARAMETERS>

    Set-CsPersistentChatRoom -Identity <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Addin <String>] [-AsObject <SwitchParameter>] [-Category <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Disabled <$true | $false>] [-Force <SwitchParameter>] [-Invitations <False | Inherit>] [-Managers <PSListModifier>] [-Members <PSListModifier>] [-Name <String>] [-Presenters <PSListModifier>] [-Privacy <Open | Closed | Secret>] [-Type <Normal | Auditorium>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 disabilita la chat room di Chat persistente con identità (Identity) atl-cs-001.litwareinc.com\\ITChatRoom.

    Set-CsPersistentChatRoom -Identity "atl-cs-001.litwareinc.com\ITChatRoom" -Disabled $True

## Esempio 2

Nell'esempio 2 vengono disabilitate tutte le chat room di Chat persistente del pool atl-cs-001.litwareinc.com. A tale scopo, vengono utilizzati innanzitutto il cmdlet **Get-CsPersistentChatRoom** e il parametro Identity per restituire tutte le chat room configurate per il pool atl-cs-001.litwareinc.com. Queste chat room vengono quindi inviate tramite pipe al cmdlet **Set-CsPersistentChatRoom**, che imposta la proprietà Disabled di ogni chat room su True ($True).

    Get-CsPersistentChatRoom -PersistentChatPoolFqdn "atl-cs-001.litwareinc.com" | Set-CsPersistentChatRoom -Disabled $True

## Esempio 3

Nell'esempio 3 vengono disabilitate tutte le chat room di Chat persistente dell'organizzazione. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsPersistentChatRoom** senza parametri per restituire una raccolta di tutte le chat room di Chat persistente. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsPersistentChatRoom**, che disabilita ogni chat room della raccolta.

    Get-CsPersistentChatRoom | Set-CsPersistentChatRoom -Disabled $True

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Le discussioni di Chat persistente sono messaggi inseriti in singole chat room. Le chat room sono forum di discussione basati su argomenti specifici. Da progettazione, i messaggi inseriti in una chat room vengono conservati per sempre. Gli utenti possono tornare nella chat room in qualsiasi momento e visualizzare tutti i messaggi precedentemente inseriti.

Il cmdlet **Set-CsPersistentChatRoom** consente di modificare una, più o tutte le chat room configurate per l'utilizzo nell'organizzazione, ad esempio assegnando responsabili e relatori a una chat room.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPersistentChatRoom"}

**Pannello di controllo di Lync Server:** per modificare una chat room esistente di Chat persistente utilizzando il Pannello di controllo di Lync Server, fare clic su **Chat persistente** e su **Stanza**. Fare quindi doppio clic quindi sulla chat room da modificare.

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
<td><p>Identificatore univoco della chat room di Chat persistente da modificare. L'identità di una chat room è costituita dal pool di Chat persistente in cui è stata configurata la chat room e dal nome della chat room, ad esempio:</p>
<p>-Identity &quot;atl-gc-001.litwareinc.com\RedmondChatRoom&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoom</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Addin</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome dell'eventuale componente aggiuntivo di Chat persistente associato alla chat room. Un componente aggiuntivo di Chat persistente è una pagina Web personalizzata che può essere incorporata in un client di Chat persistente. I componenti aggiuntivi possono essere creati utilizzando il cmdlet <strong>New-CsPersistentChatAddin</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>AsObject</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se viene specificato questo parametro, vengono utilizzati i nomi visualizzati di Active Directory quando si aggiungono o si rimuovono utenti dall'elenco Managers o Presenters. Se invece il parametro non viene specificato, vengono utilizzati gli indirizzi SIP per gestire questi elenchi.</p></td>
</tr>
<tr class="odd">
<td><p><em>Category</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Categoria a cui appartiene la chat room, ad esempio:</p>
<p>-Category &quot;IT&quot;</p>
<p>Si noti che è necessario specificare una categoria già esistente, altrimenti il comando avrà esito negativo. Le categorie, che rappresentano una raccolta di chat room, possono essere create utilizzando il cmdlet <strong>New-CsPersistentChatCategory</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire informazioni aggiuntive sulla nuova chat room.</p></td>
</tr>
<tr class="even">
<td><p><em>Disabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True ($True), la nuova chat room sarà disabilitata e non sarà disponibile per l'utilizzo quando verrà creata. Se invece non si utilizza questo parametro, la nuova chat room sarà abilitata e disponibile per l'utilizzo immediato.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Invitations</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoomInvitations</p></td>
<td><p>Specifica se gli inviti per la chat room verranno ereditati dalla categoria. In questo modo tra l'altro gli utenti inclusi nell'elenco Members riceveranno automaticamente un invito ad accedere alla nuova chat room al momento della creazione della chat room. Se si imposta il parametro su False, non verranno utilizzati inviti per la chat room. Se invece si utilizza il valore Inherit per il parametro, la chat room utilizzerà l'impostazione di Invitations specificata per la categoria di appartenenza.</p></td>
</tr>
<tr class="odd">
<td><p><em>Managers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Elenco di utenti autorizzati a definire le appartenenze alla chat room e a configurare altre impostazioni per la chat room.</p>
<p>Per aggiungere un nuovo utente all'elenco Managers, utilizzare una sintassi simile alla seguente:</p>
<p>-Managers @{Add=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>È possibile aggiungere più utenti separando i relativi indirizzi SIP con le virgole:</p>
<p>-Managers @{Add=&quot;sip:kenmyer@litwareinc.com&quot;, &quot;sip:pilar@litwareinc.com&quot;}</p>
<p>Per rimuovere un utente dall'elenco Managers, utilizzare il metodo Remove:</p>
<p>-Managers @{Remove=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>Per rimuovere tutti gli utenti dall'elenco Managers, impostare il valore della proprietà Managers su Null:</p>
<p>-Managers $Null</p>
<p>Oltre a utilizzare singoli utenti, è possibile utilizzare un'intera unità organizzativa. Il comando seguente ad esempio aggiunge tutti gli utenti dell'unità organizzativa (OU) IT all'elenco Managers:</p>
<p>-Managers @{Add=&quot;OU=IT,DC=litwareinc,DC=com&quot;}</p>
<p>Per definire tutti gli utenti di una chat room di una lista di distribuzione come responsabili (Managers), utilizzare il nome distinto Active Directory della lista di distribuzione:</p>
<p>-Managers @{Add=&quot;CN=ChatSupportGroup,OU=IT,DC=litwareinc,DC=com&quot;}</p></td>
</tr>
<tr class="even">
<td><p><em>Members</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Elenco di utenti a cui è consentito accedere alla chat room. Se la proprietà Members è impostata su Null, la chat room erediterà l'elenco di appartenenze dalla relativa categoria di Chat persistente.</p>
<p>Per aggiungere un nuovo utente all'elenco Members, utilizzare una sintassi simile alla seguente:</p>
<p>-Members @{Add=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>È possibile aggiungere più utenti separando i relativi indirizzi SIP con le virgole:</p>
<p>-Members @{Add=&quot;sip:kenmyer@litwareinc.com&quot;, &quot;sip:pilar@litwareinc.com&quot;}</p>
<p>Per rimuovere un utente dall'elenco Members, utilizzare il metodo Remove:</p>
<p>-Members @{Remove=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>Per rimuovere tutti gli utenti dall'elenco Members, impostare il valore della proprietà Members su Null:</p>
<p>-Members $Null</p>
<p>Oltre a utilizzare singoli utenti, è possibile utilizzare un'intera unità organizzativa. Il comando seguente ad esempio aggiunge tutti gli utenti dell'unità organizzativa (OU) IT all'elenco Members:</p>
<p>-Members @{Add=&quot;OU=IT,DC=litwareinc,DC=com&quot;}</p>
<p>Per definire tutti gli utenti di una chat room di una lista di distribuzione come membri (Members), utilizzare il nome distinto Active Directory della lista di distribuzione:</p>
<p>-Members @{Add=&quot;CN=ChatSupportGroup,OU=IT,DC=litwareinc,DC=com&quot;}</p></td>
</tr>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome della chat room di Chat persistente. I nomi devono essere univoci per ogni pool di Chat persistente.</p></td>
</tr>
<tr class="even">
<td><p><em>Presenters</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Elenco di utenti autorizzati a inserire messaggi in una chat room auditorium.</p>
<p>Per aggiungere un nuovo utente all'elenco Presenters, utilizzare una sintassi simile alla seguente:</p>
<p>-Presenters @{Add=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>È possibile aggiungere più utenti separando i relativi indirizzi SIP con le virgole:</p>
<p>-Presenters @{Add=&quot;sip:kenmyer@litwareinc.com&quot;, &quot;sip:pilar@litwareinc.com&quot;}</p>
<p>Per rimuovere un utente dall'elenco Presenters, utilizzare il metodo Remove:</p>
<p>-Presenters @{Remove=&quot;sip:kenmyer@litwareinc.com&quot;}</p>
<p>Per rimuovere tutti gli utenti dall'elenco Presenters, impostare il valore della proprietà Presenters su Null:</p>
<p>-Presenters $Null</p>
<p>Oltre a utilizzare singoli utenti, è possibile utilizzare un'intera unità organizzativa. Il comando seguente ad esempio aggiunge tutti gli utenti dell'unità organizzativa (OU) IT all'elenco Presenters:</p>
<p>-Presenters @{Add=&quot;OU=IT,DC=litwareinc,DC=com&quot;}</p>
<p>Per definire tutti gli utenti di una chat room di una lista di distribuzione come relatori (Presenters), utilizzare il nome distinto Active Directory della lista di distribuzione:</p>
<p>-Presenters @{Add=&quot;CN=ChatSupportGroup,OU=IT,DC=litwareinc,DC=com&quot;}</p></td>
</tr>
<tr class="odd">
<td><p><em>Privacy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoomPrivacy</p></td>
<td><p>Impostazioni di privacy della chat room. I valori consentiti sono:</p>
<p>* Open (tutti gli utenti possono individuare la chat room eseguendo una ricerca di directory e possono partecipare alle relative attività)</p>
<p>* Secret (solo i membri della chat room possono individuare la chat room eseguendo una ricerca di directory e possono partecipare alle relative attività)</p>
<p>* Closed (tutti gli utenti possono individuare la chat room eseguendo una ricerca di directory, ma solo i membri possono partecipare alle relative attività)</p></td>
</tr>
<tr class="even">
<td><p><em>Type</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoomType</p></td>
<td><p>Specifica se la chat room è configurata come Normal (in cui tutti i membri possono inserire messaggi) o come Auditorium (in cui solo i relatori possono inserire messaggi), ad esempio:</p>
<p>-Type &quot;Auditorium&quot;</p>
<p>Il valore predefinito è Normal.</p></td>
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

Il cmdlet **Set-CsPersistentChatRoom** accetta le istanze dell'oggetto Microsoft.Rtc.Management.PersistentChat.Cmdlets.ChatRoomObject inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsPersistentChatRoom** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.PersistentChat.Cmdlets.ChatRoomObject.

## Vedere anche

#### Ulteriori risorse

[Clear-CsPersistentChatRoom](clear-cspersistentchatroom.md)  
[Get-CsPersistentChatRoom](get-cspersistentchatroom.md)  
[New-CsPersistentChatRoom](new-cspersistentchatroom.md)  
[Remove-CsPersistentChatRoom](remove-cspersistentchatroom.md)

