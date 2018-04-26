---
title: Get-CsPersistentChatAddin
TOCTitle: Get-CsPersistentChatAddin
ms:assetid: 0d6b3283-c73d-4b83-b0f8-8f03aa4bba14
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204670(v=OCS.15)
ms:contentKeyID: 49299685
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPersistentChatAddin

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni su tutti i componenti aggiuntivi di Chat persistente configurati per l'utilizzo nell'organizzazione. Un componente aggiuntivo di Chat persistente è una pagina Web personalizzata che può essere incorporata in un client di Chat persistente. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsPersistentChatAddin [-PersistentChatPoolFqdn <String>] <COMMON PARAMETERS>

    Get-CsPersistentChatAddin -Identity <String> <COMMON PARAMETERS>

    COMMON PARAMETERS:

## Esempi

## Esempio 1

Nell'esempio 1 vengono restituite informazioni su tutti i componenti aggiuntivi di Chat persistente configurati per l'utilizzo nell'organizzazione.

    Get-CsPersistentChatAddin

## Esempio 2

Nell'esempio 2 vengono restituite informazioni su un componente aggiuntivo di Chat persistente specifico, ovvero il componente aggiuntivo con identità (Identity) atl-cs-001.litwareinc.com\\ITPersistentChatAddin.

    Get-CsPersistentChatAddin -Identity "atl-cs-001.litwareinc.com\ITPersistentChatAddin"

## Esempio 3

Nell'esempio 3 vengono restituite informazioni su tutti i componenti aggiuntivi di Chat persistente configurati per l'utilizzo nel pool atl-cs-001.litwareinc.com.

    Get-CsPersistentChatAddin -PersistentChatPoolFqdn "atl-cs-001.litwareinc.com"

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

I componenti aggiuntivi vengono utilizzati come estensioni di una chat room di Chat persistente. Si tratta di applicazioni esterne, ovvero elementi non incorporati in Chat persistente, associate a una chat room specifica. Ad esempio, una chat room del supporto tecnico può includere un URL che si collega a una pagina Web o a un'applicazione Silverlight che mostra lo stato delle richieste di assistenza della giornata. I cmdlet dell'interfaccia della riga di comando Windows PowerShell per Lync Server non consentono di creare questi componenti aggiuntivi. Vengono utilizzati invece i cmdlet **CsPersistentChatAddin** per associare o dissociare un componente aggiuntivo da una chat room.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPersistentChatAddin"}

**Pannello di controllo di Lync Server:** per visualizzare informazioni sui componenti aggiuntivi di Chat persistente nel Pannello di controllo di Lync Server, fare clic su **Chat persistente** e quindi su **Componente aggiuntivo**.

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
<td><p>Identificatore univoco del componente aggiuntivo di Chat persistente da restituire. L'identità (Identity) è costituita dal nome di dominio completo del pool di Chat persistente in cui si trova il componente aggiuntivo, da un carattere &quot;\&quot; e dal nome del componente aggiuntivo, ad esempio:</p>
<p>-Identity &quot;atl-gc-001.litwareincom\ITPersistentChatAddin&quot;</p>
<p>Se questo parametro non viene specificato, il cmdlet <strong>Get-CsPersistentChatAddin</strong> restituirà informazioni su tutti i componenti aggiuntivi di Chat persistente.</p></td>
</tr>
<tr class="even">
<td><p><em>PersistentChatPoolFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del pool di Chat persistente. Se questo parametro viene specificato, verranno restituiti solo i componenti aggiuntivi di Chat persistente trovati nel pool specificato. Se invece questo parametro non viene specificato, il cmdlet <strong>Get-CsPersistentChatAddin</strong> restituirà i componenti aggiuntivi di tutti i pool di Chat persistente. Ad esempio:</p>
<p>–PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsPersistentChatAddin** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsPersistentChatAddin** restituisce istanze dell'oggetto Microsoft.Rtc.Management.PersistentChat.Cmdlets.AddinObject.

## Vedere anche

#### Ulteriori risorse

[New-CsPersistentChatAddin](new-cspersistentchataddin.md)  
[Remove-CsPersistentChatAddin](remove-cspersistentchataddin.md)  
[Set-CsPersistentChatAddin](set-cspersistentchataddin.md)

