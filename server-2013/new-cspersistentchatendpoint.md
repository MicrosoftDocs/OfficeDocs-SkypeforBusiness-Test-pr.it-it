---
title: New-CsPersistentChatEndpoint
TOCTitle: New-CsPersistentChatEndpoint
ms:assetid: 3a3a7acc-3239-4140-8005-ef72ab2f61e1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204811(v=OCS.15)
ms:contentKeyID: 49300251
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPersistentChatEndpoint

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo endpoint di Chat persistente. Un endpoint di questo tipo è un oggetto contatto di Active Directory che fornisce un URL descrittivo per un pool di Chat persistente di Lync Server 2013. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    New-CsPersistentChatEndpoint -PersistentChatPoolFqdn <Fqdn> -SipAddress <String> [-Confirm [<SwitchParameter>]] [-DisplayName <String>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 crea un nuovo endpoint di Chat persistente per il pool atl-pcpool-001.litwareinc.com. Questo nuovo endpoint ha come indirizzo SIP "sip:pce@litwareinc.com" e come nome visualizzato "Persistent Chat Endpoint 1".

    New-CsPersistentChatEndpoint -SipAddress "sip:pce@litwareinc.com" -PersistentChatPoolFqdn "atl-pcpool-001.litwareinc.com" -DisplayName "Persistent Chat Endpoint 1"

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Se tuttavia sono presenti utenti che eseguono client legacy, ad esempio Microsoft Lync 2010, è possibile che per tali utenti gli URI di Chat persistente predefiniti siano difficili da gestire e utilizzare per far puntare il client legacy al pool. Per questo motivo gli amministratori possono utilizzare il cmdlet **New-CsPersistentChatEndpoint** per creare per il pool un oggetto contatto aggiuntivo che fornisca un URI più descrittivo e più facile da utilizzare.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPersistentChatEndpoint"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **New-CsPersistentChatEndpoint** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>PersistentChatPoolFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del pool di Chat persistente a cui verrà associato il nuovo endpoint, ad esempio:</p>
<p>-PersistentChatPoolFqdn &quot;atl-pc-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>SipAddress</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Identificatore univoco che consente all'endpoint di comunicare con dispositivi SIP come Lync 2013. L'indirizzo SIP deve utilizzare il prefisso sip: e un dominio SIP valido. Ad esempio:</p>
<p>-SipAddress &quot;sip:pcEndpoint1@litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome visualizzato di Active Directory per il nuovo oggetto contatto.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di passare tramite la pipeline un oggetto contatto che rappresenta il nuovo endpoint di Chat persistente. Per impostazione predefinita, il cmdlet <strong>New-CsPersistentChatEndpoint</strong> non passa oggetti tramite pipeline.</p></td>
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

Nessuno. Il cmdlet **New-CsPersistentChatEndpoint** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsPersistentChatEndpoint** crea nuove istanze della classe Microsoft.Rtc.Management.ADConnect.Schema.OCSPersistentChatContact.

## Vedere anche

#### Ulteriori risorse

[Get-CsPersistentChatEndpoint](get-cspersistentchatendpoint.md)  
[Remove-CsPersistentChatEndpoint](remove-cspersistentchatendpoint.md)

