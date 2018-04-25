---
title: Get-CsDeviceUpdateConfiguration
TOCTitle: Get-CsDeviceUpdateConfiguration
ms:assetid: e7adc8a7-616a-41b1-8f4b-5f8778e46f55
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399030(v=OCS.15)
ms:contentKeyID: 49302299
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsDeviceUpdateConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle impostazioni di configurazione per l'aggiornamento dei dispositivi attualmente distribuite nell'organizzazione. Queste impostazioni consentono di gestire il servizio Web di aggiornamento dispositivi, un componente di Lync Server utilizzato dagli amministratori per distribuire gli aggiornamenti del firmware ai telefoni e ad altri dispositivi in cui è in esecuzione Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsDeviceUpdateConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsDeviceUpdateConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 viene restituita una raccolta di tutte le impostazioni di configurazione dell'aggiornamento dei dispositivi attualmente in uso nell'organizzazione. Chiamando il cmdlet **Get-CsDeviceUpdateConfiguration** senza ulteriori parametri, vengono restituite tutte le impostazioni di aggiornamento dei dispositivi attualmente in uso.

    Get-CsDeviceUpdateConfiguration 

## ESEMPIO 2

Nell'esempio 2 vengono restituite informazioni relative alle impostazioni globali di configurazione dell'aggiornamento dei dispositivi.

    Get-CsDeviceUpdateConfiguration -Identity Global

## ESEMPIO 3

Nell'esempio 3 viene mostrato l'utilizzo del parametro Filter. Con il valore "site:\*" per il filtro viene restituita una raccolta di tutte le impostazioni di configurazione dell'aggiornamento dei dispositivi applicate nell'ambito del sito; questo perché tali impostazioni presentano tutte un valore Identity che inizia con il valore stringa "site:".

    Get-CsDeviceUpdateConfiguration -Filter site:*

## ESEMPIO 4

Nell'esempio 4 vengono restituite tutte le impostazioni di configurazione dell'aggiornamento dei dispositivi in cui la proprietà MaxLogFileSize è maggiore di 2.048.000 byte. A tale scopo, viene utilizzato il cmdlet **Get-CsDeviceUpdateConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione dell'aggiornamento dei dispositivi attualmente in uso. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona soltanto le impostazioni nelle quali la proprietà MaxLogFileSize è maggiore di 2.048.000.

    Get-CsDeviceUpdateConfiguration | Where-Object {$_.MaxLogFileSize -gt 2048000}

## ESEMPIO 5

Con il comando mostrato nell'esempio 5 vengono restituite tutte le impostazioni di configurazione dell'aggiornamento dei dispositivi che includono "Watson" come tipo di file di log valido. Per eseguire questa attività, viene utilizzato il cmdlet **Get-CsDeviceUpdateConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione dell'aggiornamento dei dispositivi. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona soltanto le impostazioni dei dispositivi che includono "Watson" nel proprio set di tipi di file di log validi.

    Get-CsDeviceUpdateConfiguration | Where-Object {$_.ValidLogFileTypes -like "*Watson*"}

## Descrizione dettagliata

Il servizio Web di aggiornamento dispositivi consente agli amministratori di distribuire gli aggiornamenti del firmware ai dispositivi in cui è in esecuzione Lync Server. Gli amministratori periodicamente caricano un insieme di regole di aggiornamento dei dispositivi in Lync Server. Una volta verificate e approvate, tali regole possono essere applicate ai dispositivi appropriati non appena questi si connettono al sistema. I dispositivi infatti verificano l'eventuale presenza di aggiornamenti inizialmente quando vengono accesi e quindi di nuovo quando un utente esegue l'accesso. Successivamente controllano la disponibilità di aggiornamenti ogni 24 ore.

Il servizio Web di aggiornamento dispositivi viene gestito mediante impostazioni di configurazione dei dispositivi che possono essere applicate nell'ambito globale o nell'ambito del sito. È possibile utilizzare il cmdlet **Get-CsDeviceUpdateConfiguration** per restituire informazioni relative alle impostazioni di configurazione dell'aggiornamento dei dispositivi attualmente in uso nell'organizzazione.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsDeviceUpdateConfiguration** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Approve-CsDeviceUpdateRule"}

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
<td><p>Fornisce un modo per utilizzare i caratteri jolly per specificare le impostazioni di configurazione dell'aggiornamento dei dispositivi. Ad esempio, per restituire una raccolta di tutte le impostazioni di configurazione applicate nell'ambito del sito, utilizzare la seguente sintassi: -Filter &quot;site:*&quot;. Per restituire tutte le impostazioni che presentano il termine &quot;EMEA&quot; nel valore Identity, utilizzare la seguente sintassi: -Filter &quot;*EMEA*&quot;. Il parametro Filter agisce soltanto sul valore Identity delle impostazioni. Non è pertanto possibile filtrare in base ad altre proprietà di configurazione dell'aggiornamento dei dispositivi.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica l'identità delle impostazioni di configurazione dell'aggiornamento dei dispositivi da recuperare. Per fare riferimento alle impostazioni globali, utilizzare la sintassi seguente: -Identity global. Per far riferimento alle impostazioni del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Si noti che non è possibile utilizzare i caratteri jolly quando si specifica un parametro Identity. Per poter utilizzare i caratteri jolly, è necessario includere il parametro Filter.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione dell'aggiornamento dei dispositivi dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsDeviceUpdateConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsDeviceUpdateConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdateConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsDeviceUpdateConfiguration](new-csdeviceupdateconfiguration.md)  
[Remove-CsDeviceUpdateConfiguration](remove-csdeviceupdateconfiguration.md)  
[Set-CsDeviceUpdateConfiguration](set-csdeviceupdateconfiguration.md)

