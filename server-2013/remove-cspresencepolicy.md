---
title: Remove-CsPresencePolicy
TOCTitle: Remove-CsPresencePolicy
ms:assetid: ecdbfef8-2b7c-4bd7-bf01-7fb230eefe9f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399070(v=OCS.15)
ms:contentKeyID: 49302365
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPresencePolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove il criterio di presenza specificato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsPresencePolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono eliminati i criteri di presenza per utente con il parametro Identity RedmondPresencePolicy.

    Remove-CsPresencePolicy -Identity "RedmondPresencePolicy"

## ESEMPIO 2

Il comando mostrato nell'esempio 2 consente di rimuovere tutti i criteri di presenza configurati nell'ambito per utente. Questi criteri hanno un valore Identity che inizia con il prefisso "tag:". Per eseguire questa attività, nel comando vengono innanzitutto utilizzati il cmdlet **Get-CsPresencePolicy** e il parametro Filter per restituire tutti i criteri di presenza per utente. Il valore di filtro "tag:\*" limita i dati restituiti ai criteri in cui il valore Identity inizia con il valore stringa "tag:". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsPresencePolicy**, che elimina ogni criterio della raccolta.

    Get-CsPresencePolicy -Filter "tag:*" | Remove-CsPresencePolicy

## ESEMPIO 3

Nell'esempio 3 vengono eliminati tutti i criteri di presenza che consentono più di 500 richieste di sottoscrizione. A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsPresencePolicy** senza alcun parametro per restituire una raccolta di tutti i criteri di presenza configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i criteri in cui la proprietà MaxPromptedSubscriber è maggiore di 500. La raccolta filtrata viene a sua volta inviata tramite pipe al cmdlet **Remove-CsPresencePolicy**, che elimina tutti i criteri di presenza che consentono più di 500 richieste di sottoscrizione.

    Get-CsPresencePolicy | Where-Object {$_.MaxPromptedSubscriber -gt 500} | Remove-CsPresencePolicy

## Descrizione dettagliata

Le informazioni sulla presenza (che, tra l'altro, indicano se un contatto è disponibile a partecipare a una conversazione di messaggistica istantanea) sono di estrema importanza. Allo stesso tempo, tuttavia, le informazioni sulla presenza comportano un costo: maggiore è il numero delle sottoscrizioni di presenza, maggiore sarà la larghezza di banda da dedicare all'aggiornamento delle informazioni sulla presenza. Se la larghezza di banda rappresenta un problema, è possibile limitare il numero di sottoscrizioni di presenza disponibili per ciascun utente.

I cmdlet **CsPresencePolicy** consentono di gestire due aspetti importanti delle sottoscrizioni di presenza: richieste di sottoscrizione e sottoscrizioni alle categorie. Quando si viene aggiunti all'elenco contatti di Lync di un'altra persona, il comportamento predefinito prevede la ricezione di una notifica popup in cui si viene informati di essere stati aggiunti al suddetto elenco. Fino alla chiusura della finestra popup visualizzata, ogni notifica viene considerata una richiesta di sottoscrizione. La proprietà MaxPromptedSubscriber del criterio di presenza consente di specificare il numero massimo di finestre di dialogo di notifica non risolte disponibili per un utente. Una volta raggiunto il numero massimo consentito, l'utente non riceverà nuove notifiche di contatto, almeno fino alla chiusura di alcune di queste finestre di dialogo.

Le sottoscrizioni alle categorie rappresentano la richiesta di una categoria di informazioni specifica. Ad esempio, un'applicazione che richiede i dati del calendario. La proprietà MaxCategorySubscription consente agli amministratori di definire un limite per il numero di sottoscrizioni alle categorie disponibili per un utente.

Prima del rilascio di Lync Server, le richieste di sottoscrizione e le sottoscrizioni alle categorie venivano gestite globalmente. Con i cmdlet **CsPresencePolicy**, ora è possibile gestire tali sottoscrizioni di presenza nell'ambito globale, nell'ambito del sito o nell'ambito per utente. In questo modo è possibile controllare l'utilizzo della larghezza di banda e, contemporaneamente, garantire l'accesso degli utenti alle informazioni sulla presenza necessarie per le proprie attività.

I criteri creati nell'ambito del sito o nell'ambito per utente possono essere rimossi in qualsiasi momento mediante il cmdlet **Remove-CsPresencePolicy**. Il cmdlet può anche essere eseguito sul criterio globale. In questo caso, tuttavia, il criterio globale non verrà effettivamente rimosso. (Lync Server non consente la rimozione dei criteri globali. Le due proprietà del criterio globale, MaxPromptedSubscriber e MaxCategorySubscription, verranno invece reimpostate sui rispettivi valori predefiniti.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Remove-CsPresencePolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPresencePolicy"}

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
<td><p>Identificatore univoco per il criterio di presenza da rimuovere. Per rimuovere un criterio configurato nell'ambito del sito, utilizzare una sintassi analoga alla seguente: -Identity &quot;site:Redmond&quot;. Per rimuovere un criterio configurato nell'ambito per utente, utilizzare una sintassi analoga alla seguente: -Identity &quot;RedmondPresencePolicy&quot;.</p>
<p>Il cmdlet <strong>Remove-CsPresencePolicy</strong> può anche essere eseguito sul criterio globale. A tale scopo, utilizzare la seguente sintassi: -Identity global. In questo caso, il criterio globale però non verrà rimosso. Le proprietà del criterio verranno invece reimpostate sui rispettivi valori predefiniti.</p></td>
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
<td><p>Se questo parametro è presente, determinerà l'eliminazione del criterio per utente da parte del cmdlet <strong>Remove-CsPresencePolicy</strong>, anche se il criterio in questione attualmente è assegnato ad almeno un utente. Se questo parametro non è presente, verrà richiesto di confermare la richiesta di eliminazione prima della rimozione di un criterio ancora in uso.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Presence.PresencePolicy. Il cmdlet **Remove-CsPresencePolicy** accetta l'input da pipeline dell'oggetto criterio di presenza.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsPresencePolicy** piuttosto elimina le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Presence.PresencePolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsPresencePolicy](get-cspresencepolicy.md)  
[Grant-CsPresencePolicy](grant-cspresencepolicy.md)  
[New-CsPresencePolicy](new-cspresencepolicy.md)  
[Set-CsPresencePolicy](set-cspresencepolicy.md)

