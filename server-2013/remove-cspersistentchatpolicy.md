---
title: Remove-CsPersistentChatPolicy
TOCTitle: Remove-CsPersistentChatPolicy
ms:assetid: d6bfe22b-084b-4d7f-8e4a-58f738493b31
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205301(v=OCS.15)
ms:contentKeyID: 49302130
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPersistentChatPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un criterio di Chat persistente esistente. I criteri di questo tipo determinano se gli utenti sono autorizzati o meno ad accedere alle chat room di Chat persistente. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsPersistentChatPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 rimuove i criteri di Chat persistente con l'identità RedmondPersistentChatPolicy.

    Remove-CsPersistentChatPolicy -Identity "RedmondPersistentChatPolicy"

## Esempio 2

Nell'esempio 2 vengono eliminati tutti i criteri di Chat persistente applicati all'ambito di sito. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsPersistentChatPolicy** e il parametro Filter per restituire tutti i criteri di Chat persistente configurati con ambito di sito. Per tale scopo viene utilizzato il valore di filtro "site:\*". Questi criteri vengono quindi inviati tramite pipe al cmdlet **Remove-CsPersistentChatPolicy**, che li elimina.

    Get-CsPersistentChatPolicy -Filter "site:*" | Remove-CsPersistentChatPolicy

## Esempio 3

Nell'esempio 3, vengono eliminati tutti i criteri di Chat persistente in cui Chat persistente è abilitato. Per eseguire questa attività, il comando innanzitutto chiama il cmdlet **Get-CsPersistentChatPolicy** senza parametri per restituire una raccolta di tutti i criteri di Chat persistente configurati per l'uso nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object** che sceglie solo i criteri in cui la proprietà EnablePersistentChat è uguale a True ($True). Tale raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsPersistentChatPolicy** che elimina ogni criterio nella raccolta.

    Get-CsPersistentChatPolicy | Where-Object {$_.EnablePersistentChat -eq $True} | Remove-CsPersistentChatPolicy

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Per impostazione predefinita, agli utenti non è concesso l'accesso al servizio Chat persistente. Questo accesso può essere concesso solo se l'utente è gestito da un criterio di Chat persistente che consente l'utilizzo del servizio. Quando si installa Lync 2013, tutti gli utenti sono gestiti da un criterio di Chat persistente globale in cui l'utilizzo di Chat persistente è disabilitato. Se si desidera concedere a tutti gli utenti l'accesso al servizio, è possibile impostare semplicemente la proprietà EnablePersistentChat di questo criterio globale su True. In alternativa, è possibile creare criteri aggiuntivi nell'ambito del sito o per utente e concedere così l'accesso a Chat persistente ad alcuni utenti negandolo invece ad altri.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPersistentChatPolicy"}

**Pannello di controllo di Lync Server:** Per rimuovere criteri di Chat persistente utilizzando il Pannello di controllo di Lync Server, fare clic su **Chat persistente** e quindi su **Criteri di Chat persistente**. Selezionare i criteri da rimuovere, fare clic su **Modifica** e quindi fare clic su **Elimina**.

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identità univoca del criterio di Chat persistente da eliminare. Per rimuovere un criterio con ambito di sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity site:Redmond</p>
<p>Per eliminare criteri per utente, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity RedmondPolicy</p>
<p>Il cmdlet <strong>Remove-CsPersistentChatPolicy</strong> può anche essere eseguito sui criteri di Chat persistente. In tale caso, tuttavia, i criteri globali non verranno effettivamente eliminati. Viceversa, tutte le proprietà nei criteri globali verranno reimpostate sui loro valori predefiniti.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se questo parametro è presente, determinerà l'eliminazione del criterio per utente da parte del cmdlet <strong>Remove-CsPersistentChatPolicy</strong>, anche se il criterio in questione attualmente è assegnato ad almeno un utente. Se questo parametro non è presente, verrà richiesto di confermare la richiesta di eliminazione prima della rimozione di un criterio ancora in uso.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Remove-CsPersistentChatPolicy** accetta istanze tramite pipeline dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.PersistentChat.PersistentChatPolicy.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsPersistentChatPolicy** elimina piuttosto le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.PersistentChat.PersistentChatPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsPersistentChatPolicy](get-cspersistentchatpolicy.md)  
[Grant-CsPersistentChatPolicy](grant-cspersistentchatpolicy.md)  
[New-CsPersistentChatPolicy](new-cspersistentchatpolicy.md)  
[Set-CsPersistentChatPolicy](set-cspersistentchatpolicy.md)

