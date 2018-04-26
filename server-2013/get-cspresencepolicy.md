---
title: Get-CsPresencePolicy
TOCTitle: Get-CsPresencePolicy
ms:assetid: 65880bdb-4482-4cfb-83de-19b239784fe5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398463(v=OCS.15)
ms:contentKeyID: 49300805
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPresencePolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce le informazioni sui criteri di presenza configurati per l'utilizzo nell'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsPresencePolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPresencePolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 vengono restituite le informazioni su tutti i criteri di presenza configurati per l'utilizzo nell'organizzazione. A tale scopo, viene chiamato il cmdlet **Get-CsPresencePolicy** senza alcun parametro.

    Get-CsPresencePolicy

## ESEMPIO 2

Con l'esempio 2 viene restituito un singolo criterio di presenza per utente, quello con identità RedmondPresencePolicy.

    Get-CsPresencePolicy -Identity "RedmondPresencePolicy"

## ESEMPIO 3

Nell'esempio 3 vengono restituite informazioni su tutti i criteri di presenza configurati nell'ambito del sito. Per ottenere questo risultato, il comando utilizza il parametro Filter e il valore del filtro "site:\*", che limita i dati restituiti ai criteri di presenza la cui identità (Identity) inizia con il valore stringa "site:".

    Get-CsPresencePolicy -Filter "site:*"

## ESEMPIO 4

Nell'esempio 4 vengono restituite le informazioni su tutti i criteri di presenza che limitano il numero massimo di richieste di sottoscrizione a 100. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsPresencePolicy** senza alcun parametro per restituire una raccolta di tutti i criteri di presenza configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object** , che seleziona solo i criteri in cui la proprietà MaxPromptedSubscriber è impostata su un valore minore o uguale a 100.

    Get-CsPresencePolicy | Where-Object {$_.MaxPromptedSubscriber -le 100}

## Descrizione dettagliata

Le informazioni sulla presenza (che, tra l'altro, indicano se un contatto è disponibile a partecipare a una conversazione di messaggistica istantanea) sono di estrema importanza. Allo stesso tempo, tuttavia, le informazioni sulla presenza comportano un costo: maggiore è il numero delle sottoscrizioni di presenza, maggiore sarà la larghezza di banda da dedicare all'aggiornamento delle informazioni sulla presenza. Se la larghezza di banda rappresenta un problema, è possibile limitare il numero di sottoscrizioni di presenza disponibili per ciascun utente.

I cmdlet **CsPresencePolicy** consentono di gestire due aspetti importanti delle sottoscrizioni relative alla presenza: richieste di sottoscrizione e sottoscrizioni alle categorie. Quando si viene aggiunti all'elenco contatti di Lync di un'altra persona, il comportamento predefinito prevede la ricezione di una notifica popup in cui si viene informati di essere stati aggiunti a tale elenco. Finché non viene chiusa la finestra popup visualizzata, ogni notifica viene considerata una richiesta di sottoscrizione. La proprietà MaxPromptedSubscriber del criterio di presenza consente di specificare il numero massimo di finestre di dialogo di notifica non risolte per un utente. Se un utente raggiunge il numero massimo consentito, l'utente non riceverà nuove notifiche di contatto, almeno fino alla risoluzione di alcune delle finestre di dialogo.

Le sottoscrizioni alle categorie rappresentano la richiesta di una categoria di informazioni specifica. Ad esempio, un'applicazione che richiede i dati del calendario. La proprietà MaxCategorySubscription consente agli amministratori di definire un limite per il numero di sottoscrizioni alle categorie disponibili per un utente.

Prima del rilascio di Lync Server, le richieste di sottoscrizione e le sottoscrizioni alle categorie venivano gestite globalmente. Con i cmdlet **CsPresencePolicy**, ora è possibile gestire tali sottoscrizioni di presenza nell'ambito globale, nell'ambito del sito o nell'ambito per utente. In questo modo è possibile controllare l'utilizzo della larghezza di banda e, contemporaneamente, garantire l'accesso degli utenti alle informazioni sulla presenza necessarie per le proprie attività.

Il cmdlet **Get-CsPresencePolicy** consente di restituire informazioni su tutti i criteri di presenza configurati per l'uso nell'organizzazione.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Get-CsPresencePolicy** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPresencePolicy"}

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
<td><p>Consente di utilizzare i caratteri jolly per specificare il criterio o i criteri da restituire. Ad esempio, per ottenere tutti i criteri di presenza configurati nell'ambito del sito, utilizzare la seguente sintassi: -Filter &quot;site:*&quot;.</p>
<p>Non è possibile utilizzare i parametri Filter e Identity nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco del criterio di presenza da recuperare. Per restituire il criterio globale, utilizzare la sintassi seguente: -Identity global. Per restituire un criterio configurato in ambito sito, utilizzare una sintassi simile alla seguente: -Identity &quot;site:Redmond&quot;. Per restituire un criterio configurato in ambito servizio, utilizzare una sintassi simile alla seguente: -Identity &quot;RedmondPresencePolicy&quot;. Non è possibile utilizzare caratteri jolly quando si specifica l'identità.</p>
<p>Se non vengono specificati né il parametro Identity né il parametro Filter, il cmdlet <strong>Get-CsPresencePolicy</strong> restituisce tutti i criteri di presenza configurati per l'utilizzo nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati dei criteri di presenza dalla replica locale del archivio di gestione centrale anziché dal archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsPresencePolicy** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Get-CsPresencePolicy** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Presence.PresencePolicy.

## Vedere anche

#### Ulteriori risorse

[Grant-CsPresencePolicy](grant-cspresencepolicy.md)  
[New-CsPresencePolicy](new-cspresencepolicy.md)  
[Remove-CsPresencePolicy](remove-cspresencepolicy.md)  
[Set-CsPresencePolicy](set-cspresencepolicy.md)

