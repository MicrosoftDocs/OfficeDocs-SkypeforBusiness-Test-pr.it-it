---
title: Reset-CsDeviceUpdateRule
TOCTitle: Reset-CsDeviceUpdateRule
ms:assetid: 0de47bcf-da8f-4dae-b293-3adac3c1acdb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398181(v=OCS.15)
ms:contentKeyID: 49299675
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Reset-CsDeviceUpdateRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rifiuta una regola di aggiornamento dei dispositivi importata nel sistema. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Reset-CsDeviceUpdateRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Reset-CsDeviceUpdateRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di ripristinare la regola di aggiornamento dei dispositivi d5ce3c10-2588-420a-82ac-dc2d9b1222ff9 trovata nel servizio WebServer:atl-cs-001.litwareinc.com.

    Reset-CsDeviceUpdateRule -Identity service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9

## ESEMPIO 2

Nell'esempio 2 vengono reimpostate tutte le regole di aggiornamento dei dispositivi configurate per il servizio WebServer:atl-cs-001.litwareinc.com. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsDeviceUpdateRule** con il parametro Filter con valore "WebServer:atl-cs-001.litwareinc.com\*" per restituire solo le regole la cui identità (Identity) inizia con la stringa "WebServer:atl-cs-001.litwareinc.com". Per definizione, si tratta di tutte le regole di aggiornamento dei dispositivi assegnate al servizio WebServer:atl-cs-001.litwareinc.com. Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Reset-CsDeviceUpdateRule**, che reimposta tutte le regole della raccolta.

    Get-CsDeviceUpdateRule -Filter service:WebServer:atl-cs-001.litwareinc.com*  | Reset-CsDeviceUpdateRule

## ESEMPIO 3

Il comando riportato nell'esempio 3 reimposta tutte le regole di aggiornamento dei dispositivi per la marca LG-Nortel. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsDeviceUpdateRule** senza alcun parametro per restituire una raccolta di tutte le regole di aggiornamento dei dispositivi attualmente in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le regole in cui la proprietà Brand è uguale a LG-Nortel. A questo punto, la raccolta filtrata viene inviata tramite pipe al cmdlet **Reset-CsDeviceUpdateRule**, che reimposta tutte le regole incluse nella raccolta filtrata.

    Get-CsDeviceUpdateRule | Where-Object {$_.Brand -eq "LG-Nortel"} | Reset-CsDeviceUpdateRule

## Descrizione dettagliata

Lync Server utilizza le regole di aggiornamento dei dispositivi per fornire gli aggiornamenti firmware ai dispositivi che eseguono Lync Phone Edition. Gli amministratori caricano periodicamente un insieme di regole di aggiornamento dei dispositivi in Lync Server. Dopo la verifica e l'approvazione, queste regole vengono scaricate e applicate automaticamente ai dispositivi appropriati non appena questi si collegano al sistema. Per impostazione predefinita, i dispositivi verificano la disponibilità di nuove regole di aggiornamento ogni volta che vengono accesi e si connettono a Lync Server. Dopo l'accesso iniziale, i dispositivi verificano inoltre la disponibilità di aggiornamenti ogni 24 ore.

Ogni nuova regola di aggiornamento dei dispositivi aggiunta al sistema viene contrassegnata come "In sospeso". Ciò significa che l'aggiornamento verrà scaricato e installato dai dispositivi di test appropriati, tuttavia non verrà scaricato e installato dai dispositivi client in generale. In questo modo è possibile testare gli aggiornamenti e verificare che non presentino problemi prima di distribuirli a tutti i dispositivi interessati. Subito dopo avere verificato che l'aggiornamento ha superato i test e funzionerà senza problemi nell'organizzazione, è possibile utilizzare il cmdlet **Approve-CsDeviceUpdateRule** per approvarlo.

Tuttavia, può anche accadere che gli amministratori decidano di non utilizzare un dato aggiornamento nell'organizzazione, perché, ad esempio, potrebbe provocare un conflitto con il software locale. In questo caso, gli amministratori possono utilizzare il cmdlet **Reset-CsDeviceUpdateRule** per rifiutare l'aggiornamento. Quando ciò accade, la proprietà PendingVersion della regola di aggiornamento viene impostata su un valore nullo. Di conseguenza, i dispositivi di test che accedono al sistema eseguiranno la disinstallazione dell'aggiornamento e reinstalleranno la sua versione approvata. Poiché l'aggiornamento non è mai stato approvato, non verrà mai installato su alcun dispositivo ad eccezione dei dispositivi di test e ciò significa che non avrà alcun impatto sugli utenti.

Il cmdlet **Reset-CsDeviceUpdateRule** può essere utilizzato solo per le regole di aggiornamento dei dispositivi con stato In sospeso. Se una regola è già stata approvata, sarà necessario utilizzare il cmdlet **Restore-CsDeviceUpdateRule** per annullare la distribuzione dell'aggiornamento ai dispositivi.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Reset-CsDeviceUpdateRule** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Reset-CsDeviceUpdateRule"}

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
<td><p>Consente di evitare la visualizzazione di prompt di conferma o messaggi di errore non irreversibile che possono verificarsi quando si esegue il cmdlet.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco della regola di aggiornamento dei dispositivi da ripristinare. L'identità di una regola di aggiornamento dei dispositivi consta di due parti: il servizio a cui è stata assegnata la regola di aggiornamento dei dispositivi (ad esempio, service:WebServer:atl-cs-001.litwareinc.com) e un identificatore univoco globale (GUID). Di conseguenza, una regola di aggiornamento dei dispositivi configurata per il sito Redmond avrà un'identità simile alla seguente: &quot;service:WebServer:atl-cs-oo1.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>DeviceUpdate.Rule</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdate.Rule. Il cmdlet **Reset-CsDeviceUpdateRule** accetta le istanze dell'oggetto regola di aggiornamento dei dispositivi inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Reset-CsDeviceUpdateRule** reimposta le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdate.Rule.

## Vedere anche

#### Ulteriori risorse

[Approve-CsDeviceUpdateRule](approve-csdeviceupdaterule.md)  
[Get-CsDeviceUpdateRule](get-csdeviceupdaterule.md)  
[Remove-CsDeviceUpdateRule](remove-csdeviceupdaterule.md)  
[Restore-CsDeviceUpdateRule](restore-csdeviceupdaterule.md)

