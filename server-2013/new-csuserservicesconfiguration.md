---
title: New-CsUserServicesConfiguration
TOCTitle: New-CsUserServicesConfiguration
ms:assetid: bdcb11b5-b8bf-4d63-a8a5-11f2b43686dd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412926(v=OCS.15)
ms:contentKeyID: 49301820
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsUserServicesConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni di configurazione di Servizi utente. Il servizio Servizi utente viene utilizzato per conservare le informazioni sulla presenza e gestire le conferenze. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsUserServicesConfiguration -Identity <XdsIdentity> [-AnonymousUserGracePeriod <TimeSpan>] [-Confirm [<SwitchParameter>]] [-DeactivationGracePeriod <TimeSpan>] [-DefaultSubscriptionExpiration <Int64>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-MaintenanceTimeOfDay <DateTime>] [-MaxContacts <UInt16>] [-MaxPersonalNotes <UInt32>] [-MaxScheduledMeetingsPerOrganizer <UInt32>] [-MaxSubscriptionExpiration <Int64>] [-MaxSubscriptions <UInt16>] [-MinSubscriptionExpiration <Int64>] [-PresenceProviders <PSListModifier>] [-SubscribeToCollapsedDG <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 crea una nuova raccolta di impostazioni di configurazione di Servizi utente per il sito Redmond (-Identity site:Redmond). Oltre a specificare l'identità, il comando consente anche di impostare il numero massimo di contatti (-MaxContacts 500) e l'ora del giorno in cui si esegue la manutenzione (-MaintenanceTimeOfDay "11:00 PM"). Il comando avrà esito negativo se le impostazioni di Servizi utente sono già state configurate per il sito Redmond. Questo si verifica perché esiste il limite di una sola raccolta di impostazioni per sito.

    New-CsUserServicesConfiguration -Identity site:Redmond -MaxContacts 500 -MaintenanceTimeOfDay "11:00 PM"

## ESEMPIO 2

Nell'esempio 2 viene inoltre creata una nuova raccolta di impostazioni di configurazione di Servizi utente per il sito Redmond. In questo esempio tuttavia la raccolta viene inizialmente creata in memoria e solo successivamente viene applicata al sito Redmond. A tale scopo, nel primo comando riportato nell'esempio vengono utilizzati il cmdlet **New-CsUserServicesConfiguration** e il parametro InMemory per creare una nuova raccolta (con valore Identity site:Redmond) presente solo in memoria. Poiché questa raccolta è presente solo in memoria, l'oggetto Servizi utente deve essere archiviato in una variabile. In questo caso, la variabile è denominata $x.

Al termine della creazione della raccolta virtuale, vengono utilizzati i comandi 2 e 3 per modificare i valori delle proprietà MaxContacts e MaintenanceTimeOfDay. Nell'ultimo comando dell'esempio viene utilizzato quindi il cmdlet **Set-CsUserServicesConfiguration** per trasformare le impostazioni virtuali in una raccolta effettiva di impostazioni di configurazione di Servizi utente applicate al sito Redmond. Questa fase conclusiva è fondamentale: se non si chiama il cmdlet **Set-CsUserServicesConfiguration**, al sito Redmond non verrà applicata alcuna impostazione e le impostazioni virtuali scompariranno non appena si terminerà la sessione di Windows PowerShell o si eliminerà la variabile $x.

    $x = New-CsUserServicesConfiguration -Identity site:Redmond -InMemory
    $x.MaxContacts = 500 
    $x.MaintenanceTimeOfDay = "11:00 PM"
    Set-CsUserServicesConfiguration -Instance $x

## Descrizione dettagliata

Lync Server utilizza il servizio Servizi utente per mantenere le informazioni sulla presenza degli utenti e per gestire le riunioni e le conferenze. A loro volta, i cmdlet **CsUserServicesConfiguration** vengono utilizzati per amministrare le impostazioni di configurazione di Servizi utente nell'ambito globale, del sito e del servizio. Si noti che l'unico servizio in grado di ospitare le impostazioni di configurazione di Servizi utente è il servizio stesso. Queste impostazioni consentono di specificare elementi quali il numero di contatti che un utente può avere, il numero di riunioni pianificate che un utente può avere in un determinato momento e l'intervallo di tempo massimo in cui una determinata riunione può rimanere attiva.

Il cmdlet **New-CsUserServicesConfiguration** consente agli amministratori di creare una nuova raccolta di impostazioni di configurazione di Servizi utente nell'ambito del sito o del servizio. (Non è possibile creare nuove raccolte nell'ambito globale). Ogni sito o servizio specifico può disporre al massimo di un'unica raccolta di impostazioni di configurazione di Servizi utente. Il comando ad esempio avrà esito negativo se si tenta di creare impostazioni per il sito Redmond e il sito ospita già una raccolta di impostazioni di configurazione di Servizi utente.

