---
title: Get-CsPersistentChatCategory
TOCTitle: Get-CsPersistentChatCategory
ms:assetid: 2ec14091-cb05-4c4c-b091-b7e88f5ca3cf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204771(v=OCS.15)
ms:contentKeyID: 49300057
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPersistentChatCategory

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle categorie di Chat persistente in uso nell'organizzazione. Una categoria di Chat persistente rappresenta una raccolta di chat room di Chat persistente. Ogni chat room deve essere associata a una categoria. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsPersistentChatCategory [-PersistentChatPoolFqdn <String>] <COMMON PARAMETERS>

    Get-CsPersistentChatCategory -Identity <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AsObject <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce informazioni su tutte le categorie di Chat persistente configurate per l'utilizzo nell'organizzazione.

    Get-CsPersistentChatCategory

## Esempio 2

Nell'esempio 2 vengono restituite informazioni su tutte le categorie di Chat persistente configurate per l'utilizzo nel pool atl-cs-001.litwareinc.com.

    Get-CsPersistentChatCategory -PersistentChatPoolFqdn "atl-cs-001.litwareinc.com"

## Esempio 3

Nell'esempio 3 vengono restituite informazioni su tutte le categorie di Chat persistente in cui la proprietà Invites è stata impostata su False. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsPersistentChatCategory** per restituire una raccolta di tutte le categorie di Chat persistente. La raccolta viene quindi inviata tramite pipe al cmdlet Where-Object, che seleziona solo le categorie in cui la proprietà Invites è impostata su False ($False).

    Get-CsPersistentChatCategory | Where-Object {$_.Invites -eq $False}

## Esempio 4

Nell'esempio 4 vengono restituite informazioni su tutte le categorie di Chat persistente in cui Ken Myer è elencato come uno dei creatori. A tale scopo, viene innanzitutto utilizzato il cmdlet **Get-CsPersistentChatCategory** per restituire una raccolta di tutte le categorie di Chat persistente. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona tutte le categorie in cui la proprietà Creators include (-contains) il nome "Ken Myer".

    Get-CsPersistentChatCategory | Where-Object {$_.Creators -contains "Ken Myer"}

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Le categorie di Chat persistente consentono agli amministratori di organizzare e gestire le chat room di Chat persistente. Utilizzando le categorie gli amministratori possono raggruppare le chat room correlate. Tutte le chat room utilizzate dal reparto amministrativo ad esempio possono essere raggruppate nella stessa categoria. Analogamente, le categorie consentono agli amministratori di gestire le autorizzazioni per le chat room, specificando gli utenti autorizzati ad accedere alle chat room, gli utenti a cui è negato l'accesso alle chat room e gli utenti a cui è consentito creare nuove chat room nella categoria.

Si noti che tutte le chat room devono appartenere a una categoria. Non è possibile creare una chat room senza assegnarla a una categoria. È necessario pertanto creare almeno una categoria prima di aggiungere una chat room all'implementazione di Chat persistente.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPersistentChatCategory"}

**Pannello di controllo di Lync Server:** per visualizzare le categorie di Chat persistente nel Pannello di controllo di Lync Server, fare clic su **Chat persistente** e quindi su **Categoria**.

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
<td><p><em>AsObject</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se viene specificato questo parametro, vengono utilizzati i nomi visualizzati di Active Directory per mostrare gli utenti contenuti nell'elenco AllowedMembers, DeniedMembers o Creators. Se invece il parametro non viene specificato, vengono utilizzati gli indirizzi SIP per mostrare gli utenti.</p></td>
</tr>
<tr class="odd">
<td><p><em>PersistentChatPoolFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del pool di Chat persistente che ospita categorie di Chat persistente. Se si utilizza il parametro PoolFqdn senza includere il parametro Name, verranno restituite informazioni su tutte le categorie di Chat persistente del pool specificato. Se si omettono i parametri Name e PoolFqdn, verranno restituite informazioni su tutte le categorie di Chat persistente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsPersistentChatCategory** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsPersistentChatCategory** restituisce istanze dell'oggetto Microsoft.Rtc.Management.PersistentChat.Cmdlets.CategoryObject.

## Vedere anche

#### Ulteriori risorse

[New-CsPersistentChatCategory](new-cspersistentchatcategory.md)  
[Remove-CsPersistentChatCategory](remove-cspersistentchatcategory.md)  
[Set-CsPersistentChatCategory](set-cspersistentchatcategory.md)

