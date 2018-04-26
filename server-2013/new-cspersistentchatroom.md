---
title: New-CsPersistentChatRoom
TOCTitle: New-CsPersistentChatRoom
ms:assetid: b00d353b-5b5b-40d6-b952-3c35170fbf8a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205166(v=OCS.15)
ms:contentKeyID: 49301678
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPersistentChatRoom

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova chat room di Chat persistente. Una chat room è un forum di discussione in cui viene trattato in genere un argomento specifico. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    New-CsPersistentChatRoom -Category <String> -Name <String> [-Addin <String>] [-Description <String>] [-Disabled <$true | $false>] [-Invitations <False | Inherit>] [-PersistentChatPoolFqdn <String>] [-Privacy <Open | Closed | Secret>] [-Type <Normal | Auditorium>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 crea una nuova chat room di Chat persistente denominata ITChatRoom nel pool atl-cs-001.litwareinc.com. In questo esempio la chat room viene aggiunta alla categoria IT.

    New-CsPersistentChatRoom -Name "ITChatRoom" -PersistentChatPoolFqdn "atl-cs-001.litwareinc.com"-Category "IT"

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Le discussioni di Chat persistente sono messaggi inseriti in singole chat room. Le chat room sono forum di discussione basati su argomenti specifici. Da progettazione, i messaggi inseriti in una chat room vengono conservati per sempre. Gli utenti possono tornare nella chat room in qualsiasi momento e visualizzare tutti i messaggi precedentemente inseriti.

Il cmdlet **New-CsPersistentChatRoom** consente agli amministratori di creare nuove chat room di Chat persistente. Si noti che utilizzando il cmdlet **New-CsPersistentChatRoom** non sono disponibili tutte le proprietà di una chat room. Non è possibile ad esempio assegnare responsabili o relatori di chat room. A tale scopo, è necessario creare la chat room e quindi effettuare le assegnazioni utilizzando il cmdlet [Set-CsPersistentChatRoom](set-cspersistentchatroom.md).

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPersistentChatRoom"}

**Pannello di controllo di Lync Server:** per creare una nuova chat room di Chat persistente utilizzando il Pannello di controllo di Lync Server, fare clic su **Chat persistente**, su **Stanza** e quindi su **Nuovo**.

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
<td><p><em>Category</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Categoria in cui deve essere creata la chat room. Ad esempio:</p>
<p>-Category &quot;IT&quot;</p>
<p>La categoria specificata deve essere già presente, altrimenti il comando avrà esito negativo. Le categorie, che sono raccolte di chat room di Chat persistente, possono essere create utilizzando il cmdlet <strong>New-CsPersistentChatCategory</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome della nuova chat room di Chat persistente. I nomi devono essere univoci per pool di Chat persistente.</p></td>
</tr>
<tr class="odd">
<td><p><em>Addin</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome del componente aggiuntivo di Chat persistente associato alla chat room. Un componente aggiuntivo di Chat persistente è una pagina Web personalizzata che può essere incorporata in un client di Chat persistente. I componenti aggiuntivi possono essere creati utilizzando il cmdlet <strong>New-CsPersistentChatAddin</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire informazioni aggiuntive sulla nuova chat room.</p></td>
</tr>
<tr class="odd">
<td><p><em>Disabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se questo parametro è presente, la nuova chat room verrà disabilitata e non sarà disponibile per l'utilizzo quando viene creata. Se questo parametro non viene utilizzato, la nuova chat room verrà abilitata e sarà immediatamente disponibile per l'utilizzo.</p></td>
</tr>
<tr class="even">
<td><p><em>Invitations</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoomInvitations</p></td>
<td><p>Specifica se gli inviti per la nuova chat room verranno ereditati dalla categoria. Tra l'altro, questo significa che gli utenti presenti nell'elenco AllowedMembers riceveranno automaticamente un invito a partecipare a una nuova chat room quando questa viene creata.</p></td>
</tr>
<tr class="odd">
<td><p><em>PersistentChatPoolFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del pool di Chat persistente in cui verrà inserita la nuova chat room. Ad esempio:</p>
<p>-PersistentChatPoolFqdn &quot;atl-gc-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Privacy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoomPrivacy</p></td>
<td><p>Impostazioni di privacy per la nuova chat room. I valori consentiti sono:</p>
<p>* Open (qualsiasi utente può individuare la chat room eseguendo una ricerca nella directory e chiunque può partecipare alle attività della chat room)</p>
<p>* Secret (solo i membri della chat room possono individuarla eseguendo una ricerca nella directory e solo i membri possono partecipare alle attività della chat room)</p>
<p>* Closed (qualsiasi utente può individuare la chat room eseguendo una ricerca nella directory, ma solo i membri possono partecipare alle attività della chat room)</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoomType</p></td>
<td><p>Specifica se la nuova chat room deve essere configurata come chat room normale (in cui tutti i membri possono inserire messaggi) o come chat room di tipo auditorium (in cui solo i relatori possono inserire messaggi). Ad esempio:</p>
<p>-Type &quot;Auditorium&quot;</p>
<p>Il valore predefinito è Normal.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsPersistentChatRoom** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **New-CsPersistentChatRoom** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.PersistentChat.Cmdlets.ChatRoomObject.

## Vedere anche

#### Ulteriori risorse

[Clear-CsPersistentChatRoom](clear-cspersistentchatroom.md)  
[Get-CsPersistentChatRoom](get-cspersistentchatroom.md)  
[Remove-CsPersistentChatRoom](remove-cspersistentchatroom.md)  
[Set-CsPersistentChatRoom](set-cspersistentchatroom.md)

