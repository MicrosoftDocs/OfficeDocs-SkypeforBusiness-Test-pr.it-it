---
title: Get-CsPersistentChatRoom
TOCTitle: Get-CsPersistentChatRoom
ms:assetid: 9826c44b-35a6-473e-97d4-952415d640d1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205123(v=OCS.15)
ms:contentKeyID: 49301401
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPersistentChatRoom

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle chat room di Chat persistente configurate per l'utilizzo nell'organizzazione. Una chat room è un forum di discussione che in genere riguarda un argomento specifico. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsPersistentChatRoom [-Addin <String>] [-Category <String>] [-ChatContentExceedsMB <Int32>] [-Disabled <$true | $false>] [-Filter <String>] [-Invitations <False | Inherit>] [-Manager <String>] [-Member <String>] [-PersistentChatPoolFqdn <String>] [-Privacy <Open | Closed | Secret>] [-ResultSize <Int32>] [-SearchDescription <SwitchParameter>] [-Type <Normal | Auditorium>] <COMMON PARAMETERS>

    Get-CsPersistentChatRoom [-Identity <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AsObject <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce le informazioni su tutte le chat room di Chat persistente configurate per l'utilizzo nell'organizzazione.

    Get-CsPersistentChatRoom

## Esempio 2

Nell'esempio 2 vengono restituite le informazioni su una singola chat room di Chat persistente, ovvero la chat room con l'identità atl-cs-001.litwareinc.com\\ITChatRoom.

    Get-CsPersistentChatRoom -Identity "atl-cs-001.litwareinc.com\ITChatRoom"

## Esempio 3

Nell'esempio 3 vengono restituite le informazioni su tutte le chat room di Chat persistente configurate per il pool atl-cs-001.litwareinc.com.

    Get-CsPersistentChatRoom -PersistentChatPoolFqdn "atl-cs-001.litwareinc.com"

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Le discussioni di Chat persistente sono messaggi inseriti in singole chat room. Le chat room sono forum di discussione basati su argomenti specifici. Da progettazione, i messaggi inseriti in una chat room vengono conservati per sempre. Gli utenti possono tornare nella chat room in qualsiasi momento e visualizzare tutti i messaggi precedentemente inseriti.

Il cmdlet **Get-CsPersistentChatRoom** consente di restituire informazioni su tutte le chat room configurate per l'utilizzo nell'organizzazione..

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPersistentChatRoom"}

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
<td><p><em>Addin</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Restituisce le chat room associate al componente aggiuntivo di chat room specificato.</p>
<p>È possibile specificare un solo componente aggiuntivo per comando.</p></td>
</tr>
<tr class="even">
<td><p><em>AsObject</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se viene specificato questo parametro, vengono utilizzati i nomi visualizzati di Active Directory per mostrare gli utenti contenuti nell'elenco Managers o Presenters. Se invece il parametro non viene specificato, vengono utilizzati gli indirizzi SIP per mostrare gli utenti.</p></td>
</tr>
<tr class="odd">
<td><p><em>Category</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Restituisce le informazioni su tutte le chat room di Chat persistente incluse nella categoria specificata. Ad esempio:</p>
<p>-Category &quot;ITChat&quot;</p>
<p>È possibile specificare una sola categoria quando si utilizza il parametro Category. Non è inoltre possibile utilizzare i parametri PersistentChatPoolFqdn, Filter o Identity in qualsiasi comando in cui venga utilizzato il parametro Category.</p></td>
</tr>
<tr class="even">
<td><p><em>ChatContentExceedsMB</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Restituisce le chat room il cui contenuto cumulativo superi il valore specificato, in megabyte.</p></td>
</tr>
<tr class="odd">
<td><p><em>Disabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Consente di ricercare le chat room attive (specificando il valore $False) oppure le chat room disabilitate (specificando il valore $True).</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di restituire le informazioni sulle chat room di Chat persistente in base al nome e/o alla descrizione della chat room. Per restituire le informazioni su una chat room con un nome specifico, utilizzare una sintassi simile alla seguente:</p>
<p>-Filter {Name –like &quot;ITChat&quot;}</p>
<p>Tale sintassi restituisce solo le informazioni relative alle chat room con il nome ITChat.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Identificatore univoco della chat room di Chat persistente da restituire. L'identità di una chat room è costituita dal pool di Chat persistente in cui la chat room è stata configurata e dal nome della chat room. Ad esempio:</p>
<p>-Identity &quot;atl-gc-001.litwareinc.com\RedmondChatRoom&quot;</p>
<p>Non è possibile utilizzare il parametro Category, Filter o PersistentChatPoolFqdn nei comandi in cui viene utilizzato il parametro Identity. Se si chiama il cmdlet <strong>Get-CsPersistentChatRoom</strong> senza alcun parametro, verranno restituite informazioni su tutte le chat room configurate per l'utilizzo nell'organizzazione.</p></td>
</tr>
<tr class="even">
<td><p><em>Invitations</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoomInvitations</p></td>
<td><p>Restituisce le chat room in cui vengono utilizzati inviti (specificando il valore Inherit) oppure le chat room in cui non vengono utilizzati inviti (specificando il valore False).</p></td>
</tr>
<tr class="odd">
<td><p><em>Manager</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Restituisce le chat room gestite dall'utente specificato. Ad esempio:</p>
<p>-Manager &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>È possibile specificare un solo responsabile per comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Member</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Restituisce le chat room di cui l'utente specificato è membro. Ad esempio:</p>
<p>-Member &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>È possibile specificare un solo membro per comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>PersistentChatPoolFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Restituisce le informazioni su tutte le chat room di Chat persistente configurate nel pool di Chat persistente specificato. Ad esempio:</p>
<p>-PersistentChatPoolFqdn &quot;atl-gc-001.litwareinc.com&quot;</p>
<p>Non è possibile utilizzare i parametri Category, Filter o Identity in qualsiasi comando in cui venga utilizzato il parametro PersistentChatPoolFqdn.</p></td>
</tr>
<tr class="even">
<td><p><em>Privacy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoomPrivacy</p></td>
<td><p>Consente di restituire le chat room che soddisfano l'impostazione di privacy specificata. I valori consentiti sono:</p>
<p>* Open (qualsiasi utente può individuare la chat room eseguendo una ricerca nella directory e chiunque può partecipare alle attività della chat room)</p>
<p>* Secret (solo i membri della chat room possono individuarla eseguendo una ricerca nella directory e solo i membri possono partecipare alle attività della chat room)</p>
<p>* Closed (qualsiasi utente può individuare la chat room eseguendo una ricerca nella directory, ma solo i membri possono partecipare alle attività della chat room)</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Consente di limitare il numero di record restituiti dal cmdlet. Ad esempio, per restituire sette chat room (indipendentemente dal numero di chat room nella foresta), includere il parametro ResultSize e impostarne il valore su 7. Non c'è modo di stabilire quali sette chat room verranno restituite.</p>
<p>La dimensione del risultato può essere impostata su qualsiasi numero intero compreso tra 0 e 2147483647 (inclusi). Se l'impostazione è 0, il comando viene eseguito, ma non restituisce dati. Se si imposta ResultSize su 7 ma nella foresta sono presenti solo tre chat room, il comando restituirà le tre chat room e quindi verrà completato senza errori.</p></td>
</tr>
<tr class="even">
<td><p><em>SearchDescription</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di ricercare il valore di testo specificato nel nome o nella descrizione della chat room. Per ricercare sia il nome sia la descrizione, includere il parametro SearchDescription insieme al parametro Filter. Ad esempio:</p>
<p>-SearchDescription –Filter &quot;IT chat room&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoomType</p></td>
<td><p>Restituisce le chat room in base al tipo. I valori consentiti sono:</p>
<p>* Normal (chat room in cui tutti i membri possono inserire messaggi)</p>
<p>* Auditorium (chat room in cui solo i relatori possono inserire messaggi)</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsPersistentChatRoom** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsPersistentChatRoom** restituisce istanze dell'oggetto Microsoft.Rtc.Management.PersistentChat.Cmdlets.ChatRoomObject.

## Vedere anche

#### Ulteriori risorse

[Clear-CsPersistentChatRoom](clear-cspersistentchatroom.md)  
[New-CsPersistentChatRoom](new-cspersistentchatroom.md)  
[Remove-CsPersistentChatRoom](remove-cspersistentchatroom.md)  
[Set-CsPersistentChatRoom](set-cspersistentchatroom.md)

