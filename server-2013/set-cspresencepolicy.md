---
title: Set-CsPresencePolicy
TOCTitle: Set-CsPresencePolicy
ms:assetid: 2d1f157b-d35d-402b-904d-281c013d2c30
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425782(v=OCS.15)
ms:contentKeyID: 49300050
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPresencePolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un criterio di presenza esistente. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsPresencePolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPresencePolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-MaxCategorySubscription <UInt16>] [-MaxPromptedSubscriber <UInt16>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di modificare il criterio di presenza RedmondPresencePolicy per un singolo utente. In questo esempio, il valore della proprietà MaxPromptedSubscriber è impostato su 300.

    Set-CsPresencePolicy -Identity "RedmondPresencePolicy" -MaxPromptedSubscriber 300

## ESEMPIO 2

Il comando riportato nell'esempio 2 è una variante del comando utilizzato nell'esempio 1. In questo caso, la proprietà MaxPromptedSubscriber viene però impostata su 300 per tutti i criteri di presenza configurati per l'utilizzo nell'organizzazione. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsPresencePolicy** senza alcun parametro. Viene così restituita una raccolta di tutti i criteri di presenza configurati per l'utilizzo nell'organizzazione. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsPresencePolicy**, che imposta su 300 il valore della proprietà MaxPromptedSubscriber di ogni criterio della raccolta.

    Get-CsPresencePolicy | Set-CsPresencePolicy -MaxPromptedSubscriber 300

## ESEMPIO 3

Nell'esempio 3 viene mostrato come configurare i criteri di presenza nell'organizzazione in modo che nessun criterio consenta più di 300 richieste di sottoscrizione. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsPresencePolicy** senza alcun parametro per restituire una raccolta di tutti i criteri di presenza nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i criteri in cui il valore della proprietà MaxPromptedSubscriber è maggiore di 300. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsPresencePolicy** che, per ogni criterio della raccolta, imposta il numero massimo di richieste di sottoscrizione su 300. Di conseguenza, nessun criterio consentirà più di 300 richieste di sottoscrizione, anche se alcuni criteri potrebbero consentire un numero di richieste inferiore a 300.

    Get-CsPresencePolicy | Where-Object {$_.MaxPromptedSubscriber -gt 300} | Set-CsPresencePolicy -MaxPromptedSubscriber 300

## Descrizione dettagliata

Le informazioni sulla presenza (che, tra l'altro, indicano se un contatto è disponibile a partecipare a una conversazione di messaggistica istantanea) sono di estrema importanza. Allo stesso tempo, tuttavia, le informazioni sulla presenza comportano un costo: maggiore è il numero delle sottoscrizioni di presenza, maggiore sarà la larghezza di banda da dedicare all'aggiornamento delle informazioni sulla presenza. Se la larghezza di banda rappresenta un problema, è possibile limitare il numero di sottoscrizioni di presenza disponibili per ciascun utente.

I cmdlet **CsPresencePolicy** consentono di gestire due aspetti importanti delle sottoscrizioni relative alla presenza: richieste di sottoscrizione e sottoscrizioni alle categorie. Quando si viene aggiunti all'elenco contatti di Lync di un'altra persona, il comportamento predefinito prevede la ricezione di una notifica popup in cui si viene informati di essere stati aggiunti a tale elenco. Finché non viene chiusa la finestra popup visualizzata, ogni notifica viene considerata una richiesta di sottoscrizione. La proprietà MaxPromptedSubscriber del criterio di presenza consente di specificare il numero massimo di finestre di dialogo di notifica non risolte per un utente. Se un utente raggiunge il numero massimo consentito, l'utente non riceverà nuove notifiche di contatto, almeno fino alla risoluzione di alcune delle finestre di dialogo.

Le sottoscrizioni alle categorie rappresentano la richiesta di una categoria di informazioni specifica. Ad esempio, un'applicazione che richiede i dati del calendario. La proprietà MaxCategorySubscription consente agli amministratori di definire un limite per il numero di sottoscrizioni alle categorie disponibili per un utente.

Prima del rilascio di Lync Server, le richieste di sottoscrizione e le sottoscrizioni alle categorie venivano gestite globalmente. Con i cmdlet **CsPresencePolicy**, ora è possibile gestire tali sottoscrizioni di presenza nell'ambito globale, nell'ambito del sito o nell'ambito per utente. In questo modo è possibile controllare l'utilizzo della larghezza di banda e, contemporaneamente, garantire l'accesso degli utenti alle informazioni sulla presenza necessarie per le proprie attività.

Il cmdlet **Set-CsPresencePolicy** consente di modificare qualunque criterio di presenza configurato per l'utilizzo nella propria organizzazione. Modificare un criterio di presenza significa impostare un diverso valore per la proprietà MaxPromptedSubscriber e/o la proprietà MaxCategorySubscription.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsPresencePolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPresencePolicy"}

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
<td><p>Consente agli amministratori di fornire un testo aggiuntivo da associare a un criterio di presenza. Il parametro Description potrebbe ad esempio includere informazioni sugli utenti a cui assegnare il criterio.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco del criterio di presenza da modificare. Per modificare il criterio globale, utilizzare la seguente sintassi: -Identity global. Per modificare un criterio nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity &quot;site:Redmond&quot;. Per modificare un criterio a livello di singolo utente, utilizzare una sintassi simile alla seguente: -Identity &quot;RedmondPresencePolicy&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto criterio di presenza</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxCategorySubscription</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero massimo di sottoscrizioni alla categoria consentito in un dato momento. Una sottoscrizione alla categoria rappresenta una richiesta per una categoria specifica di informazioni, ad esempio, un'applicazione che richiede i dati del calendario.</p>
<p>È possibile impostare MaxCategorySubscription su qualsiasi numero intero compreso fra 0 e 3000; il valore predefinito è 1000.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxPromptedSubscriber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero massimo di richieste di sottoscrizione che un utente può avere in qualunque momento. Per impostazione predefinita, ogni volta che un utente viene aggiunto all'elenco contatti di un altro utente, viene visualizzata la relativa finestra di dialogo di notifica che consente di eseguire operazioni come aggiungere la persona al proprio elenco contatti o bloccare tale persona e non consentirle di visualizzare la propria presenza. Fino a quando non si sceglie come procedere e non si chiude la finestra di dialogo, ogni notifica conta come una richiesta di sottoscrizione.</p>
<p>È possibile impostare MaxPromptedSubscriber su qualsiasi numero intero compreso tra 0 e 600 inclusi. Il valore predefinito è 200. Se si imposta il valore su 0, gli utenti non riceveranno alcuna notifica quando vengono aggiunti all'elenco contatti di un altro utente.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Presence.PresencePolicy. Il cmdlet **Set-CsPresencePolicy** accetta l'input da pipeline dell'oggetto criterio di presenza.

## Tipi restituiti

Il cmdlet **Set-CsPresencePolicy** non restituisce oggetti o valori. Il cmdlet invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Presence.PresencePolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsPresencePolicy](get-cspresencepolicy.md)  
[Grant-CsPresencePolicy](grant-cspresencepolicy.md)  
[New-CsPresencePolicy](new-cspresencepolicy.md)  
[Remove-CsPresencePolicy](remove-cspresencepolicy.md)

