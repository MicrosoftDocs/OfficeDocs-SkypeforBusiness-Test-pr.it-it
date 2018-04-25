---
title: Remove-CsDeviceUpdateConfiguration
TOCTitle: Remove-CsDeviceUpdateConfiguration
ms:assetid: 4335eb24-61a6-4e76-8242-edfd861d7d0b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425933(v=OCS.15)
ms:contentKeyID: 49300366
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsDeviceUpdateConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove le impostazioni di configurazione per l'aggiornamento dei dispositivi specificate. Queste impostazioni consentono di gestire il servizio Web di aggiornamento dispositivi, un componente di Lync Server utilizzato dagli amministratori per distribuire aggiornamenti del firmware ai telefoni e ad altri dispositivi in cui è in esecuzione Lync Phone Edition. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsDeviceUpdateConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene utilizzato il cmdlet **Remove-CsDeviceUpdateConfiguration** per "rimuovere" le impostazioni globali di configurazione dell'aggiornamento dei dispositivi. Dal momento che le impostazioni globali non possono essere realmente rimosse, il comando non elimina nulla. Tutte le proprietà nelle impostazioni globali di configurazione dell'aggiornamento dei dispositivi verranno tuttavia reimpostate sui rispettivi valori predefiniti.

    Remove-CsDeviceUpdateConfiguration -Identity global

## ESEMPIO 2

Il comando riportato nell'esempio 2 rimuove le impostazioni di configurazione per l'aggiornamento dei dispositivi con identità (identity) site:Redmond. Dal momento che queste impostazioni sono state configurate nell'ambito del sito, è possibile eliminarle e il sito Redmond non disporrà più di un insieme personale di impostazioni di configurazione per l'aggiornamento dei dispositivi.

    Remove-CsDeviceUpdateConfiguration -Identity site:Redmond

## ESEMPIO 3

Con l'esempio 3 vengono rimosse tutte le impostazioni di configurazione per l'aggiornamento dei dispositivi configurate nell'ambito del sito. Per eseguire tale operazione vengono utilizzati il cmdlet **Get-CsDeviceUpdateConfiguration** e il parametro Filter per restituire tutte le impostazioni la cui identità inizia con il valore stringa "site:"; per definizione, si tratta di tutte le impostazioni configurate nell'ambito del sito. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsDeviceUpdateConfiguration**, che rimuove ciascun elemento nella raccolta.

    Get-CsDeviceUpdateConfiguration -Filter "site:*" | Remove-CsDeviceUpdateConfiguration 

## ESEMPIO 4

Nell'esempio 4 vengono eliminate tutte le impostazioni di configurazione dell'aggiornamento dei dispositivi la cui proprietà MaxLogFileSize è maggiore di 1.024.000 byte. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsDeviceUpdateConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione dell'aggiornamento dei dispositivi. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni di configurazione in cui la proprietà MaxLogFileSize è maggiore di 1.024.000 byte. Tale raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsDeviceUpdateConfiguration**, che elimina ogni elemento della raccolta.

    Get-CsDeviceUpdateConfiguration | Where-Object {$_.MaxLogFileSize -lt 1024000} | Remove-CsDeviceUpdateConfiguration

## Descrizione dettagliata

Il servizio Web di aggiornamento dispositivi consente agli amministratori di distribuire aggiornamenti firmware ai dispositivi che eseguono Lync Phone Edition. Gli amministratori caricano periodicamente un insieme di regole di aggiornamento dei dispositivi su Lync Server. Dopo essere state verificate e approvate, queste regole possono essere applicate ai dispositivi appropriati non appena questi si connettono al sistema. I dispositivi verificano la disponibilità di aggiornamenti quando vengono accessi per la prima volta e di nuovo quando un utente esegue l'accesso. Successivamente, controllano la disponibilità di aggiornamenti ogni 24 ore.

Lync Server utilizza le impostazioni di configurazione per l'aggiornamento dei dispositivi al fine di gestire il servizio Web di aggiornamento dispositivi; queste impostazioni di configurazione possono essere applicate nell'ambito globale o del sito. Per impostazione predefinita, le impostazioni sono disponibili solo nell'ambito globale; tuttavia, è possibile utilizzare il cmdlet **New-CsDeviceUpdateConfiguration** per assegnare impostazioni personalizzate anche nell'ambito del sito.

È inoltre possibile utilizzare il cmdlet **Remove-CsDeviceUpdateConfiguration** per eliminare le impostazioni assegnate nell'ambito del sito. Quando si esegue questo cmdlet su un sito, le impostazioni di configurazione dell'aggiornamento dei dispositivi assegnate a tale sito vengono rimosse. È altresì possibile eseguire il cmdlet **Remove-CsDeviceUpdateConfiguration** sulle impostazioni globali. In questo caso, però, le impostazioni globali non verranno rimosse perché non è possibile rimuovere le impostazioni globali di configurazione dell'aggiornamento dei dispositivi. In realtà, le proprietà globali verranno reimpostate sui rispettivi valori predefiniti. Ad esempio, si supponga di avere modificato la proprietà globale MaxLogCacheLimit impostandola su 1.024.000 byte. Se si esegue il cmdlet **Remove-CsDeviceUpdateConfiguration** sulle impostazioni globali, queste non verranno rimosse, ma le proprietà modificate verranno reimpostate sui valori predefiniti. Questo significa che la proprietà MaxLogCacheLimit verrà reimpostata su 512.000 byte.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Remove-CsDeviceUpdateConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsDeviceUpdateConfiguration"}

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
<td><p>Indica l'identità delle impostazioni di configurazione per l'aggiornamento dei dispositivi da rimuovere. Per fare riferimento alle impostazioni globali, utilizzare la sintassi seguente: -Identity global. Per referenziare le impostazioni del sito, utilizzare una sintassi simile a quella riportata di seguito: -Identity site:Redmond. Si noti che non è possibile utilizzare i caratteri jolly quando si specifica un parametro Identity.</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdateConfiguration. Il cmdlet **Remove-CsDeviceUpdateConfiguration** accetta le istanze dell'oggetto configurazione dell'aggiornamento dei dispositivi inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsDeviceUpdateConfiguration** elimina invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdateConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsDeviceUpdateConfiguration](get-csdeviceupdateconfiguration.md)  
[New-CsDeviceUpdateConfiguration](new-csdeviceupdateconfiguration.md)  
[Set-CsDeviceUpdateConfiguration](set-csdeviceupdateconfiguration.md)

