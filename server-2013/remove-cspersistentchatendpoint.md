---
title: Remove-CsPersistentChatEndpoint
TOCTitle: Remove-CsPersistentChatEndpoint
ms:assetid: 0211850c-b4e7-4bb2-9a82-bfbfbd7de7b7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204626(v=OCS.15)
ms:contentKeyID: 49299493
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPersistentChatEndpoint

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un endpoint esistente di Chat persistente. Un endpoint di Chat persistente è un oggetto contatto di Active Directory che fornisce un URL descrittivo per un pool di Chat persistente di Lync Server 2013. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsPersistentChatEndpoint -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 elimina l'endpoint di Chat persistente con identità (Identity) "sip:pce@litwareinc.com". In questo esempio viene utilizzato l'indirizzo SIP per l'identità.

    Remove-CsPersistentChatEndpoint -Identity "sip:pce@litwareinc.com"

## Esempio 2

Nell'esempio 2 vengono eliminati tutti gli endpoint di Chat persistente configurati per il pool atl-pcpool-001.litwareinc.com. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsPersistentChatEndpoint** e il parametro PoolFqdn per restituire tutti gli endpoint per il pool atl-pcpool-001.litwareinc.com. Gli endpoint della raccolta vengono quindi inviati tramite pipe al cmdlet **Remove-CsPersistentChatEndpoint**, che li rimuove.

    Get-CsPersistentChatEndpoint -PoolFqdn "atl-pcpool-001.litwareinc.com" | Remove-CsPersistentChatEndpoint

## Esempio 3

Il comando riportato nell'esempio 3 elimina tutti gli endpoint di Chat persistente configurati per l'utilizzo nell'organizzazione. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsPersistentChatEndpoint** per restituire una raccolta di tutti gli endpoint di Chat persistente. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsPersistentChatEndpoint**, che elimina ogni endpoint in essa contenuto.

    Get-CsPersistentChatEndpoint | Remove-CsPersistentChatEndpoint

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Se però sono presenti utenti che eseguono client legacy, ad esempio Microsoft Lync 2010, è possibile che per tali utenti gli URI di Chat persistente predefiniti siano difficili da utilizzare per far puntare il client legacy al pool. Per questo motivo gli amministratori possono utilizzare il cmdlet [New-CsPersistentChatEndpoint](new-cspersistentchatendpoint.md) per creare per il pool un oggetto contatto aggiuntivo che fornisca un URI più descrittivo e più facile da utilizzare. Questi endpoint possono essere rimossi successivamente utilizzando il cmdlet **Remove-CsPersistentChatEndpoint**.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPersistentChatEndpoint"}

Pannello di controllo di Lync Server: le funzioni eseguite dal cmdlet **Remove-CsPersistentChatEndpoint** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Identificatore univoco dell'endpoint di Chat persistente da rimuovere. Le identità (Identity) degli endpoint in genere vengono specificate utilizzando l'indirizzo SIP o il nome visualizzato dell'endpoint, ad esempio:</p>
<p>-Identity &quot;sip:pcEndpoint1@litwareinc.com&quot;</p>
<p>È tuttavia possibile utilizzare anche l'identità completa dell'endpoint, ad esempio:</p>
<p>-Identity &quot;CN={33e5014b-dcba-46b5-9bf7-48f4d5fca69d}, CN=Application Contacts,CN=RTC Service,CN=Services,CN=Configuration,DC=litwareinc,DC=com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
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

Il cmdlet **Remove-CsPersistentChatEndpoint** accetta le istanze della classe Microsoft.Rtc.Management.ADConnect.Schema.OCSPersistentChatContact inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsPersistentChatEndpoint** non restituisce oggetti o dati.

## Vedere anche

#### Ulteriori risorse

[Get-CsPersistentChatEndpoint](get-cspersistentchatendpoint.md)  
[New-CsPersistentChatEndpoint](new-cspersistentchatendpoint.md)

