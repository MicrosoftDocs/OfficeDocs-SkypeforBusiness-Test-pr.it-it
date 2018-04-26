---
title: Get-CsPersistentChatPolicy
TOCTitle: Get-CsPersistentChatPolicy
ms:assetid: 0f33d177-dec6-44a3-a9ef-dd39029a4ddd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204673(v=OCS.15)
ms:contentKeyID: 49299696
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPersistentChatPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui criteri di Chat persistente configurati per l'utilizzo nell'organizzazione. I criteri di questo tipo determinano se gli utenti sono autorizzati o meno ad accedere alle chat room di Chat persistente. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsPersistentChatPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPersistentChatPolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce informazioni su tutti i criteri di Chat persistente configurati per l'utilizzo nell'organizzazione.

    Get-CsPersistentChatPolicy

## Esempio 2

Nell'esempio 2 vengono restituite solo le informazioni relative al criterio di Chat persistente per utente con identità (Identity) RedmondPersistentChatPolicy.

    Get-CsPersistentChatPolicy -Identity "RedmondPersistentChatPolicy"

## Esempio 3

Nell'esempio 3 vengono restituite informazioni relative a tutti i criteri di Chat persistente configurati nell'ambito del sito. Per ottenere questo risultato, viene incluso il parametro Filter con valore "site:\*".

    Get-CsPersistentChatPolicy -Filter "site:*"

## Esempio 4

Nell'esempio 4 vengono restituite solo le informazioni relative ai criteri di Chat persistente con Chat persistente abilitata. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsPersistentChatPolicy** senza parametri per restituire una raccolta di tutti i criteri di Chat persistente configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i criteri in cui la proprietà EnablePersistentChat è uguale a True ($True).

    Get-CsPersistentChatPolicy | Where-Object {$_.EnablePersistentChat -eq $True}

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Per impostazione predefinita, agli utenti non è concesso l'accesso al servizio Chat persistente. Questo accesso può essere concesso solo se l'utente è gestito da un criterio di Chat persistente che consente l'utilizzo del servizio. Quando si installa Lync 2013, tutti gli utenti sono gestiti da un criterio di Chat persistente globale in cui l'utilizzo di Chat persistente è disabilitato. Se si desidera concedere a tutti gli utenti l'accesso al servizio, è possibile impostare semplicemente la proprietà EnablePersistentChat di questo criterio globale su True. In alternativa, è possibile creare criteri aggiuntivi nell'ambito del sito o per utente e concedere così l'accesso a Chat persistente ad alcuni utenti negandolo invece ad altri.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPersistentChatPolicy"}

**Pannello di controllo di Lync Server:** per visualizzare informazioni sui criteri di Chat persistente nel Pannello di controllo di Lync Server, fare clic su **Chat persistente** e quindi su **Criteri di Chat persistente**.

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare i caratteri jolly per ricercare i criteri di Chat persistente. Per cercare ad esempio tutti i criteri configurati nell'ambito del sito, utilizzare la sintassi seguente:</p>
<p>-Filter &quot;site:*&quot;</p>
<p>Non è possibile utilizzare i parametri Filter e Identity nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identità univoca assegnata al criterio al momento della creazione. I criteri di Chat persistente possono essere assegnati nell'ambito globale, del sito o per utente. Per fare riferimento all'istanza globale, utilizzare la sintassi seguente:</p>
<p>-Identity global</p>
<p>Per ottenere un criterio nell'ambito del sito, utilizzare la sintassi seguente:</p>
<p>-Identity site:Redmond</p>
<p>Per fare riferimento a un criterio nell'ambito per utente, utilizzare la sintassi seguente:</p>
<p>-Identity RedmondPersistentChatPolicy</p>
<p>Non è possibile utilizzare i caratteri jolly, come l'asterisco (*), con il parametro Identity. Per cercare i criteri utilizzando i caratteri jolly, utilizzare il parametro Filter.</p>
<p>Se non si specifica né il parametro Identity né il parametro Filter, il cmdlet <strong>Get-CsPersistentChatPolicy</strong> restituisce informazioni su tutti i criteri di Chat persistente configurati per l'utilizzo nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati dei criteri di Chat persistente dalla replica locale dell'archivio di gestione centrale anziché direttamente dall'archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsPersistentChatPolicy** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Get-CsPersistentChatPolicy** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.PersistentChat.PersistentChatPolicy.

## Vedere anche

#### Ulteriori risorse

[Grant-CsPersistentChatPolicy](grant-cspersistentchatpolicy.md)  
[New-CsPersistentChatPolicy](new-cspersistentchatpolicy.md)  
[Remove-CsPersistentChatPolicy](remove-cspersistentchatpolicy.md)  
[Set-CsPersistentChatPolicy](set-cspersistentchatpolicy.md)

