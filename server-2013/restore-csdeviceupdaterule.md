---
title: Restore-CsDeviceUpdateRule
TOCTitle: Restore-CsDeviceUpdateRule
ms:assetid: 4c89d529-23fc-470e-9006-f15a18ed13fd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398305(v=OCS.15)
ms:contentKeyID: 49300482
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Restore-CsDeviceUpdateRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di eseguire il rollback di una regola di aggiornamento dei dispositivi approvata per l'utilizzo nell'organizzazione. Quando si ripristina una regola di aggiornamento dei dispositivi, la versione approvata della regola viene reimpostata in modo da riflettere l'aggiornamento che era in uso prima dell'approvazione della regola. A loro volta, i dispositivi client che accedono al sistema disinstallano automaticamente l'aggiornamento più recente e scaricano e reinstallano la versione precedente dell'aggiornamento. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Restore-CsDeviceUpdateRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Restore-CsDeviceUpdateRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di ripristinare la regola di aggiornamento dei dispositivi d5ce3c10-2588-420a-82ac-dc2d9b1222ff9 trovata nel servizio WebServer:atl-cs-001.litwareinc.com.

    Restore-CsDeviceUpdateRule -Identity service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9

## ESEMPIO 2

Nell'esempio 2 vengono ripristinate tutte le regole di aggiornamento dei dispositivi configurate per il servizio WebServer:atl-cs-001.litwareinc.com. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsDeviceUpdateRule** con il parametro Filter. Il valore di filtro "WebServer:atl-cs-001.litwareinc.com\*" restituisce solo le regole con l'identità che inizia con il valore stringa "WebServer:atl-cs-001.litwareinc.com". Per definizione, si tratta di tutte le regole di aggiornamento dei dispositivi assegnate al servizio WebServer:atl-cs-001.litwareinc.com. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Restore-CsDeviceUpdateRule**, che ripristina tutte le regole della raccolta.

    Get-CsDeviceUpdateRule -Filter service:WebServer:atl-cs-001.litwareinc.com* | Restore-CsDeviceUpdateRule

## ESEMPIO 3

Nell'esempio 3 viene illustrato come ripristinare tutte le regole di aggiornamento dei dispositivi per uno specifico marchio (LG-Nortel). A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsDeviceUpdateRule** senza alcun parametro per restituire una raccolta di tutte le regole di aggiornamento dei dispositivi attualmente in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le regole in cui la proprietà Brand è uguale a LG-Nortel. Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Restore-CsDeviceUpdateRule**, che ripristina ogni regola della raccolta filtrata.

    Get-CsDeviceUpdateRule | Where-Object {$_.Brand -eq "LG-Nortel"} | Restore-CsDeviceUpdateRule

## Descrizione dettagliata

Lync Server utilizza le regole di aggiornamento dei dispositivi per fornire gli aggiornamenti del firmware ai dispositivi in cui è installato Lync Phone Edition. Gli amministratori caricano periodicamente un insieme di regole di aggiornamento dei dispositivi in Lync Server. Dopo essere state testate e approvate, queste regole vengono automaticamente scaricate e applicate ai dispositivi appropriati quando questi si connettono al sistema. Per impostazione predefinita, i dispositivi verificano la disponibilità di nuove regole di aggiornamento tutte le volte che vengono accesi e si connettono a Lync Server. I dispositivi verificano la presenza di aggiornamenti anche ogni 24 ore dopo l'accesso iniziale.

Ogni nuova regola di aggiornamento dei dispositivi aggiunta al sistema viene contrassegnata come "In sospeso". Ciò significa che l'aggiornamento verrà scaricato e installato dai dispositivi di test appropriati. Non verrà tuttavia scaricato e installato dai dispositivi client in generale. Ciò consente di testare gli aggiornamenti e verificare che non presentino problemi prima di distribuirli a tutti i dispositivi interessati. Non appena verificato che l'aggiornamento ha superato i test e funzionerà senza problemi nell'organizzazione, è possibile utilizzare il cmdlet **Approve-CsDeviceUpdateRule** per approvarlo.

Quando si approva un aggiornamento, alla proprietà ApprovedVersion viene assegnato il valore della proprietà PendingVersion della regola di aggiornamento associata e la proprietà PendingVersion viene cancellata. Ad esempio, si supponga che la proprietà PendingVersion di una nuova regola di aggiornamento sia la versione 1.0.0.1. Dopo l'esecuzione del cmdlet **Approve-CsDeviceUpdateRule**, la proprietà PendingVersion verrà impostata su un valore nullo e la proprietà ApprovedVersion verrà impostata su 1.0.0.1. La volta successiva che un dispositivo client verificherà la presenza di aggiornamenti, l'aggiornamento verrà automaticamente scaricato e installato.

Inoltre, eventuali versioni precedenti dell'aggiornamento (ad esempio, la versione 1.0.0.0) vengono contrassegnate come RestoreVersion. Questa versione dell'aggiornamento resta sul sistema e viene utilizzata nel caso sia necessario eseguire il rollback del nuovo aggiornamento. Se si verificano dei problemi, gli amministratori possono utilizzare il cmdlet **Restore-CsDeviceUpdateRule** per eseguire il rollback dell'aggiornamento. In questo caso, la prossima volta che un dispositivo client verificherà la presenza di aggiornamenti disinstallerà automaticamente il nuovo aggiornamento (versione 1.0.0.1) e reinstallerà l'aggiornamento precedente (1.0.0.0).

Si noti che questo è possibile solo se è disponibile un aggiornamento precedente da reinstallare. Se così non fosse, l'aggiornamento di cui si deve eseguire il rollback verrà semplicemente disinstallato.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Restore-CsDeviceUpdateRule** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Restore-CsDeviceUpdateRule"}

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
<td><p>Identificatore univoco della regola di aggiornamento dei dispositivi da ripristinare. L'identità di una regola di aggiornamento dei dispositivi consta di due parti: il servizio a cui è stata assegnata la regola di aggiornamento dei dispositivi (ad esempio, service:WebServer:atl-cs-001.litwareinc.com) e un identificatore univoco globale (GUID). Di conseguenza, una regola di aggiornamento dei dispositivi configurata per il sito Redmond avrà un'identità simile alla seguente: service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdate.Rule. Il cmdlet **Restore-CsDeviceUpdateRule** accetta le istanze dell'oggetto regola di aggiornamento dei dispositivi inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Restore-CsDeviceUpdateRule** ripristina le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdate.Rule.

## Vedere anche

#### Ulteriori risorse

[Approve-CsDeviceUpdateRule](approve-csdeviceupdaterule.md)  
[Get-CsDeviceUpdateRule](get-csdeviceupdaterule.md)  
[Remove-CsDeviceUpdateRule](remove-csdeviceupdaterule.md)  
[Reset-CsDeviceUpdateRule](reset-csdeviceupdaterule.md)

