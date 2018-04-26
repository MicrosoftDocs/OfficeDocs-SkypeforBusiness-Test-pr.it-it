---
title: Set-CsUserServicesConfiguration
TOCTitle: Set-CsUserServicesConfiguration
ms:assetid: 51d76f29-4b2b-4208-962c-c5420414ad1b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398340(v=OCS.15)
ms:contentKeyID: 49300550
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUserServicesConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta esistente di impostazioni di configurazione di Servizi utente. Il servizio Servizi utente viene utilizzato per gestire le conferenze e conservare le informazioni sulla presenza. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsUserServicesConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsUserServicesConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AnonymousUserGracePeriod <TimeSpan>] [-Confirm [<SwitchParameter>]] [-DeactivationGracePeriod <TimeSpan>] [-DefaultSubscriptionExpiration <Int64>] [-Force <SwitchParameter>] [-MaintenanceTimeOfDay <DateTime>] [-MaxContacts <UInt16>] [-MaxPersonalNotes <UInt32>] [-MaxScheduledMeetingsPerOrganizer <UInt32>] [-MaxSubscriptionExpiration <Int64>] [-MaxSubscriptions <UInt16>] [-MinSubscriptionExpiration <Int64>] [-PresenceProviders <PSListModifier>] [-SubscribeToCollapsedDG <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di modificare le impostazioni di configurazione di Servizi utente per il sito Redmond (-Identity site:Redmond). In questo esempio, il valore di AnonymousUserGracePeriod è impostato su 30 minuti (00 ore: 30 minuti: 00 secondi).

    Set-CsUserServicesConfiguration -Identity site:Redmond -AnonymousUserGracePeriod "00:30:00"

## ESEMPIO 2

Nell'Esempio 2, nelle impostazioni di configurazione di Servizi utente applicate al sito Redmond viene modificata la proprietà MaintenanceTimeOfDay. Per ottenere questo risultato, il parametro MaintenanceTimeOfDay viene, ad esempio, impostato su 13:30 e di conseguenza questa sarà l'ora in cui verrà eseguita la manutenzione.

    Set-CsUserServicesConfiguration -Identity site:Redmond -MaintenanceTimeOfDay "13:30"

## ESEMPIO 3

Nell'esempio 3 vengono recuperate tutte le impostazioni di configurazione di Servizi utente applicate nell'ambito del servizio e quindi viene modificato il numero massimo di contatti consentiti per ognuno di questi elementi. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsUserServicesConfiguration** e il parametro Filter per recuperare tutte le impostazioni configurate nell'ambito del servizio. Il valore di filtro "service:\*" restituisce solo i dati relativi alle impostazioni la cui identità inizia con la stringa "service:". La raccolta filtrata viene quindi passata al cmdlet **Set-CsUserServicesConfiguration**, che imposta su 300 la proprietà MaxContacts per ogni elemento della raccolta.

    Get-CsUserServicesConfiguration -Filter "service:*" | Set-CsUserServicesConfiguration -MaxContacts 300

## ESEMPIO 4

Nell'esempio 4 vengono modificate tutte le impostazioni di configurazione di Servizi utente che consentono agli utenti di avere più di 300 contatti. Dopo questa modifica, nessuna impostazione consentirà di avere più di 300 contatti. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsUserServicesConfiguration** senza parametri aggiuntivi. Viene così restituita una raccolta di tutte le impostazioni di configurazione di Servizi utente attualmente in uso nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà MaxContacts è maggiore di 300. La raccolta filtrata viene a sua volta inviata tramite pipe al cmdlet **Set-CsUserServicesConfiguration**, che imposta su 300 il numero massimo di contatti consentiti per ogni elemento della raccolta filtrata.

    Get-CsUserServicesConfiguration | Where-Object {$_.MaxContacts -gt 300} | Set-CsUserServicesConfiguration -MaxContacts 300

## Descrizione dettagliata

Lync Server utilizza il servizio Servizi utente per mantenere le informazioni sulla presenza degli utenti e per gestire le riunioni e le conferenze. A loro volta, i cmdlet **CsUserServicesConfiguration** vengono utilizzati per amministrare le impostazioni di configurazione di Servizi utente nell'ambito globale, del sito e del servizio. Si noti che l'unico servizio in grado di ospitare le impostazioni di configurazione di Servizi utente è il servizio stesso. Queste impostazioni consentono di specificare elementi quali il numero di contatti di cui un utente può disporre, il numero di riunioni pianificate che un utente può avere in un determinato momento e l'intervallo di tempo massimo in cui una determinata riunione può rimanere attiva.

Il cmdlet **Set-CsUserServicesConfiguration** consente agli amministratori di modificare le informazioni relative a una o più impostazioni di configurazione di Servizi utente attualmente in uso.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsUserServicesConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsUserServicesConfiguration"}

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
<td><p><em>AnonymousUserGracePeriod</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Indica per quanto un utente anonimo (non autenticato) può rimanere in una riunione senza che alla stessa riunione sia presente un utente autenticato. Se ad esempio questo valore è impostato su 15 minuti, un utente anonimo può rimanere nella riunione al massimo per 15 minuti prima che sia necessario che un utente autenticato partecipi alla stessa riunione. Se un utente autenticato non prende parte alla riunione prima della scadenza del periodo di tolleranza, l'utente anonimo verrà rimosso dalla riunione. Questa impostazione si applica sia alle riunioni pianificate sia alle riunioni ad hoc create facendo clic su Riunione immediata in Lync.</p>
<p>Il valore della proprietà AnonymousUserGracePeriod deve essere specificato nel formato seguente: giorni.minuti:secondi (ad esempio 0.00:30:00 per indicare 30 minuti). Il periodo di tolleranza può essere impostato su un valore compreso tra 0 secondi e 1 giorno. Il valore predefinito è 90 minuti (01:30:00).</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>DeactivationGracePeriod</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>La quantità massima di tempo in cui una riunione può rimanere attiva. Questo valore deve essere specificato nel seguente formato: giorni.ore:minuti:secondi. Ad esempio, per indicare che una riunione deve rimanere attiva per 60 ore si utilizza il seguente formato: 2.12:00:00 (2 giorni: 12 ore: 00 minuti: 00 secondi).</p>
<p>Il valore della proprietà DeactivationGracePeriod deve essere compreso tra 8 ore e 365 giorni, inclusi. Il valore predefinito è 1 giorno.</p></td>
</tr>
<tr class="even">
<td><p><em>DefaultSubscriptionExpiration</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int64</p></td>
<td><p>Ogni volta che un utente effettua una richiesta di dati, come, ad esempio, le informazioni sulla presenza, vengono create delle sottoscrizioni. Quando la richiesta viene effettuata, l'utente, o più correttamente l'applicazione client dell'utente, può richiedere la durata del periodo di validità della sottoscrizione prima che sia necessario rinnovarla. Se non viene effettuata alcuna richiesta, la sottoscrizione viene impostata sul valore specificato dalla proprietà DefaultSubscriptionExpiration.</p>
<p>La durata minima predefinita della sottoscrizione deve essere espressa come numero intero compreso tra 300 secondi (5 minuti) e 86400 secondi (24 ore), inclusi. Il valore predefinito è 28800 secondi (8 ore).</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni di configurazione di Servizi utente da modificare. Per modificare le impostazioni globali, utilizzare la seguente sintassi: -Identity global. Per modificare le impostazioni configurate nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Per modificare le impostazioni a livello di servizio, utilizzare una sintassi simile alla seguente: -Identity service:UserServer:atl-cs-001.litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto UserServicesSettings</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>MaintenanceTimeOfDay</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.DateTime</p></td>
<td><p>Indica l'ora in cui viene effettuata la manutenzione del database pianificata su base regolare, ad esempio, la cancellazione dei record obsoleti. Questo valore deve essere specificato come data-ora, con la possibilità di scegliere tra il formato 24 ore (ad esempio, &quot;14:00&quot;) e il formato 12 ore (in uso nel mondo anglosassone, ad esempio, &quot;2:00 PM&quot;).</p>
<p>Il valore predefinito per MaintenanceTimeOfDay è 1:00 AM (01:00:00).</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxContacts</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Il numero massimo di contatti che un utente può avere; il valore predefinito è 250. La proprietà MaxContacts esprime il numero massimo assoluto di contatti che un utente può avere. Tuttavia, è possibile utilizzare i cmdlet <strong>CsClientPolicy</strong> per specificare, per determinati utenti, un numero massimo di contatti inferiore a quello impostato in MaxContacts.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxPersonalNotes</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il numero massimo di note personali memorizzate nella cronologia note dell'utente. Per impostazione predefinita, le ultime 3 note personali vengono conservate nella cronologia note. Il numero massimo di note che possono essere conservate nella cronologia è 10.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxScheduledMeetingsPerOrganizer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Il numero massimo di riunioni per le quali un singolo utente può fungere da organizzatore a una data ora. Il valore predefinito è 1000. Ciò significa che se un utente è già l'organizzatore di 1000 riunioni, la sua richiesta di pianificare una nuova riunione (la numero 1001) avrà esito negativo.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxSubscriptionExpiration</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int64</p></td>
<td><p>Ogni volta che un utente effettua una richiesta di dati, come, ad esempio, le informazioni sulla presenza, vengono create delle sottoscrizioni. Quando la richiesta viene effettuata, l'utente, o più correttamente l'applicazione client dell'utente, può richiedere la durata del periodo di validità della sottoscrizione prima che sia necessario rinnovarla. La proprietà MaxSubscriptionExpiration esprime la durata massima del periodo di concessione dei client. Ad esempio, se la durata massima è impostata su 28800 secondi e il client richiede un intervallo di timeout pari a 86400 secondi, al client verrà assegnato il periodo di validità massimo consentito: 28800 secondi.</p>
<p>La durata massima della sottoscrizione deve essere espressa come numero intero compreso tra 300 secondi (5 minuti) e 86400 secondi (24 ore), inclusi. Il valore predefinito è 43200 secondi (12 ore).</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxSubscriptions</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Il numero massimo di finestre di dialogo di sottoscrizione SIP che un utente può tenere simultaneamente aperte. Una finestra di dialogo di sottoscrizione rappresenta una richiesta di risorse SIP.</p></td>
</tr>
<tr class="even">
<td><p><em>MinSubscriptionExpiration</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int64</p></td>
<td><p>Ogni volta che un utente effettua una richiesta di dati, come, ad esempio, le informazioni sulla presenza, vengono create delle sottoscrizioni. Quando la richiesta viene effettuata, l'utente, o più correttamente l'applicazione client dell'utente, può richiedere la durata del periodo di validità della sottoscrizione prima che sia necessario rinnovarla. La proprietà MinSubscriptionExpiration esprime la durata minima del periodo di concessione dei client. Ad esempio, se la durata minima è impostata su 1200 secondi e il client richiede un intervallo di timeout pari a 200 secondi, al client verrà assegnato il periodo di validità minimo consentito: 1200 secondi.</p>
<p>La durata minima della sottoscrizione deve essere espressa come numero intero compreso tra 300 secondi (5 minuti) e 86400 secondi (24 ore), inclusi. Il valore predefinito è 1200 secondi (20 minuti).</p></td>
</tr>
<tr class="odd">
<td><p><em>PresenceProviders</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Raccolta di provider del servizio di presenza per le impostazioni di configurazione di Servizi utenti. È preferibile aggiungere tali provider a una raccolta di impostazioni di configurazione di Servizi utenti utilizzando il cmdlet <strong>New-CsPresenceProvider</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>SubscribeToCollapsedDG</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True (il valore predefinito), alle applicazioni client sarà consentito di iscriversi ai gruppi di distribuzione attualmente non espansi nell'elenco dei contatti. Ciò consente al client di conservare informazioni sulla presenza di ciascun membro del gruppo aggiornate al minuto. Se impostato su False, alle applicazioni client non verrà consentito di iscriversi ai gruppi &quot;compressi&quot;.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.UserServicesSettings. Il cmdlet **Set-CsUserServicesConfiguration** accetta le istanze dell'oggetto impostazioni di Servizi utente inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsUserServicesConfiguration** non restituisce oggetti o valori. Il cmdlet invece configura le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.UserServicesSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsUserServicesConfiguration](get-csuserservicesconfiguration.md)  
[New-CsUserServicesConfiguration](new-csuserservicesconfiguration.md)  
[Remove-CsUserServicesConfiguration](remove-csuserservicesconfiguration.md)

