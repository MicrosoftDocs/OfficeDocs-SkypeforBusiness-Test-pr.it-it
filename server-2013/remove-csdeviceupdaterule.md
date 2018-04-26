---
title: Remove-CsDeviceUpdateRule
TOCTitle: Remove-CsDeviceUpdateRule
ms:assetid: 42b0bcd5-d567-4867-841e-0d35ac05c09f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425930(v=OCS.15)
ms:contentKeyID: 49300357
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsDeviceUpdateRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una regola di aggiornamento dei dispositivi configurata per l'utilizzo nell'organizzazione. Le regole di aggiornamento dei dispositivi consentono di associare gli aggiornamenti firmware ai dispositivi che eseguono Lync Phone Edition. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsDeviceUpdateRule -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene eliminata la regola di aggiornamento dei dispositivi con identità (Identity) service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9. Dopo l'eliminazione della regola, il corrispondente aggiornamento firmware non sarà più disponibile.

    Remove-CsDeviceUpdateRule -Identity service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9

## ESEMPIO 2

Il comando riportato nell'esempio 2 rimuove tutte le regole di aggiornamento dei dispositivi configurate per l'utilizzo nell'organizzazione. A tale scopo, viene chiamato il cmdlet **Get-CsDeviceUpdateRule** (senza alcun parametro) per restituire una raccolta di tutte le regole di aggiornamento dei dispositivi attualmente in uso. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsDeviceUpdateRule**, che a sua volta elimina ogni regola della raccolta.

    Get-CsDeviceUpdateRule | Remove-CsDeviceUpdateRule

## ESEMPIO 3

Nell'esempio 3 vengono rimosse tutte le regole di aggiornamento dei dispositivi importate per il servizio WebServer:atl-cs-001.litwareinc.com. A tale scopo, il comando innanzitutto utilizza il cmdlet **Get-CsDeviceUpdateRule** e il parametro Filter per recuperare tutte le regole di aggiornamento dei dispositivi la cui identità inizia con il valore stringa "service:WebServer:atl-cs-001.litwareinc.com". Questa raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsDeviceUpdateRule**, che elimina ogni regola della raccolta.

    Get-CsDeviceUpdateRule -Filter service:WebServer:atl-cs-001.litwareinc.com* | Remove-CsDeviceUpdateRule

## ESEMPIO 4

Nell'esempio 4 vengono eliminate tutte le regole di aggiornamento dei dispositivi nelle quali il parametro Brand è uguale a "LG-Nortel". A tale scopo, viene chiamato il cmdlet **Get-CsDeviceUpdateRule** senza alcun parametro per recuperare una raccolta di tutte le regole di aggiornamento dei dispositivi in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le regole nelle quali il parametro Brand è uguale a "LG-Nortel". Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsDeviceUpdateRule**, che elimina ogni regola della raccolta.

    Get-CsDeviceUpdateRule | Where-Object {$_.Brand -eq "LG-Nortel"} | Remove-CsDeviceUpdateRule

## Descrizione dettagliata

Lync Server utilizza le regole di aggiornamento dei dispositivi come strumento per fornire gli aggiornamenti firmware ai dispositivi che eseguono Lync Phone Edition. Gli amministratori caricano periodicamente un insieme di regole di aggiornamento dei dispositivi in Lync Server. Dopo essere state verificate e approvate, queste regole vengono scaricate e applicate automaticamente ai dispositivi appropriati non appena questi si connettono al sistema. Per impostazione predefinita, i dispositivi verificano la disponibilità di nuove regole di aggiornamento ogni volta che vengono accesi e si connettono a Lync Server. Dopo l'accesso iniziale, i dispositivi verificano inoltre la disponibilità di aggiornamenti ogni 24 ore.

Gli amministratori non possono creare proprie regole di aggiornamento dei dispositivi. Le regole di aggiornamento possono essere create solamente scaricando e importando set di regole dal sito Web Microsoft. Ciò significa che, nel tempo, vengono probabilmente raccolte regole non aggiornate o che non sono utili per l'organizzazione. Se ad esempio l'organizzazione non utilizza più telefoni LG-Nortel, gli aggiornamenti firmware per questi dispositivi non sono più necessari. Sebbene queste regole non necessarie non creino alcun problema, possono complicare l'amministrazione. L'esecuzione del cmdlet **Get-CsDeviceUpdateRule** per restituire una raccolta di tutte le regole di aggiornamento dei dispositivi può creare confusione se la maggior parte di queste regole non è poi effettivamente applicabile nell'organizzazione. Per semplificare l'amministrazione, è possibile utilizzare il cmdlet **Remove-CsDeviceUpdateRule** per rimuovere eventuali regole o set di regole di aggiornamento dei dispositivi importati per essere utilizzati.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Remove-CsDeviceUpdateRule** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsDeviceUpdateRule"}

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
<td><p>Identificatore univoco della regola di aggiornamento dei dispositivi. L'identità di una regola di aggiornamento dei dispositivi è composta di due parti: l'ambito del servizio nel quale la regola è stata applicata (ad esempio, service:WebServer:atl-cs-001.litwareinc.com) e l'identificatore univoco globale (GUID) preassegnato alla regola (ad esempio, d5ce3c10-2588-420a-82ac-dc2d9b1222ff9). Basata su queste norme, l'identità di una data regola di aggiornamento dei dispositivi sarà simile a: &quot;service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9&quot;.</p>
<p>I caratteri jolly non sono consentiti quando si specifica una identità.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdate.Rule. Il cmdlet **Remove-CsDeviceUpdateRule** accetta le istanze dell'oggetto regola di aggiornamento dei dispositivi inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Remove-CsDeviceUpdateRule** non restituisce oggetti o valori. Il cmdlet invece elimina le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.Rule.

## Vedere anche

#### Ulteriori risorse

[Approve-CsDeviceUpdateRule](approve-csdeviceupdaterule.md)  
[Get-CsDeviceUpdateRule](get-csdeviceupdaterule.md)  
[Reset-CsDeviceUpdateRule](reset-csdeviceupdaterule.md)  
[Restore-CsDeviceUpdateRule](restore-csdeviceupdaterule.md)

