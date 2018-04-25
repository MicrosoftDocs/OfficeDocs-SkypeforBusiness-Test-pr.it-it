---
title: Remove-CsPersistentChatMessage
TOCTitle: Remove-CsPersistentChatMessage
ms:assetid: 0cb53905-4608-44a9-ba3d-ba51fc90d65e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204668(v=OCS.15)
ms:contentKeyID: 49299662
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPersistentChatMessage

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Sostituisce uno o più messaggi di Chat persistente nel database di Chat persistente con un messaggio predefinito o fornito dall'amministratore. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsPersistentChatMessage -ReplaceMessage <String> [-CaseSensitive <$true | $false>] [-EndDate <DateTime>] [-Filter <String>] [-MatchClause <And | Or | Exact>] [-StartDate <DateTime>] [-UserUri <String>] <COMMON PARAMETERS>

    Remove-CsPersistentChatMessage -Remove <SwitchParameter> [-CaseSensitive <$true | $false>] [-EndDate <DateTime>] [-Filter <String>] [-MatchClause <And | Or | Exact>] [-StartDate <DateTime>] [-UserUri <String>] <COMMON PARAMETERS>

    Remove-CsPersistentChatMessage [-CaseSensitive <$true | $false>] [-EndDate <DateTime>] [-Filter <String>] [-MatchClause <And | Or | Exact>] [-StartDate <DateTime>] [-UserUri <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -Identity <String> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 rimuove dalla chat room ITChatRoom del server atl-persistentchat-001.litwareinc.com tutti i messaggi di Chat persistente inseriti prima del 1° aprile 2012 (4/1/2012).

    Remove-CsPersistentChatMessage -Identity "atl-persistentchat-001.litwareinc.com\ITChatRoom" -EndDate "4/1/2012"

## Esempio 2

Nell'esempio 2 vengono rimossi dalla chat room ITChatRoom del server atl-persistentchat-001.litwareinc.com tutti i messaggi di Chat persistente inseriti dall'utente kenmyer@litwareinc.com.

    Remove-CsPersistentChatMessage -Identity "atl-persistentchat-001.litwareinc.com\ITChatRoom" -UserUri "sip:kenmyer@litwareinc.com"

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Le discussioni di Chat persistente sono messaggi inseriti in singole chat room. Le chat room sono forum di discussione basati su argomenti specifici. Da progettazione, i messaggi inseriti in una chat room vengono conservati per sempre. Gli utenti possono tornare nella chat room in qualsiasi momento e visualizzare tutti i messaggi precedentemente inseriti.

È possibile tuttavia che un amministratore desideri rimuovere messaggi da una chat room, ad esempio se un utente ha inserito una serie di messaggi contenenti informazioni errate su un'imminente riunione aziendale. Il cmdlet **Remove-CsPersisentChatMessage** consente agli amministratori di rimuovere un singolo messaggio o un insieme di messaggi di chat in base a criteri quali l'utente che ha inserito il messaggio o le parole chiave contenute nel messaggio.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPersistentChatMessage"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Remove-CsPersistentChatMessage** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Identificatore univoco della chat room contenente il messaggio da eliminare, ad esempio:</p>
<p>-Identity &quot;atl-persistentchat-001.litwareinc.com\ITChatRoom&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Remove</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se viene specificato, questo parametro rimuove il messaggio di Chat persistente senza lasciare un messaggio sostitutivo.</p>
<p>Non è possibile utilizzare i parametri Remove e ReplaceMessage nello stesso comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReplaceMessage</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di specificare il testo del messaggio sostitutivo. Per impostazione predefinita, viene utilizzato il testo che indica che il messaggio è stato sostituito dall'amministratore di Chat persistente.</p></td>
</tr>
<tr class="even">
<td><p><em>CaseSensitive</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se questo parametro viene specificato, indica che deve essere rispettata la distinzione tra maiuscole e minuscole per la ricerca dei messaggi da rimuovere. In altri termini, una &quot;A&quot; maiuscola verrà considerata come carattere diverso da una &quot;a&quot; minuscola. Per impostazione predefinita, nelle ricerche non viene rispettata la distinzione tra maiuscole e minuscole.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>EndDate</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.DateTime</p></td>
<td><p>Consente di applicare un filtro in base ai messaggi inseriti nella data specificata o prima di tale data.</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>È possibile utilizzare parole chiave per identificare i messaggi da eliminare. Per cercare ad esempio tutti i messaggi che includono la parola chiave &quot;Fabrikam&quot;, utilizzare la sintassi seguente:</p>
<p>-Filter &quot;Fabrikam&quot;</p>
<p>Per cercare più parole chiave, inserirle tutte in una singola stringa separandole con spazi:</p>
<p>-Filter &quot;Fabrikam Contoso TailspinToys&quot;</p>
<p>Per impostazione predefinita, il cmdlet <strong>Remove-CsPersistentChatMessage</strong> cercherà i messaggi utilizzando tutte le parole chiave specificate. Per eseguire la ricerca di messaggi utilizzando una delle parole chiave fornite, utilizzare il parametro MatchClause e impostarlo su &quot;Or&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>MatchClause</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.RemoveOcsMessageChatCmdlet+AndOr</p></td>
<td><p>Specifica il modo in cui il cmdlet <strong>Remove-CsPersistentChatMessage</strong> gestisce più parole chiave. I valori consentiti sono i seguenti:</p>
<p>* All (vengono restituiti i messaggi che includono tutte le parole chiave specificate)</p>
<p>* Or (vengono restituiti i messaggi che includono una o più parole chiave tra quelle specificate)</p>
<p>* Exact (vengono restituiti i messaggi che corrispondono esattamente alla frase specificata, incluso l'ordine delle parole)</p>
<p>La sintassi seguente ad esempio cerca i messaggi che includono nel testo la frase esatta &quot;For internal use only&quot;:</p>
<p>-Filter &quot;For internal use only&quot; –MatchClause &quot;Exact&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>StartDate</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.DateTime</p></td>
<td><p>Consente di applicare un filtro in base ai messaggi inseriti nella data specificata o dopo tale data.</p></td>
</tr>
<tr class="even">
<td><p><em>UserUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo SIP dell'utente che ha inserito il messaggio o i messaggi da rimuovere.</p></td>
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

Nessuno. Il cmdlet **Remove-CsPersistentChatMessage** non accetta input da pipeline.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Clear-CsPersistentChatRoom](clear-cspersistentchatroom.md)

