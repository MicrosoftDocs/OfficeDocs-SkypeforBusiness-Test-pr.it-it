---
title: Set-CsDeviceUpdateConfiguration
TOCTitle: Set-CsDeviceUpdateConfiguration
ms:assetid: 4f200a03-984a-4c5b-a9c1-a866ba1851cd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398320(v=OCS.15)
ms:contentKeyID: 49300525
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsDeviceUpdateConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta di impostazioni di configurazione del servizio Web di aggiornamento dispositivi. Queste impostazioni vengono utilizzate per gestire il servizio Web di aggiornamento dispositivi, un componente di Lync Server che consente agli amministratori di distribuire aggiornamenti firmware ai telefoni e ad altri dispositivi in cui è in esecuzione Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsDeviceUpdateConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsDeviceUpdateConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-LogCleanUpInterval <TimeSpan>] [-LogCleanUpTimeOfDay <DateTime>] [-LogFlushInterval <TimeSpan>] [-MaxLogCacheLimit <UInt32>] [-MaxLogFileSize <UInt32>] [-ValidLogFileExtensions <PSListModifier>] [-ValidLogFileTypes <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene illustrato come utilizzare il cmdlet **Set-CsDeviceUpdateConfiguration** per modificare le impostazioni di configurazione globali. In questo caso, vengono modificati i valori di due proprietà: la proprietà MaxLogFileSize viene impostata su 2048000 byte e la proprietà MaxLogCacheLimit viene impostata su 1024000 byte.

    Set-CsDeviceUpdateConfiguration -Identity global -MaxLogFileSize 2048000 -MaxLogCacheLimit 1024000

## ESEMPIO 2

Nell'esempio 2 viene modificata la proprietà LogFlushInterval per le impostazioni di configurazione per l'aggiornamento dei dispositivi con identità (Identity) site:Redmond. Per ottenere questo risultato, vengono utilizzati il parametro Identity per specificare le impostazioni nel sito Redmond e il parametro LogFlushInterval per indicare il valore della proprietà da modificare. In questo caso, LogFlushInterval è impostato su 2 minuti (00 ore: 02 minuti: 00 secondi).

    Set-CsDeviceUpdateConfiguration -Identity site:Redmond -LogFlushInterval 00:02:00

## ESEMPIO 3

Nell'esempio 3 vengono modificate tutte le impostazioni di configurazione dell'aggiornamento dei dispositivi dell'organizzazione in modo tale che LogCleanUpInterval venga impostato su 14 giorni. A tale scopo, viene utilizzato innanzitutto il cmdlet **Get-CsDeviceUpdateConfiguration** per recuperare una raccolta di tutte le impostazioni di configurazione dell'aggiornamento dei dispositivi. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsDeviceUpdateConfiguration**, che utilizza il parametro LogCleanUpInterval per impostare l'intervallo di pulizia del log per ogni elemento della raccolta su 14 giorni (14 giorni . 00 ore : 00 minuti : 00 secondi).

    Get-CsDeviceUpdateConfiguration | Set-CsDeviceUpdateConfiguration -LogCleanUpInterval 14.00:00:00

## ESEMPIO 4

Nell'esempio 4 viene illustrato come modificare il valore di una proprietà per tutte le impostazioni di configurazione dell'aggiornamento dei dispositivi configurate nell'ambito del sito. In questo caso, il comando imposta LogCleanUpInterval su 20 giorni (20 giorni . 00 ore : 00 minuti : 00 secondi). A tale scopo, viene utilizzato il cmdlet **Get-CsDeviceUpdateConfiguration** con il parametro Filter. Il valore di filtro "site:\*" restituisce solo i dati relativi alle impostazioni la cui identità inizia con il valore stringa "site:". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsDeviceUpdateConfiguration**, che modifica il valore dell'intervallo di pulizia del log per ogni elemento della raccolta.

    Get-CsDeviceUpdateConfiguration -Filter "site:*" | Set-CsDeviceUpdateConfiguration -LogCleanUpInterval 20.00:00:00

## ESEMPIO 5

Nell'esempio 5 viene rimosso CELog dall'elenco dei tipi di file di log validi utilizzato dalle impostazioni di configurazione dell'aggiornamento dei dispositivi. In questo comando viene utilizzato innanzitutto il cmdlet **Get-CsDeviceUpdateConfiguration** per recuperare una raccolta di tutte le impostazioni di configurazione dell'aggiornamento dei dispositivi attualmente in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsDeviceUpdateConfiguration**, che utilizza il parametro ValidLogFileTypes per rimuovere CELog dall'elenco dei tipi di file di log validi. Il valore del parametro passato a ValidLogFileTypes, @{Remove="CELog"}, indica al cmdlet **Set-CsDeviceUpdateConfiguration** di rimuovere CELog dall'insieme di tipi di file validi. Per rimuovere più tipi di file con un unico comando, includere i tipi aggiuntivi come elenco di valori separati da virgole. Ad esempio:

@{Remove="CELog","Watson"}

    Get-CsDeviceUpdateConfiguration | Set-CsDeviceUpdateConfiguration -ValidLogFileTypes @{Remove="CELog"}

## Descrizione dettagliata

Il servizio Web di aggiornamento dispositivi consente agli amministratori di distribuire aggiornamenti firmware ai dispositivi in cui viene eseguito Lync Phone Edition. Gli amministratori caricano periodicamente un insieme di regole di aggiornamento dei dispositivi su Lync Server. Dopo essere state verificate e approvate, queste regole possono essere applicate ai dispositivi appropriati non appena questi si connettono al sistema. I dispositivi verificano la disponibilità di aggiornamenti quando vengono accessi per la prima volta e di nuovo quando un utente esegue l'accesso. Successivamente, controllano la disponibilità di aggiornamenti ogni 24 ore.

Le impostazioni di configurazione per l'aggiornamento dei dispositivi possono essere applicate nell'ambito globale o del sito. Il cmdlet **Set-CsDeviceUpdateConfiguration** consente di modificare una raccolta di impostazioni. Ad esempio, è possibile utilizzare questo cmdlet per modificare per quanto tempo viene conservato un file di registrazione prima che venga eliminato automaticamente dal sistema.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsDeviceUpdateConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsDeviceUpdateConfiguration"}

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
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni di configurazione per l'aggiornamento del dispositivo da modificare. Per ottenere le impostazioni globali, utilizzare la seguente sintassi: -Identity global. Per ottenere le impostazioni del sito, utilizzare una sintassi simile alla seguente: -Identity &quot;site:Redmond&quot;. Si noti che non è consentito utilizzare i caratteri jolly per specificare l'identità.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto DeviceUpdateSettings</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>LogCleanUpInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Consente di specificare il periodo di tempo in cui un file di log per l'aggiornamento del dispositivo viene mantenuto prima che venga eliminato dal sistema.</p>
<p>Il valore deve essere immesso nel formato gg.hh:mm:ss, dove gg è il numero di giorni, hh è il numero di ore, mm è il numero di minuti e ss è il numero di secondi. Per immettere solo i giorni, è necessario immettere dopo il valore un punto (.).</p>
<p>Valore minimo: 1.00:00:00 (1 giorno)</p>
<p>Valore massimo: 365.00:00:00 (1 anno)</p>
<p>Valore predefinito: 10.00:00:00 (10 giorni)</p></td>
</tr>
<tr class="even">
<td><p><em>LogCleanUpTimeOfDay</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.DateTime</p></td>
<td><p>Indica l'ora e il giorno in cui il sistema controlla la presenza di eventuali file di log scaduti che è necessario eliminare. I file di log &quot;scaduti&quot; sono tutti quei file più vecchi del valore specificato per la proprietà LogCleanupInterval.</p>
<p>Il valore specificato per il parametro LogCleanupTimeOfDay deve essere nel formato 24 ore hh:mm, dove hh indica le ore e mm i minuti. In questo formato, 00:00 indica la mezzanotte; 08:30 indica le otto e trenta di mattina e 23:52 indica le undici e cinquantadue di sera.</p></td>
</tr>
<tr class="odd">
<td><p><em>LogFlushInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Indica la frequenza con cui le informazioni archiviate nella cache del file di log vengono scritte nel file di log effettivo. Per impostazione predefinita, le informazioni sull'aggiornamento del dispositivo non vengono scritte immediatamente nel file di log, ma vengono memorizzate nella cache finché: 1) l'intervallo di tempo flush del log non scade; 2) la cache non raggiunge la dimensione massima. Se questo valore è impostato su 10 minuti (00:10:00), le informazioni nella cache verranno scritte nel file di log ogni 10 minuti. Dopo aver registrato i dati, la cache verrà eliminata.</p>
<p>Il valore deve essere immesso nel formato hh:mm:ss, dove hh è il numero di ore, mm è il numero di minuti e ss è il numero di secondi.</p>
<p>Valore minimo: 00:01:00 (1 minuto)</p>
<p>Valore massimo: 1:00:00 (1 ora)</p>
<p>Valore predefinito: 00:05:00</p></td>
</tr>
<tr class="even">
<td><p><em>MaxLogCacheLimit</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il numero massimo di informazioni (in byte) che è possibile contenere nella cache del file di log prima di essere eliminata e prima che i dati vengano scritti nel file di log. Per impostazione predefinita, i file di log vengono scaricati ogni 5 minuti. Per ulteriori informazioni, fare riferimento alla descrizione del parametro LogFlushInterval. Tuttavia, se la cache raggiunge la dimensione massima, le informazioni in essa contenute verranno scritte automaticamente nel file di log (e la cache verrà svuotata) anche se non è ancora scaduto l'intervallo flush del log.</p>
<p>Valore predefinito: 512000</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxLogFileSize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica la dimensione massima, in byte, di un file di log. Quando un file raggiunge la dimensione massima, il batch successivo di dati viene scritto automaticamente in un nuovo file di log. Il file di log precedente verrà mantenuto finché non scade l'intervallo di pulizia del log.</p>
<p>Valore predefinito: 1024000</p></td>
</tr>
<tr class="even">
<td><p><em>ValidLogFileExtensions</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Indica le estensioni del file di log valide che possono essere utilizzate con il servizio Web Aggiornamento dispositivi. Questo elenco può essere modificato. Non è tuttavia necessario modificarlo, a meno che non si utilizzi un dispositivo compatibile con Lync Phone Edition che crea file di log che utilizzano un'estensione di file diversa.</p>
<p>Valore predefinito: .dmp, .clg, .clg2, .bak, .kdmp, .dat, .bin, .cat, .xml, .txt, .hex</p></td>
</tr>
<tr class="odd">
<td><p><em>ValidLogFileTypes</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Indica i tipi di file di log mantenuti dal sistema di aggiornamento dei dispositivi. I tipi di file predefiniti comprendono:</p>
<p>Watson. File di log creati automaticamente da un dispositivo nel caso si verifichi un arresto anomalo del sistema.</p>
<p>CELog. Log per telefoni con Lync in cui sono contenuti i risultati dei test funzionali e una registrazione di eventi di sistema critici.</p>
<p>È possibile aggiungere altri tipi di file se si dispone di un dispositivo compatibile con Lync Phone Edition che crea un diverso tipo di file di log. È inoltre possibile rimuovere file. Se ad esempio non si desidera archiviare i file CELog, è possibile rimuovere il tipo di file CELog.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdateConfiguration. Il cmdlet **Set-CsDeviceUpdateConfiguration** accetta le istanze dell'oggetto configurazione dell'aggiornamento dei dispositivi inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsDeviceUpdateConfiguration** non restituisce oggetti o valori. Il cmdlet invece configura le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdateConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsDeviceUpdateConfiguration](get-csdeviceupdateconfiguration.md)  
[New-CsDeviceUpdateConfiguration](new-csdeviceupdateconfiguration.md)  
[Remove-CsDeviceUpdateConfiguration](remove-csdeviceupdateconfiguration.md)

