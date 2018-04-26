---
title: New-CsDeviceUpdateConfiguration
TOCTitle: New-CsDeviceUpdateConfiguration
ms:assetid: 2a06450d-291e-40f9-a780-45e2c4b28494
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425761(v=OCS.15)
ms:contentKeyID: 49300007
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsDeviceUpdateConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova istanza delle impostazioni di configurazione per l'aggiornamento dei dispositivi. Queste impostazioni vengono utilizzate per gestire il servizio Web di aggiornamento dispositivi, un componente di Lync Server che consente agli amministratori di distribuire aggiornamenti firmware ai telefoni e ad altri dispositivi in cui è installato Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsDeviceUpdateConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-LogCleanUpInterval <TimeSpan>] [-LogCleanUpTimeOfDay <DateTime>] [-LogFlushInterval <TimeSpan>] [-MaxLogCacheLimit <UInt32>] [-MaxLogFileSize <UInt32>] [-ValidLogFileExtensions <PSListModifier>] [-ValidLogFileTypes <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di creare un nuovo gruppo di impostazioni di configurazione per l'aggiornamento dei dispositivi con Identity site:Redmond. Dal momento che nel comando non sono inclusi altri parametri, questa nuova raccolta di impostazioni di configurazione utilizzerà i valori predefiniti per ogni proprietà.

    New-CsDeviceUpdateConfiguration -Identity site:Redmond

## ESEMPIO 2

Anche nell'esempio 2 viene creato un nuovo insieme di impostazioni di configurazione per l'aggiornamento dei dispositivi con Identity site:Redmond. In questo caso, vengono utilizzati altri due parametri per personalizzare le nuove impostazioni: MaxLogFileSize per impostare la dimensione massima del file di log su 2048000 byte e LogCleanUpInterval per impostare l'intervallo di pulizia del log su 7 giorni (7 giorni . 00 ore : 00 minuti : 00 secondi).

    New-CsDeviceUpdateConfiguration -Identity site:Redmond -MaxLogFileSize 204800 -LogCleanUpInterval 7.00:00:00

## Descrizione dettagliata

Il servizio Web di aggiornamento dispositivi consente agli amministratori di distribuire aggiornamenti firmware ai dispositivi che eseguono Lync Server. Gli amministratori caricano periodicamente un insieme di regole di aggiornamento dei dispositivi su Lync Server. Dopo essere state verificate e approvate, queste regole possono essere applicate ai dispositivi appropriati non appena questi si connettono al sistema. I dispositivi verificano la disponibilità di aggiornamenti quando vengono accessi per la prima volta e di nuovo quando un utente esegue l'accesso. Successivamente, controllano la disponibilità di aggiornamenti ogni 24 ore.

Le impostazioni di configurazione per l'aggiornamento dei dispositivi, utilizzate per gestire servizio Web di aggiornamento dispositivi, possono essere assegnate a livello globale o nell'ambito del sito. Per creare una nuova raccolta di impostazioni per un sito, utilizzare il cmdlet **New-CsDeviceUpdateConfiguration**. Si noti che è possibile creare le nuove impostazioni solo nell'ambito del sito; il comando avrà esito negativo se si cerca di creare una nuova raccolta di impostazioni nell'ambito globale. Inoltre, il comando avrà esito negativo se si cerca di creare una nuova raccolta di impostazioni per il sito Redmond e quel sito ospita già una raccolta di impostazioni di configurazione per l'aggiornamento dei dispositivi. Ciò perché per ogni sito è possibile avere solo una raccolta di impostazioni di configurazione per l'aggiornamento dei dispositivi.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsDeviceUpdateConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsDeviceUpdateConfiguration"}

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
<td><p>Indica l'identità delle nuove impostazioni di configurazione per l'aggiornamento dei dispositivi. Dal momento che le nuove impostazioni possono essere create solo nell'ambito del sito, il parametro Identity sarà simile al seguente: -Identity &quot;site:Redmond&quot;.</p></td>
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
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
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
<p>Il valore specificato per il parametro LogCleanupTimeOfDay deve essere nel formato 24 ore hh:mm, dove hh indica le ore e mm i minuti. In questo formato, 00:00 indica la mezzanotte; 08:30 indica le otto e trenta di mattina e 23:52 indica le undici e cinquantadue di sera. Il valore predefinito è Null.</p></td>
</tr>
<tr class="odd">
<td><p><em>LogFlushInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Indica la frequenza con cui le informazioni archiviate nella cache del file di log vengono scritte nel file di log effettivo. Per impostazione predefinita, le informazioni sull'aggiornamento dei dispositivi non vengono scritte immediatamente nel file di log, ma vengono memorizzate nella cache finché: 1) l'intervallo di tempo flush del log non scade; 2) la cache non raggiunge la dimensione massima. Se questo valore è impostato su 10 minuti (00:10:00), le informazioni nella cache verranno scritte nel file di log ogni 10 minuti. Dopo aver registrato i dati, la cache verrà eliminata.</p>
<p>Il valore deve essere immesso nel formato hh:mm:ss, dove hh è il numero di ore, mm è il numero di minuti e ss è il numero di secondi.</p>
<p>Valore minimo: 00:01:00 (1 minuto)</p>
<p>Valore massimo: 1:00:00 (1 ora)</p>
<p>Valore predefinito: 00:05:00</p></td>
</tr>
<tr class="even">
<td><p><em>MaxLogCacheLimit</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il numero massimo di informazioni (in byte) che la cache del file di log può contenere prima che sia necessario svuotarla e scrivere i dati in un file di log. Per impostazione predefinita, i file di log vengono scaricati ogni X minuti. Per ulteriori informazioni, fare riferimento alla descrizione del parametro LogFlushInterval. Tuttavia, se la cache raggiunge la dimensione massima, le informazioni in essa contenute verranno scritte automaticamente nel file di log (e la cache verrà svuotata) anche se non è ancora scaduto l'intervallo flush del log.</p>
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
<td><p>Indica le estensioni del file di log valide che possono essere utilizzate con servizio Web di aggiornamento dispositivi. Questo elenco può essere modificato. Tuttavia, non vi è alcun motivo per modificarlo a meno che non si utilizzi un dispositivo con Lync Server, che crea file di log che utilizzano un'estensione file diversa.</p>
<p>Valore predefinito: .dmp, .clg, .clg2, .bak, .kdmp, .dat, .bin, .cat, .xml, .txt, .hex</p></td>
</tr>
<tr class="odd">
<td><p><em>ValidLogFileTypes</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Indica i tipi di file di log mantenuti dal sistema di aggiornamento dei dispositivi. I tipi di file predefiniti comprendono:</p>
<p>Watson. File di log generati automaticamente da un dispositivo se il sistema smette di rispondere.</p>
<p>CELog. Log per telefoni con Lync che includono i risultati dei test funzionali e un record degli eventi di sistema critici.</p>
<p>È possibile aggiungere altri tipi di file se si dispone di un dispositivo con Lync Phone Edition che crea un diverso tipo di file di log. È inoltre possibile rimuovere file. Se ad esempio non si desidera archiviare i file CELog, è possibile rimuovere il tipo di file CELog.</p></td>
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

Nessuno. Il cmdlet **New-CsDeviceUpdateConfiguration** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsDeviceUpdateConfiguration** crea le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdateConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsDeviceUpdateConfiguration](get-csdeviceupdateconfiguration.md)  
[Remove-CsDeviceUpdateConfiguration](remove-csdeviceupdateconfiguration.md)  
[Set-CsDeviceUpdateConfiguration](set-csdeviceupdateconfiguration.md)

