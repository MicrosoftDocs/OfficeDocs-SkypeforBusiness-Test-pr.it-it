---
title: Remove-CsPersistentChatCategory
TOCTitle: Remove-CsPersistentChatCategory
ms:assetid: 09d2c1e6-07b6-47c2-b48f-f0c8bdfa1507
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204660(v=OCS.15)
ms:contentKeyID: 49299622
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPersistentChatCategory

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una categoria esistente di Chat persistente. Una categoria di Chat persistente rappresenta una raccolta di chat room di Chat persistente e ogni chat room deve essere associata a una categoria. Questo cmdlet è stato introdotto in Lync Server 2013. Non è possibile rimuovere le categorie a meno che non siano vuote. Per rimuovere una categoria devono essere state rimosse tutte le chat room in essa contenute.

## Sintassi

    Remove-CsPersistentChatCategory -Identity <String> <COMMON PARAMETERS>

    Remove-CsPersistentChatCategory -Instance <Category> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 rimuove la categoria di Chat persistente con identità (Identity) "atl-cs-001.litwareinc.com\\helpdesk".

    Remove-CsPersistentChatCategory -Identity "atl-cs-001.litwareinc.com\helpdesk"

## Esempio 2

Nell'esempio 2 vengono rimosse tutte le categorie di Chat persistente attualmente in uso nell'organizzazione. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsPersistentChatCategory** per recuperare una raccolta di tutte le categorie di Chat persistente. Questa raccolta viene inviata tramite pipe al cmdlet **Remove-CsPersistentChatCategory**, che quindi elimina ogni categoria inclusa nella raccolta.

    Get-CsPersistentChatCategory | Remove-CsPersistentChatCategory

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Le categorie di Chat persistente consentono agli amministratori di organizzare e gestire le chat room di Chat persistente. Utilizzando le categorie gli amministratori possono raggruppare le chat room correlate. Tutte le chat room utilizzate dal reparto amministrativo ad esempio possono essere raggruppate nella stessa categoria. Analogamente, le categorie consentono agli amministratori di gestire le autorizzazioni per le chat room, specificando gli utenti autorizzati ad accedere alle chat room, gli utenti a cui è negato l'accesso alle chat room e gli utenti a cui è consentito creare nuove chat room nella categoria.

Si noti che tutte le chat room devono appartenere a una categoria. Non è possibile creare una chat room senza assegnarla a una categoria. È necessario pertanto creare almeno una categoria prima di aggiungere una chat room all'implementazione di Chat persistente.

Il cmdlet **Remove-CsPersistentChatCategory** consente di rimuovere le categorie di Chat persistente. Considerare che le categorie possono essere rimosse solo se sono vuote. È necessario pertanto rimuovere tutte le chat room di una categoria prima di poter rimuovere la categoria stessa.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPersistentChatCategory"}

**Pannello di controllo di Lync Server:** per rimuovere una categoria di Chat persistente utilizzando il Pannello di controllo di Lync Server, fare clic su **Chat persistente** e quindi su **Categoria**. Selezionare la categoria da rimuovere, fare clic su **Modifica** e quindi su **Elimina**.

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
<td><p>Identificatore univoco della categoria di Chat persistente da rimuovere. Un'identità (Identity) è costituita dal valore del parametro PoolFqdn e dal nome di categoria, ad esempio:</p>
<p>-Identity &quot;atl-cs-001.litwareinc.com\helpdesk&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.Category</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Remove-CsPersistentChatCategory** accetta le istanze dell'oggetto Microsoft.Rtc.Management.PersistentChat.Cmdlets.CategoryObject inviate tramite pipeline. Il cmdlet accetterà inoltre valori stringa che rappresentano l'identità di una categoria esistente di Chat persistente.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsPersistentChatCategory** invece elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.PersistentChat.Cmdlets.CategoryObject.

## Vedere anche

#### Ulteriori risorse

[Get-CsPersistentChatCategory](get-cspersistentchatcategory.md)  
[New-CsPersistentChatCategory](new-cspersistentchatcategory.md)  
[Set-CsPersistentChatCategory](set-cspersistentchatcategory.md)

