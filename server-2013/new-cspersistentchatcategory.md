---
title: New-CsPersistentChatCategory
TOCTitle: New-CsPersistentChatCategory
ms:assetid: 37a6f55d-0fec-480f-8d96-60c313a48c74
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204803(v=OCS.15)
ms:contentKeyID: 49300195
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPersistentChatCategory

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova categoria di Chat persistente. Una categoria di Chat persistente rappresenta una raccolta di chat room di Chat persistente. Ogni chat room deve essere associata a una categoria. Non è possibile assegnare chat room a una categoria nel momento in cui questa viene creata. Le chat room esistenti devono invece essere assegnate successivamente a una categoria utilizzando il cmdlet **Set-CsPersistentChatRoom**. Le nuove chat room tuttavia possono essere assegnate alla categoria nel momento in cui vengono create. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    New-CsPersistentChatCategory -Name <String> [-Description <String>] [-EnableFileUpload <SwitchParameter>] [-EnableInvitations <SwitchParameter>] [-PersistentChatPoolFqdn <String>] [-RemoveChatHistory <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 crea una nuova categoria di Chat persistente denominata HelpDesk nel pool atl-cs-001.litwareinc.com. In questo esempio viene abilitato il caricamento dei file includendo il parametro EnableFileUpload.

    New-CsPersistentChatCategory -Name "HelpDesk" -PersistentChatPoolFqdn "atl-cs-001.litwareinc.com" -EnableFileUpload 

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Le categorie di Chat persistente consentono agli amministratori di organizzare e gestire le chat room di Chat persistente. Utilizzando le categorie gli amministratori possono raggruppare le chat room correlate. Tutte le chat room utilizzate dal reparto amministrativo ad esempio possono essere raggruppate nella stessa categoria. Analogamente, le categorie consentono agli amministratori di gestire le autorizzazioni per le chat room, specificando gli utenti autorizzati ad accedere alle chat room, gli utenti a cui è negato l'accesso alle chat room e gli utenti a cui è consentito creare nuove chat room nella categoria.

Si noti che tutte le chat room devono appartenere a una categoria. Non è possibile creare una chat room senza assegnarla a una categoria. È necessario pertanto creare almeno una categoria prima di aggiungere una chat room all'implementazione di Chat persistente.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPersistentChatCategory"}

**Pannello di controllo di Lync Server:** per creare una nuova categoria di Chat persistente utilizzando il Pannello di controllo di Lync Server, fare clic su **Chat persistente**, su **Categoria** e quindi su **Nuovo**.

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
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome assegnato alla categoria di Chat persistente. I nomi devono essere univoci per ogni pool di Chat persistente.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Testo aggiuntivo per la categoria di Chat persistente. Description può ad esempio illustrare lo scopo della categoria e il tipo di chat room previste per la categoria.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableFileUpload</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, questo parametro consente i caricamenti di file nelle chat room della categoria.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableInvitations</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se si specifica questo parametro, vengono abilitati gli inviti per la categoria. In questo modo tra l'altro gli utenti inclusi nell'elenco AllowedMembers riceveranno automaticamente un invito ad accedere alla nuova chat room al momento della creazione della chat room.</p></td>
</tr>
<tr class="odd">
<td><p><em>PersistentChatPoolFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del pool di Chat persistente in cui deve essere creata la categoria.</p></td>
</tr>
<tr class="even">
<td><p><em>RemoveChatHistory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se si include questo parametro, verrà disabilitata per la nuova categoria la funzionalità di cronologia delle chat. La cronologia delle chat in genere è disabilitata solo per le chat room utilizzate per gli annunci che vengono inseriti una volta e che non devono più essere utilizzati come riferimento.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsPersistentChatCategory** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsPersistentChatCategory** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.PersistentChat.Cmdlets.CategoryObject.

## Vedere anche

#### Ulteriori risorse

[Get-CsPersistentChatCategory](get-cspersistentchatcategory.md)  
[Remove-CsPersistentChatCategory](remove-cspersistentchatcategory.md)  
[Set-CsPersistentChatCategory](set-cspersistentchatcategory.md)

