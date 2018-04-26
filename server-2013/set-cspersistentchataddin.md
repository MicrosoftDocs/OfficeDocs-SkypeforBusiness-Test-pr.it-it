---
title: Set-CsPersistentChatAddin
TOCTitle: Set-CsPersistentChatAddin
ms:assetid: 1badd6b5-e519-47a1-9434-9fa5a00b79ff
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204721(v=OCS.15)
ms:contentKeyID: 49299846
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPersistentChatAddin

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un componente aggiuntivo esistente di Chat persistente. Un componente aggiuntivo di Chat persistente è una pagina Web personalizzata che può essere incorporata in un client di Chat persistente.Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsPersistentChatAddin -Instance <Addin> <COMMON PARAMETERS>

    Set-CsPersistentChatAddin -Identity <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Name <String>] [-Url <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Nell'esempio 1 viene modificato l'URL assegnato al componente aggiuntivo di Chat persistente ITPersistentChatAddin. In questo caso l'URL cambia in http://atl-cs-001.litwareinc.com/itchat2.

    Set-CsPersistentChatAddin -Identity "atl-cs-001.litwareinc.com\ITPersistentChatAddin" -Url "http://atl-cs-001.litwareinc.com/itchat2"

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

I componenti aggiuntivi vengono utilizzati come estensioni di una chat room di Chat persistente. Si tratta di applicazioni esterne, ovvero elementi non incorporati in Chat persistente, associate a una chat room specifica. Ad esempio, una chat room del supporto tecnico può includere un URL che si collega a una pagina Web o a un'applicazione Silverlight che mostra lo stato delle richieste di assistenza della giornata. I cmdlet dell'interfaccia della riga di comando Windows PowerShell per Lync Server non consentono di creare questi componenti aggiuntivi. Vengono utilizzati invece i cmdlet **CsPersistentChatAddin** per associare o dissociare un componente aggiuntivo da una chat room.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPersistentChatAddin"}

**Pannello di controllo di Lync Server:** per modificare un componente aggiuntivo esistente di Chat persistente utilizzando il Pannello di controllo di Lync Server, fare clic su **Chat persistente** e su **Componente aggiuntivo**. Fare quindi doppio clic sul componente aggiuntivo da modificare.

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
<td><p>Identificatore univoco del componente aggiuntivo di Chat persistente. L'identità (Identity) è costituita dal nome di dominio completo del pool di Chat persistente in cui si trova il componente aggiuntivo, da un carattere &quot;\&quot; e dal nome del componente aggiuntivo, ad esempio:</p>
<p>-Identity &quot;atl-gc-001.litwareincom\ITPersistentChatAddin&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.Addin</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome descrittivo assegnato al componente aggiuntivo di Chat persistente. I nomi devono essere univoci per ogni pool di Chat persistente.</p></td>
</tr>
<tr class="odd">
<td><p><em>Url</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL della pagina Web che deve essere visualizzata con il componente aggiuntivo di Chat persistente.</p></td>
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

Il cmdlet **Set-CsPersistentChatAddin** accetta le istanze dell'oggetto Microsoft.Rtc.Management.PersistentChat.Cmdlets.AddinObject inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsPersistentChatAddin** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.PersistentChat.Cmdlets.AddinObject.

## Vedere anche

#### Ulteriori risorse

[Get-CsPersistentChatAddin](get-cspersistentchataddin.md)  
[New-CsPersistentChatAddin](new-cspersistentchataddin.md)  
[Remove-CsPersistentChatAddin](remove-cspersistentchataddin.md)

