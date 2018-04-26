---
title: Remove-CsPersistentChatAddin
TOCTitle: Remove-CsPersistentChatAddin
ms:assetid: e218e88a-326e-4405-ba58-4d34b41191b4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205350(v=OCS.15)
ms:contentKeyID: 49302250
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPersistentChatAddin

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un componente aggiuntivo esistente di Chat persistente. Un componente aggiuntivo di Chat persistente è una pagina Web personalizzata che può essere incorporata in un client di Chat persistente. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsPersistentChatAddin -Identity <String> <COMMON PARAMETERS>

    Remove-CsPersistentChatAddin -Instance <Addin> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Nell'esempio 1 viene rimosso il componente aggiuntivo di Chat persistente ITChatAddin presente nel pool atl-cs-001.litwareinc.com.

    Remove-CsPersistentChatAddin -Identity "atl-cs-001.litwareinc.com\ITChatAddin"

## Esempio 2

Il comando riportato nell'esempio 2 rimuove i componenti aggiuntivi di Chat persistente attualmente in uso nell'organizzazione. A tale scopo, il primo comando utilizza il cmdlet **Get-CsPersistentChatAddin** per restituire una raccolta di tutti i componenti aggiuntivi di Chat persistente attualmente in uso. Questa raccolta viene inviata tramite pipe al cmdlet **Remove-CsPersistentChatAddin** che, quindi, elimina ogni componente aggiuntivo nella raccolta.

    Get-CsPersistentChatAddin | Remove-CsPersistentChatAddin

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

I componenti aggiuntivi vengono utilizzati come estensioni di una chat room di Chat persistente. Si tratta di applicazioni esterne, ovvero elementi non incorporati in Chat persistente, associate a una chat room specifica. Ad esempio, una chat room dell'helpdesk può includere un URL che si collega a una pagina Web o a un'applicazione Silverlight che mostra lo stato delle richieste di assistenza della giornata. I cmdlet dell'interfaccia della riga di comando Windows PowerShell di Lync Server non consentono di creare questi componenti aggiuntivi. Vengono utilizzati invece i cmdlet **CsPersistentChatAddin** per associare o dissociare un componente aggiuntivo da una chat room.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPersistentChatAddin"}

**Pannello di controllo di Lync Server:** Per rimuovere un componente aggiuntivo di Chat persistente utilizzando il Pannello di controllo di Lync Server, fare clic su **Chat persistente** e quindi su **Componente aggiuntivo**. Selezionare il componente aggiuntivo da rimuovere, fare clic su **Modifica** e quindi fare clic su **Elimina**.

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
<td><p>Identificatore univoco per il componente aggiuntivo di Chat persistente da rimuovere. L'identità è composta dal nome di dominio completo del pool di Chat persistente in cui il componente aggiuntivo è posizionato, un carattere &quot;\&quot; e il nome del componente aggiuntivo. Ad esempio:</p>
<p>-Identity &quot;atl-gc-001.litwareincom\ITPersistentChatAddin&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.Addin</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di visualizzare una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando; ad esempio, se si tenta di rimuovere un componente aggiuntivo attualmente associato a una o più chat room.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Remove-CsPersistentChatAddin** accetta le istanze da pipeline dell'oggetto Microsoft.Rtc.Management.PersistentChat.Cmdlets.AddinObject. Il cmdlet accetta inoltre un valore stringa che rappresenta l'identità di un componente aggiuntivo esistente.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsPersistentChatAddin** elimina invece le istanze esistenti dell'oggetto Microsoft.Rtc.Management.PersistentChat.Cmdlets.AddinObject.

## Vedere anche

#### Ulteriori risorse

[Get-CsPersistentChatAddin](get-cspersistentchataddin.md)  
[New-CsPersistentChatAddin](new-cspersistentchataddin.md)  
[Set-CsPersistentChatAddin](set-cspersistentchataddin.md)

