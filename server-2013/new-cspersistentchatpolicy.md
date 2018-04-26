---
title: New-CsPersistentChatPolicy
TOCTitle: New-CsPersistentChatPolicy
ms:assetid: f7d42a24-598a-4ea3-8a0f-25575b5235ea
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205396(v=OCS.15)
ms:contentKeyID: 49302508
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPersistentChatPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo criterio di Chat persistente nell'ambito del sito o per utente. I criteri di questo tipo determinano se gli utenti sono autorizzati o meno ad accedere alle chat room di Chat persistente. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    New-CsPersistentChatPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Description <String>] [-EnablePersistentChat <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 crea nuovi criteri di Chat persistente con l'identità RedmondPersistentChatPolicy. In questo esempio, Chat persistente è abilitato utilizzando il parametro EnablePersistentChat e il valore del parametro $True.

    New-CsPersistentChatPolicy -Identity "RedmondPersistentChatPolicy" -EnablePersistentChat $True

## Esempio 2

L'esempio 2 è una variazione del comando riportato nell'esempio 1. L'unica differenza è che i nuovi criteri vengono applicati all'ambito di sito anziché all'ambito per utente. A tal fine l'identità viene impostata sul valore di stringa "site:" seguito dal nome del sito stesso, in questo caso, site:Redmond.

    New-CsPersistentChatPolicy -Identity "site:Redmond" -EnablePersistentChat $True

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Per impostazione predefinita, agli utenti non è concesso l'accesso al servizio Chat persistente. Questo accesso può essere concesso solo se l'utente è gestito da un criterio di Chat persistente che consente l'utilizzo del servizio. Quando si installa Lync 2013, tutti gli utenti sono gestiti da un criterio di Chat persistente globale in cui l'utilizzo di Chat persistente è disabilitato. Se si desidera concedere a tutti gli utenti l'accesso al servizio, è possibile impostare semplicemente la proprietà EnablePersistentChat di questo criterio globale su True. In alternativa, è possibile creare criteri aggiuntivi nell'ambito del sito o per utente e concedere così l'accesso a Chat persistente ad alcuni utenti negandolo invece ad altri.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPersistentChatPolicy"}

**Pannello di controllo di Lync Server:** Per creare nuovi criteri di Chat persistente utilizzando il Pannello di controllo di Lync Server, fare clic su **Chat persistente**, quindi su **Criteri di Chat persistente**, scegliere **Nuovo** e quindi fare clic su **Criteri sito** o **Criteri utente**.

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
<td><p>Identificatore univoco da assegnare ai criteri. È possibile creare criteri di Chat persistente con ambito di sito o con ambito per utente. Per creare nuovi criteri di sito, utilizzare il prefisso &quot;site:&quot; e il nome del sito come identità. Ad esempio, utilizzare la sintassi seguente per creare nuovi criteri per il sito Redmond:</p>
<p>-Identity site:Redmond</p>
<p>Per creare nuovi criteri per utente, utilizzare una sintassi analoga alla seguente:</p>
<p>-Identity SalesPersistentChatPolicy</p>
<p>Notare che non è possibile creare nuovi criteri globali. Se si desidera apportare modifiche ai criteri globali, utilizzare invece il cmdlet <strong>Set-CsPersistentChatPolicy</strong>. Analogamente, non è possibile creare nuovi criteri di sito o per utente se esistono già criteri con tale identità. Se è necessario apportare modifiche a criteri esistenti, utilizzare il cmdlet <strong>Set-CsPersistentChatPolicy</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire testo di spiegazione che accompagna i criteri. La descrizione può, ad esempio, includere informazioni sugli utenti a cui i criteri devono essere assegnati.</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePersistentChat</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando è impostato su True, agli utenti interessati dai criteri è consentito utilizzare Chat persistente. Quando impostato su False (valore predefinito) agli utenti interessati dai criteri non è consentito utilizzare Chat persistente.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
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

Nessuno. Il cmdlet **New-CsPersistentChatPolicy** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **New-CsPersistentChatPolicy** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.PersistentChat.PersistentChatPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsPersistentChatPolicy](get-cspersistentchatpolicy.md)  
[Grant-CsPersistentChatPolicy](grant-cspersistentchatpolicy.md)  
[Remove-CsPersistentChatPolicy](remove-cspersistentchatpolicy.md)  
[Set-CsPersistentChatPolicy](set-cspersistentchatpolicy.md)

