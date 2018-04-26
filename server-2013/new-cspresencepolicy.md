---
title: New-CsPresencePolicy
TOCTitle: New-CsPresencePolicy
ms:assetid: a0b54f25-db48-4797-8f0e-0e826830217c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412747(v=OCS.15)
ms:contentKeyID: 49301516
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPresencePolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo criterio di presenza nell'ambito del sito o nell'ambito per utente. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsPresencePolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-MaxCategorySubscription <UInt16>] [-MaxPromptedSubscriber <UInt16>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 consente di creare un nuovo criterio di presenza per utente con Identity RedmondPresencePolicy. In questo esempio il valore della proprietà MaxPromptedSubscriber è impostato su 400 e il valore della proprietà MaxCategorySubscription su 500.

    New-CsPresencePolicy -Identity "RedmondPresencePolicy" -MaxPromptedSubscriber 400 -MaxCategorySubscription 500

## ESEMPIO 2

Nell'esempio 2, inizialmente, viene creato un nuovo criterio di presenza per utente in memoria e, solo in un secondo momento, questo viene convertito in un criterio di presenza effettivo. A tale scopo, il primo comando dell'esempio crea un criterio di presenza con l'identità RedmondPresencePolicy e archivia il criterio in una variabile denominata $x. Il parametro InMemory garantisce che il criterio venga creato unicamente in memoria e che non venga aggiunto immediatamente a Lync Server.

I comandi 2 e 3 vengono utilizzati successivamente per configurare le proprietà MaxPromptedSubscriber e MaxCategorySubscription del criterio virtuale. Dopo che sono stati impostati i valori del criterio, nella riga 4 viene utilizzato il cmdlet **Set-CsPresencePolicy** con il parametro Instance per creare un criterio di presenza effettivo in base alle informazioni archiviate nella variabile $x. Il passaggio successivo è fondamentale: se non si chiama il cmdlet **Set-CsPresencePolicy**, il criterio sarà presente solo nella memoria e verrà eliminato non appena si chiude la sessione di Windows PowerShell o si elimina la variabile $x.

    $x = New-CsPresencePolicy -Identity "RedmondPresencePolicy" -InMemory
    $x.MaxPromptedSubscriber = 400
    $x.MaxCategorySubscription = 500
    Set-CsPresencePolicy -Instance $x

## Descrizione dettagliata

Le informazioni sulla presenza (che, tra l'altro, indicano se un contatto è disponibile a partecipare a una conversazione di messaggistica istantanea) sono di estrema importanza. Allo stesso tempo, tuttavia, le informazioni sulla presenza comportano un costo: maggiore è il numero delle sottoscrizioni di presenza, maggiore sarà la larghezza di banda da dedicare all'aggiornamento delle informazioni sulla presenza. Se la larghezza di banda rappresenta un problema, è possibile limitare il numero di sottoscrizioni di presenza disponibili per ciascun utente.

I cmdlet **CsPresencePolicy** consentono di gestire due aspetti importanti delle sottoscrizioni relative alla presenza: richieste di sottoscrizione e sottoscrizioni alle categorie. Quando si viene aggiunti all'elenco contatti di Lync di un'altra persona, il comportamento predefinito prevede la ricezione di una notifica popup in cui si viene informati di essere stati aggiunti a tale elenco. Finché non viene chiusa la finestra popup visualizzata, ogni notifica viene considerata una richiesta di sottoscrizione. La proprietà MaxPromptedSubscriber del criterio di presenza consente di specificare il numero massimo di finestre di dialogo di notifica non risolte per un utente. Se un utente raggiunge il numero massimo consentito, l'utente non riceverà nuove notifiche di contatto, almeno fino alla risoluzione di alcune delle finestre di dialogo.

Le sottoscrizioni alle categorie rappresentano la richiesta di una categoria di informazioni specifica. Ad esempio, un'applicazione che richiede i dati del calendario. La proprietà MaxCategorySubscription consente agli amministratori di definire un limite per il numero di sottoscrizioni alle categorie disponibili per un utente.

Prima di Lync Server, le richieste di sottoscrizione e le sottoscrizioni alle categorie venivano gestite a livello globale. Grazie ai cmdlet **CsPresencePolicy**, è possibile gestire le sottoscrizioni relative alla presenza nell'ambito globale, del sito o del singolo utente. In questo modo è possibile controllare l'utilizzo della larghezza di banda e, contemporaneamente, garantire l'accesso degli utenti alle informazioni sulla presenza necessarie per le loro attività.

Il cmdlet **New-CsPresencePolicy** consente di creare criteri di presenza personalizzati nell'ambito del sito o nell'ambito per utente. I criteri creati nell'ambito del sito vengono applicati automaticamente al sito in questione. I criteri dell'ambito per utente invece devono essere assegnati ai diversi utenti eseguendo il cmdlet **Grant-CsPresencePolicy**. Si noti che non è possibile creare un nuovo criterio di presenza nell'ambito globale, né un secondo criterio di presenza a un sito. Ad esempio, il sito Redmond può ospitare solo un criterio di presenza.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsPresencePolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPresencePolicy"}

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
<td><p>Identificatore univoco per il nuovo criterio di presenza. Per creare un nuovo criterio per utente, utilizzare la sintassi: -Identity &quot;RedmondPresencePolicy&quot;. Per creare un nuovo criterio nell'ambito del sito, utilizzare la sintassi: -Identity &quot;site:Redmond&quot;.</p>
<p>Si noti che non è possibile creare un nuovo criterio di presenza nell'ambito globale. Inoltre, il comando non funziona, se il sito in questione ospita già un criterio di presenza o se si tenta di utilizzare l'identità di un criterio per utente già esistente.</p></td>
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
<td><p>Consente agli amministratori di fornire un testo aggiuntivo da associare a un criterio di presenza. Il parametro Description potrebbe ad esempio includere informazioni sugli utenti a cui assegnare il criterio.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
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
<td><p>Il numero massimo di sottoscrittori con richiesta che un utente può avere in un dato momento. Per impostazione predefinita, ogni volta che un utente viene aggiunto all'elenco contatti di un altro utente, ne viene informato tramite notifica e può scegliere se eseguire operazioni quali aggiungere l'altro utente al proprio elenco contatti o bloccare la visualizzazione della propria presenza. Fino a quando non si esegue un'azione e si chiude la richiesta della finestra di dialogo, ogni notifica vale come un sottoscrittore con richiesta.</p>
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

Nessuno. Il cmdlet **New-CsPresencePolicy** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **New-CsPresencePolicy** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Presence.PresencePolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsPresencePolicy](get-cspresencepolicy.md)  
[Grant-CsPresencePolicy](grant-cspresencepolicy.md)  
[Remove-CsPresencePolicy](remove-cspresencepolicy.md)  
[Set-CsPresencePolicy](set-cspresencepolicy.md)

