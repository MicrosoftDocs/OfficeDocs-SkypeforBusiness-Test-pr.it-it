---
title: New-CsPersistentChatAddin
TOCTitle: New-CsPersistentChatAddin
ms:assetid: 0566f4c2-0903-4dd1-87bc-784f0bdb4391
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204641(v=OCS.15)
ms:contentKeyID: 49299548
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPersistentChatAddin

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di configurare un nuovo componente aggiuntivo di Chat persistente. Un componente aggiuntivo di Chat persistente è una pagina Web personalizzata che può essere incorporata in un client di Chat persistente. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    New-CsPersistentChatAddin -Name <String> -Url <String> [-PersistentChatPoolFqdn <String>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 crea un nuovo componente aggiuntivo di Chat persistente (con nome ITPersistentChatAddin) per il pool atl-cs-001.litwareinc.com. Il parametro URL e il valore del parametro http://atl-cs-001.litwareinc.com/itchat specificano la posizione della pagina Web del componente aggiuntivo.

    New-CsPersistentChatAddin -Name "ITPersistentChatAddin" -PersistentChatPoolFqdn "atl-cs-001.litwareinc.com" -Url "http://atl-cs-001.litwareinc.com/itchat"

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

I componenti aggiuntivi vengono utilizzati come estensioni di una chat room di Chat persistente. Si tratta di applicazioni esterne, ovvero elementi non incorporati in Chat persistente, associate a una chat room specifica. Ad esempio, una chat room del supporto tecnico può includere un URL che si collega a una pagina Web o a un'applicazione Silverlight che visualizza lo stato delle richieste di assistenza della giornata. Lync Server Management Shell non consente di creare questi componenti aggiuntivi. Vengono utilizzati invece i cmdlet **CsPersistentChatAddin** per associare o dissociare un componente aggiuntivo da una chat room.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli del controllo di accesso basato sui ruoli creati personalmente), al prompt di Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPersistentChatAddin"}

**Pannello di controllo di Lync Server:** per creare un nuovo componente aggiuntivo di Chat persistente utilizzando il Pannello di controllo di Lync Server, fare clic su **Chat persistente**, **Componente aggiuntivo** e quindi su **Nuovo**.

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
<td><p>Nome descrittivo da assegnare al componente aggiuntivo di Chat persistente. I nomi devono essere univoci per ogni pool di server Chat persistente.</p></td>
</tr>
<tr class="even">
<td><p><em>Url</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>URL della pagina Web da visualizzare con il componente aggiuntivo di Chat persistente.</p></td>
</tr>
<tr class="odd">
<td><p><em>PersistentChatPoolFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del pool di server Chat persistente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsPersistentChatAddin** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsPersistentChatAddin** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.PersistentChat.Cmdlets.AddinObject.

## Vedere anche

#### Ulteriori risorse

[Get-CsPersistentChatAddin](get-cspersistentchataddin.md)  
[Remove-CsPersistentChatAddin](remove-cspersistentchataddin.md)  
[Set-CsPersistentChatAddin](set-cspersistentchataddin.md)

