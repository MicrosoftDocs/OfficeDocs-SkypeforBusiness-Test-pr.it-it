---
title: Approve-CsDeviceUpdateRule
TOCTitle: Approve-CsDeviceUpdateRule
ms:assetid: d82e0494-4868-4d13-ac03-e5a5d0f2380e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398949(v=OCS.15)
ms:contentKeyID: 49302153
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Approve-CsDeviceUpdateRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Approva una regola di aggiornamento dispositivi importata nel sistema. Dopo l'approvazione di una regola di aggiornamento dispositivi, l'aggiornamento corrispondente verrà scaricato e installato automaticamente dai dispositivi client interessati dall'aggiornamento. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Approve-CsDeviceUpdateRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Approve-CsDeviceUpdateRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 approva la regola di aggiornamento dispositivi d5ce3c10-2588-420a-82ac-dc2d9b1222ff9 presente nel servizio WebServer:atl-cs-001.litwareinc.com.

    Approve-CsDeviceUpdateRule -Identity service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9

## ESEMPIO 2

Nell'esempio 2 vengono approvate tutte le regole di aggiornamento dispositivi configurate per il servizio WebServer:atl-cs-001.litwareinc.com. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsDeviceUpdateRule** con il parametro Filter. Il valore di filtro "service:WebServer:atl-cs-001.litwareinc.com\*" garantisce che vengano restituite solo le regole con un valore Identity che inizia con il valore stringa "service:WebServer:atl-cs-001.litwareinc.com". Per definizione, si tratta di tutte le regole di aggiornamento dispositivi assegnate al servizio WebServer:atl-cs-001.litwareinc.com. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Approve-CsDeviceUpdateRule**, che approva ogni regola presente nella raccolta.

    Get-CsDeviceUpdateRule -Filter service:WebServer:atl-cs-001.litwareinc.com* | Approve-CsDeviceUpdateRule

## ESEMPIO 3

Il comando mostrato nell'esempio 3 approva tutte le regole di aggiornamento dispositivi per la marca specificata (LG-Nortel). A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsDeviceUpdateRule** per restituire una raccolta di tutte le regole di aggiornamento dispositivi attualmente in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le regole in cui la proprietà Brand è uguale a LG-Nortel. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Approve-CsDeviceUpdateRule**, che approva ogni regola presente nella raccolta.

    Get-CsDeviceUpdateRule | Where-Object {$_.Brand -eq "LG-Nortel"} | Approve-CsDeviceUpdateRule

## Descrizione dettagliata

In Lync Server le regole di aggiornamento dispositivi vengono utilizzate per fornire aggiornamenti del firmware per i dispositivi in cui è in esecuzione Lync Phone Edition. Gli amministratori periodicamente caricano un insieme di regole di aggiornamento dispositivi in Lync Server. Una volta verificate e approvate, tali regole vengono scaricate e applicate automaticamente ai dispositivi appropriati non appena tali dispositivi si connettono al sistema. Per impostazione predefinita, i dispositivi verificano l'eventuale presenza di nuove regole di aggiornamento ogni volta che vengono accesi e si connettono a Lync Server. Dopo tale accesso iniziale, i dispositivi verificano inoltre l'esistenza di aggiornamenti ogni 24 ore.

Ogni nuova regola di aggiornamento dispositivi aggiunta al sistema viene contrassegnata come "In sospeso". Ciò significa che l'aggiornamento verrà scaricato e installato dai dispositivi di test appropriati ma che non verrà scaricato e installato dai dispositivi client in generale. In questo modo sarà possibile verificare gli aggiornamenti e garantire che non vi siano effetti negativi prima di rendere l'aggiornamento ampiamente disponibile. Quando si è certi che l'aggiornamento abbia superato i test effettuati e funzioni all'interno dell'organizzazione, è possibile utilizzare il cmdlet **Approve-CsDeviceUpdateRule** per approvarlo.

Dopo aver approvato un aggiornamento, il valore di PendingVersion della regola di aggiornamento associata viene assegnato ad ApprovedVersion e la proprietà PendingVersion viene cancellata. Si supponga, ad esempio, che il valore di PendingVersion di una nuova regola di aggiornamento sia versione 1.0.0.1. Dopo aver eseguito il cmdlet **Approve-CsDeviceUpdateRule**, PendingVersion verrà impostato su un valore NULL e ApprovedVersion verrà impostato su 1.0.0.1. Al successivo accesso, il dispositivo client verificherà automaticamente la disponibilità di aggiornamenti recentemente approvati a esso applicabili. Se presenti, l'aggiornamento verrà scaricato e installato automaticamente.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Approve-CsDeviceUpdateRule** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per la regola di aggiornamento dispositivi da approvare. L'identità di una regola di aggiornamento dispositivi è composta da due parti: il servizio in cui la regola di aggiornamento dispositivi è stata assegnata, ad esempio service:WebServer:atl-cs-001.litwareinc.com, e un identificatore univoco globale (GUID). Di conseguenza, una regola di aggiornamento dispositivi configurata per il sito Redmond avrà un parametro Identity simile al seguente: service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto DeviceUpdate.Rule</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdate.Rule. Il cmdlet **Approve-CsDeviceUpdateRule** accetta istanze da pipeline dell'oggetto regola di aggiornamento dispositivi.

## Tipi restituiti

Nessuno. Il cmdlet **Approve-CsDeviceUpdateRule** approva piuttosto le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdate.Rule.

## Vedere anche

#### Ulteriori risorse

[Get-CsDeviceUpdateRule](get-csdeviceupdaterule.md)  
[Remove-CsDeviceUpdateRule](remove-csdeviceupdaterule.md)  
[Reset-CsDeviceUpdateRule](reset-csdeviceupdaterule.md)  
[Restore-CsDeviceUpdateRule](restore-csdeviceupdaterule.md)

