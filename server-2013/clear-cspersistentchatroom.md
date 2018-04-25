---
title: Clear-CsPersistentChatRoom
TOCTitle: Clear-CsPersistentChatRoom
ms:assetid: 6b7801d8-d924-4e97-9b17-ceb6a263a7a7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204976(v=OCS.15)
ms:contentKeyID: 49300885
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Clear-CsPersistentChatRoom

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove tutto il contenuto da una chat room di Chat persistente a partire dall'elemento meno recente fino alla data di fine specificata. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Clear-CsPersistentChatRoom -Identity <String> <COMMON PARAMETERS>

    Clear-CsPersistentChatRoom -Instance <ChatRoom> <COMMON PARAMETERS>

    COMMON PARAMETERS: -EndDate <DateTime> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio rimuove dalla chat room di Chat persistente ITChatRoom tutto il contenuto aggiunto entro il 1° marzo 2012 (3/1/2012).

    Clear-CsPersistentChatRoom -Identity "atl-cs-001.litwareinc.com\ITChatRoom" -EndDate "3/1/2012"

## Esempio 2

Nell'esempio 2 viene rimosso da tutte le chat room dell'organizzazione il contenuto aggiunto entro il 1° marzo 2012. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsPersistentChatRoom** senza parametri in modo da restituire una raccolta di tutte le chat room dell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Clear-CsPersistentChatRoom**, che rimuove da ogni chat room della raccolta il contenuto aggiunto entro il 1° marzo 2012. Per evitare di visualizzare la richiesta di conferma ogni volta che si tenta di cancellare una chat room diversa, viene aggiunto il parametro Confirm utilizzando la sintassi seguente:

\-Confirm:$False

    Get-CsPersistentChatRoom | Clear-CsPersistentChatRoom -EndDate "3/1/2012" -Confirm:$False

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Le discussioni di Chat persistente sono messaggi inseriti in singole chat room. Le chat room sono forum di discussione basati su argomenti specifici. Da progettazione, i messaggi inseriti in una chat room vengono conservati per sempre. Gli utenti possono tornare nella chat room in qualsiasi momento e visualizzare tutti i messaggi precedentemente inseriti.

È possibile tuttavia che a volte gli amministratori debbano cancellare tutti i messaggi di una chat room (o almeno alcuni), ad esempio per liberare spazio nel database oppure perché l'obiettivo della chat room sta cambiando. Indipendentemente dal motivo, il cmdlet **Clear-CsPersistentChatRoom** consente di eliminare tutti i messaggi di una chat room o solo i messaggi inseriti in un determinato periodo di tempo, ad esempio tutti i messaggi inseriti prima del 1° agosto 2012.

**Nota:** per rimuovere un insieme di messaggi sulla base di criteri più specifici, ad esempio tutti i messaggi inseriti da un determinato utente, utilizzare il cmdlet [Remove-CsPersistentChatMessage](remove-cspersistentchatmessage.md).

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli del controllo di accesso basato sui ruoli creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Clear-CsPersistentChatRoom"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Clear-CsPersistentChatRoom** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>EndDate</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.DateTime</p></td>
<td><p>Indica la data di fine in base alla quale deve essere rimosso il contenuto. Se ad esempio si specifica per EndDate la data 3/1/2012, ovvero 1° marzo 2012 nel formato inglese (Stati Uniti), verrà rimosso tutto il contenuto di Chat persistente aggiunto alla chat room entro il 1° marzo 2012.</p>
<p>È necessario specificare un valore per il parametro EndDate quando si esegue il cmdlet <strong>Clear-CsPersistentChatRoom</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Identità della chat room di cui deve essere rimosso il contenuto, ad esempio:</p>
<p>-Identity &quot;atl-cs-001.litwareinc.com\ITChatRoom&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ChatRoom</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando. Se si imposta il valore di questo parametro su False, non verrà visualizzata una richiesta di conferma quando si esegue il cmdlet:</p>
<p>-Confirm:$False</p></td>
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

Il cmdlet **Clear-CsPersistentChatRoom** accetta istanze dell'oggetto Microsoft.Rtc.Management.GroupChat.Cmdlets.ChatRoomObject inviate tramite pipeline.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Remove-CsPersistentChatMessage](remove-cspersistentchatmessage.md)

