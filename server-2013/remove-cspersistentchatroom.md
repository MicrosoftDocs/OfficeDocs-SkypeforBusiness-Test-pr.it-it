---
title: Remove-CsPersistentChatRoom
TOCTitle: Remove-CsPersistentChatRoom
ms:assetid: 04cadd5d-13dc-4de5-b0b5-8c2f9bbbc7a7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204639(v=OCS.15)
ms:contentKeyID: 49299539
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPersistentChatRoom

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una o più chat room di Chat persistente. Una chat room è un forum di discussione in cui viene trattato in genere un argomento specifico. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsPersistentChatRoom -Identity <String> <COMMON PARAMETERS>

    Remove-CsPersistentChatRoom -Instance <ChatRoom> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 rimuove la chat room di Chat persistente RedmondChatRoom.

    Remove-CsPersistentChatRoom -Identity "atl-gc-001.litwareinc.com\RedmondChatRoom"

## Esempio 2

Nell'esempio 2 vengono rimosse tutte le chat room di Chat persistente in uso nell'organizzazione. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsPersistentChatRoom** senza parametri per restituire una raccolta di tutte le chat room disponibili. La raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsPersistentChatRoom**, che elimina ogni chat room inclusa nella raccolta.

    Get-CsPersistentChatRoom  | Remove-CsPersistentChatRoom

## Esempio 3

Nell'esempio 3 vengono rimosse tutte le chat room "chiuse". Una chat room viene definita "chiusa" se qualsiasi utente può individuarla eseguendo una ricerca di directory, ma solo i membri possono partecipare alle relative attività. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsPersistentChatRoom** e il parametro Privacy per restituire una raccolta di tutte le chat room chiuse. La raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsPersistentChatConfiguration**, che elimina ogni chat room inclusa nella raccolta.

    Get-CsPersistentChatRoom -Privacy "Closed"  | Remove-CsPersistentChatRoom

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Le discussioni di Chat persistente sono messaggi inseriti in singole chat room. Le chat room sono forum di discussione basati su argomenti specifici. Da progettazione, i messaggi inseriti in una chat room vengono conservati per sempre. Gli utenti possono tornare nella chat room in qualsiasi momento e visualizzare tutti i messaggi precedentemente inseriti.

Il cmdlet **Remove-CsPersistentChatRoom** consente agli amministratori di rimuovere una o più chat room di Chat persistente configurate per l'utilizzo nell'organizzazione.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPersistentChatRoom"}

**Pannello di controllo di Lync Server:** per eliminare una chat room di Chat persistente esistente utilizzando il Pannello di controllo di Lync Server, fare clic su **Chat persistente**, su **Stanza** e quindi selezionare la chat room da eliminare. Per eliminare la chat room, fare clic su **Modifica** e quindi su **Elimina**.

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
<td><p>Identificatore univoco della chat room di Chat persistente da rimuovere. L'identità di una chat room è costituita dal pool di Chat persistente in cui è stata configurata la chat room e dal nome della chat room, ad esempio:</p>
<p>-Identity &quot;atl-gc-001.litwareinc.com\RedmondChatRoom&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoom</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
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

Il cmdlet **Remove-CsPersistentChatRooms** accetta le istanze dell'oggetto Microsoft.Rtc.Management.PersistentChat.Cmdlets.ChatRoomObject inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsPersistentChatRoom** invece elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.PersistentChat.Cmdlets.ChatRoomObject.

## Vedere anche

#### Ulteriori risorse

[Clear-CsPersistentChatRoom](clear-cspersistentchatroom.md)  
[Get-CsPersistentChatRoom](get-cspersistentchatroom.md)  
[New-CsPersistentChatRoom](new-cspersistentchatroom.md)  
[Set-CsPersistentChatRoom](set-cspersistentchatroom.md)