Utenti autorizzati a eseguire questo cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsUserServicesConfiguration** i membri dei gruppi seguenti: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsUserServicesConfiguration"}

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
<td><p>Identificatore univoco per le impostazioni di configurazione di Servizi utente da creare. Per creare impostazioni nell'ambito del sito, usare una sintassi analoga alla seguente: -Identity site:Redmond. Per creare impostazioni a livello del servizio, usare una sintassi analoga alla seguente: -Identity service:UserServer:atl-cs-001.litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>AnonymousUserGracePeriod</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Indica la quantità di tempo in cui un utente anonimo (non autenticato) può rimanere in una riunione senza che alla stessa riunione sia presente un utente autenticato. Se, ad esempio, questo valore è impostato su 15 minuti, un utente anonimo può rimanere nella riunione al massimo per 15 minuti prima che sia necessario che un utente autenticato partecipi alla stessa riunione. Se un utente autenticato non prende parte alla riunione prima della scadenza del periodo di tolleranza, l'utente anonimo verrà rimosso dalla riunione. Questa impostazione si applica sia alle riunioni pianificate che alle riunioni ad hoc create facendo clic su Riunione immediata in Microsoft Lync.</p>
<p>È necessario specificare AnonymousUserGracePeriod utilizzando il seguente formato: giorni.ore:minuti:secondi, ad esempio 0.00:30:00 per indicare 30 minuti. È possibile impostare il periodo di tolleranza su qualsiasi valore compreso tra 0 secondi e 1 giorno; il valore predefinito è 90 minuti (01:30:00).</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DeactivationGracePeriod</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Il tempo massimo durante il quale una riunione può rimanere attiva. È necessario specificare questo valore utilizzando il seguente formato: giorni.ore:minuti:secondi. Ad esempio, per fare in modo che una riunione abbia una durata di 60 ore, è consigliabile utilizzare il seguente formato: 2.12:00:00 (2 giorni. 12 ore: 00 minuti: 00 secondi).</p>
<p>DeactivationGracePeriod deve essere compreso tra 8 ore e 365 giorni. Il valore predefinito è 1 giorno (1.00:00:00).</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultSubscriptionExpiration</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int64</p></td>
<td><p>Le sottoscrizioni vengono create ogni volta che un utente richiede dei dati, ad esempio le informazioni sulla presenza. Quando la richiesta viene emessa, l'utente o, più precisamente, l'applicazione client dell'utente, può richiedere la durata di validità della sottoscrizione prima del rinnovo. Se la richiesta non viene presentata, la sottoscrizione è impostata sul valore specificato dalla proprietà DefaultSubscriptionExpiration.</p>
<p>La durata predefinita della sottoscrizione deve essere espressa come numero intero compreso tra 300 secondi (5 minuti) e 86400 secondi (24 ore) inclusi. Il valore predefinito è 28800 secondi (8 ore).</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>MaintenanceTimeOfDay</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.DateTime</p></td>
<td><p>Indica l'ora del giorno in cui viene eseguita la regolare manutenzione programmata del database, ad esempio, la cancellazione dei record obsoleti. Questo valore deve essere specificato come valore di data e ora. È possibile utilizzare il formato 24 ore, ad esempio &quot;14:00&quot;, o il formato 12 ore, ad esempio &quot;2:00 PM&quot;.</p>
<p>Il valore predefinito per MaintenanceTimeOfDay è 1:00 AM (01:00:00).</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxContacts</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Il numero massimo di contatti consentiti per un utente. Il valore predefinito è 250. La proprietà MaxContacts rappresenta il numero massimo assoluto di contatti consentiti per un utente. Tuttavia, è possibile utilizzare i cmdlet CsClientPolicy per limitare alcuni utenti all'utilizzo di un numero massimo di contatti inferiore al valore della proprietà MaxContacts.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxPersonalNotes</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il numero massimo di note personali memorizzate nella cronologia note dell'utente. Per impostazione predefinita, le ultime 3 note personali sono mantenute nella cronologia note. Il numero massimo di note che è possibile mantenere nella cronologia è 10.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxScheduledMeetingsPerOrganizer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Il numero massimo di riunioni che un utente singolo è in grado di gestire come organizzatore in un dato lasso di tempo. Il valore predefinito è 1000. Se pertanto un utente è già l'organizzatore di 1000 riunioni, un eventuale richiesta per programmare una nuova riunione (numero di riunione 1001) avrà esito negativo.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxSubscriptionExpiration</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int64</p></td>
<td><p>Le sottoscrizioni vengono create ogni volta che un utente richiede dei dati, ad esempio le informazioni sulla presenza. Quando la richiesta viene emessa, l'utente o, più precisamente, l'applicazione client dell'utente, può richiedere la durata di validità della sottoscrizione prima del rinnovo. La proprietà MaxSubscriptionExpiration rappresenta il tempo massimo che può essere concesso ai client. Ad esempio, se il tempo massimo è impostato su 28800 secondi e un client richiede un intervallo di timeout di 86400 secondi, al client viene assegnato il periodo di scadenza massimo, 28800 secondi.</p>
<p>La durata massima della sottoscrizione deve essere espressa come numero intero compreso tra 300 secondi (5 minuti) e 86400 secondi (24 ore) inclusi. Il valore predefinito è 43200 secondi (12 ore).</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxSubscriptions</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero massimo di finestre di dialogo di sottoscrizione SIP che un utente può avere aperte in un determinato momento. Una finestra di dialogo di sottoscrizione rappresenta una richiesta di risorse SIP. Il valore predefinito è 200.</p></td>
</tr>
<tr class="even">
<td><p><em>MinSubscriptionExpiration</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int64</p></td>
<td><p>Le sottoscrizioni vengono create ogni volta che un utente richiede dei dati, ad esempio le informazioni sulla presenza. Quando la richiesta viene emessa, l'utente o, più precisamente, l'applicazione client dell'utente, può richiedere la durata di validità della sottoscrizione prima del rinnovo. La proprietà MinSubscriptionExpiration rappresenta il tempo minimo che può essere concesso ai client. Ad esempio, se il tempo minimo è impostato su 1200 secondi e un client richiede un intervallo di timeout di 200 secondi, al client viene assegnato il periodo di scadenza minimo, 1200 secondi.</p>
<p>La durata minima della sottoscrizione deve essere espressa come numero intero compreso tra 300 secondi (5 minuti) e 86400 secondi (24 ore) inclusi. Il valore predefinito è 1200 secondi (20 minuti).</p></td>
</tr>
<tr class="odd">
<td><p><em>PresenceProviders</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Raccolta di provider del servizio di presenza per le nuove impostazioni di configurazione di Servizi utenti. È preferibile aggiungere tali provider a una raccolta di impostazioni di configurazione di Servizi utenti utilizzando il cmdlet <strong>New-CsPresenceProvider</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>SubscribeToCollapsedDG</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True (valore predefinito), sarà consentito alle applicazioni client sottoscrivere gruppi di distribuzione attualmente non espansi nell'elenco contatti. In questo modo il client potrà gestire informazioni sulla presenza aggiornate per ciascun membro del gruppo. Se impostato su False, alle applicazioni client non sarà consentito di sottoscrivere i gruppi &quot;compressi&quot;.</p></td>
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

Nessuno. Il cmdlet **New-CsUserServicesConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **New-CsUserServicesConfiguration** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.storageService.StorageServiceSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsUserServicesConfiguration](get-csuserservicesconfiguration.md)  
[Remove-CsUserServicesConfiguration](remove-csuserservicesconfiguration.md)  
[Set-CsUserServicesConfiguration](set-csuserservicesconfiguration.md)

