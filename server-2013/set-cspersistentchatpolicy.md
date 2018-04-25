---
title: Set-CsPersistentChatPolicy
TOCTitle: Set-CsPersistentChatPolicy
ms:assetid: b724bc13-d4fe-4529-9a48-e4cec8b7dce2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205192(v=OCS.15)
ms:contentKeyID: 49301755
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPersistentChatPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un criterio di Chat persistente esistente. I criteri di questo tipo determinano se gli utenti sono autorizzati o meno ad accedere alle chat room di Chat persistente. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsPersistentChatPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPersistentChatPolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-EnablePersistentChat <$true | $false>] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Nell'esempio 1 Chat persistente viene abilitata per il criterio di Chat persistente globale.

    Set-CsPersistentChatPolicy -Identity "global" -EnablePersistentChat $True

## Esempio 2

Nell'esempio 2 Chat persistente viene abilitata per tutti i criteri di Chat persistente configurati nell'organizzazione. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsPersistentChatPolicy** senza alcun parametro per restituire una raccolta di tutti i criteri di Chat persistente. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsPersistentChatPolicy**, che imposta su True ($True) il parametro EnablePersistentChat per ogni criterio della raccolta.

    Get-CsPersistentChatPolicy | Set-CsPersistentChatPolicy -EnablePersistentChat $True

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Per impostazione predefinita, agli utenti non è concesso l'accesso al servizio Chat persistente. Questo accesso può essere concesso solo se l'utente è gestito da un criterio di Chat persistente che consente l'utilizzo del servizio. Quando si installa Lync 2013, tutti gli utenti sono gestiti da un criterio di Chat persistente globale in cui l'utilizzo di Chat persistente è disabilitato. Se si desidera concedere a tutti gli utenti l'accesso al servizio, è possibile impostare semplicemente la proprietà EnablePersistentChat di questo criterio globale su True. In alternativa, è possibile creare criteri aggiuntivi nell'ambito del sito o per utente e concedere così l'accesso a Chat persistente ad alcuni utenti negandolo invece ad altri.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPersistentChatPolicy"}

**Pannello di controllo di Lync Server:** per modificare un criterio di Chat persistente esistente utilizzando il Pannello di controllo di Lync Server, fare clic su **Chat persistente**, su **Criteri di Chat persistente** e quindi fare doppio clic sul criterio da modificare.

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire testo di spiegazione che accompagna i criteri. La descrizione può, ad esempio, includere informazioni sugli utenti a cui i criteri devono essere assegnati.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePersistentChat</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, gli utenti interessati dal criterio saranno autorizzati a utilizzare Chat persistente. Se impostato su False (valore predefinito), gli utenti interessati dal criterio non saranno autorizzati a utilizzare Chat persistente.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco del criterio di Chat persistente da modificare. Per modificare il criterio globale, utilizzare la sintassi seguente:</p>
<p>-Identity global</p>
<p>Per modificare un criterio nell'ambito del sito, utilizzare la sintassi seguente:</p>
<p>-Identity site:Redmond</p>
<p>Per modificare un criterio per utente, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity RedmondPolicy</p>
<p>Se non si include il parametro Identity, il cmdlet <strong>Set-CsPersistentChatPolicy</strong> modificherà automaticamente il criterio globale.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
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

Il cmdlet **Set-CsPersistentChatPolicy** accetta istanze tramite pipeline dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.PersistentChat.PersistentChatPolicy.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsPersistentChatPolicy** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.PersistentChat.PersistentChatPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsPersistentChatPolicy](get-cspersistentchatpolicy.md)  
[Grant-CsPersistentChatPolicy](grant-cspersistentchatpolicy.md)  
[New-CsPersistentChatPolicy](new-cspersistentchatpolicy.md)  
[Remove-CsPersistentChatPolicy](remove-cspersistentchatpolicy.md)

