---
title: Get-CsPersistentChatEligiblePrincipal
TOCTitle: Get-CsPersistentChatEligiblePrincipal
ms:assetid: 541de778-3aca-4d3f-9d46-d9b6d8212987
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204891(v=OCS.15)
ms:contentKeyID: 49300595
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPersistentChatEligiblePrincipal

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce le entità idonee per una categoria o una chat room di Chat persistente. Tra le entità idonee sono inclusi i membri o i responsabili consentiti (per una categoria di chat room), nonché i relatori consentiti (solo per le chat room). Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsPersistentChatEligiblePrincipal -Category <String> <COMMON PARAMETERS>

    Get-CsPersistentChatEligiblePrincipal -Room <String> [-Presenters <SwitchParameter>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Filter <String>] [-PersistentChatPoolFqdn <String>] [-ResultSize <Int32>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce informazioni sulle entità idonee per la categoria di Chat persistente ITChat.

    Get-CsPersistentChatEligiblePrincipal -PersistentChatPoolFqdn "atl-persistentchat-001.litwareinc.com" -Category "ITChat"

## Esempio 2

Nell'esempio 2 vengono restituite informazioni per tutti i relatori idonei per la chat room HelpDeskChatRoom.

    Get-CsPersistentChatEligiblePrincipal -PersistentChatPoolFqdn "atl-persistentchat-001.litwareinc.com" -Room "HelpDeskChatRoom" -Presenters

## Esempio 3

L'esempio 3 è una variante del comando riportato nell'esempio 2. In questo esempio tuttavia vengono restituite informazioni solo per i relatori di Chat persistente che non rappresentano account utente. A tale scopo, viene utilizzato innanzitutto il cmdlet **Get-CsPersistentChatEligiblePrincipal** per restituire tutti i relatori della chat room HelpDeskChatRoom. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i relatori in cui la proprietà PersistentChatPrincipalType è diversa da (-ne) "user".

    Get-CsPersistentChatEligiblePrincipal -PersistentChatPoolFqdn "atl-persistentchat-001.litwareinc.com" -Room "HelpDeskChatRoom" -Presenters | Where-Object {$_.PersistentChatPrincipalType -ne "user"}

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Le categorie di chat consentono di specificare alcuni utenti come creatori, ovvero utenti autorizzati a creare chat room all'interno della categoria. Analogamente, le chat room consentono di specificare gli utenti come responsabili e/o come relatori. Per l'assegnazione di uno di questi ruoli, è necessario però che gli utenti in questione siano inclusi nell'elenco AllowedMembers della categoria o chat room specificata. Per recuperare l'elenco dei membri consentiti per una chat room o una categoria, è possibile utilizzare i cmdlet [Get-CsPersistentChatRoom](get-cspersistentchatroom.md) e [Get-CsPersistentChatCategory](get-cspersistentchatcategory.md). Se tuttavia all'elenco dei membri consentiti è stato aggiunto un gruppo di sicurezza, un dominio o un'unità organizzativa, non verranno visualizzati i nomi dei relativi utenti. Se ad esempio nell'elenco dei membri consentiti è incluso il gruppo di sicurezza FinanceManagers, non saranno visibili i nomi degli utenti appartenenti a tale gruppo. Verrà visualizzato solo il nome del gruppo.

Per visualizzare il nome di tutti gli utenti del gruppo, nonché i nomi di tutti gli utenti dell'elenco dei membri consentiti di una categoria o di una chat room, utilizzare invece **Get-CsPersistentChatEligiblePrincipal**.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPersistentChatEligiblePrincipal"}

Pannello di controllo di Lync Server: le funzioni eseguite dal cmdlet **Get-CsPersistentChatEligiblePrincipal** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Nome della categoria di Group Chat di cui devono essere restituite le entità idonee. È necessario utilizzare il parametro Category o Room quando si effettua la chiamata al cmdlet <strong>Get-CsPersistentChatEligiblePrincipal</strong>. Non è possibile tuttavia utilizzare entrambi i parametri nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Room</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome della chat room di Group Chat di cui devono essere restituite le entità idonee. È necessario utilizzare il parametro Category o Room quando si effettua la chiamata al cmdlet <strong>Get-CsPersistentChatEligiblePrincipal</strong>. Non è possibile tuttavia utilizzare entrambi i parametri nello stesso comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di applicare un filtro in base alle entità idonee utilizzando una ricerca con caratteri jolly, ad esempio:</p>
<p>-Filter &quot;*smith*&quot;</p>
<p>Si noti che il parametro Filter consente di applicare un filtro solo in base agli indirizzi SIP degli utenti.</p></td>
</tr>
<tr class="even">
<td><p><em>PersistentChatPoolFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del pool di Chat persistente, ad esempio:</p>
<p>-PersistentChatPoolFqdn &quot;atl-persistentchat-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Presenters</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se si include questo parametro nel comando, vengono restituiti i relatori idonei di una chat room di Chat persistente. Se invece non si include il parametro nel comando, il cmdlet <strong>Get-CsPersistentChatEligiblePrincipal</strong> restituisce i membri e i responsabili idonei.</p>
<p>Questo parametro può essere utilizzato solo insieme al parametro Room e può restituire informazioni solo per le chat room configurate come auditorium.</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Consente di limitare il numero di record restituiti dal cmdlet. Per restituire ad esempio sette entità di Chat persistente (indipendentemente dal numero di utenti contenuti nella foresta), includere il parametro ResultSize e impostare il relativo valore su 7. Si noti che non è possibile stabilire quali saranno le sette entità restituite.</p>
<p>La dimensione del risultato può essere impostata su un numero intero compreso tra 0 e 2147483647, estremi inclusi. Se si imposta il parametro su 0, il comando verrà eseguito ma non restituirà dati. Se si imposta ResultSize su 7 ma la foresta include solo tre entità, il comando restituirà le tre entità e verrà completato senza errori.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsPersistentChatEligiblePrincipal** non accetta dati da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsPersistentChatEligiblePrincipal** restituisce istanze dell'oggetto Microsoft.Rtc.Management.GroupChat.Cmdlets.ADPersistentChatPrincipal.

## Vedere anche

#### Ulteriori risorse

[Set-CsPersistentChatCategory](set-cspersistentchatcategory.md)  
[New-CsPersistentChatRoom](new-cspersistentchatroom.md)

