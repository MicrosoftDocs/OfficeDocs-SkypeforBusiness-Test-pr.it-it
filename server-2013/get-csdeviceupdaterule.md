---
title: Get-CsDeviceUpdateRule
TOCTitle: Get-CsDeviceUpdateRule
ms:assetid: 14291802-a833-4f5f-8b4b-a465de6f7f2b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398215(v=OCS.15)
ms:contentKeyID: 49299764
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsDeviceUpdateRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle regole di aggiornamento dei dispositivi configurate per l'utilizzo nell'organizzazione. Le regole di aggiornamento dei dispositivi vengono utilizzate per associare aggiornamenti del firmware a dispositivi che eseguono Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsDeviceUpdateRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsDeviceUpdateRule [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Descrizione dettagliata

In Lync Server vengono utilizzate le regole di aggiornamento dei dispositivi per fornire aggiornamenti del firmware a dispositivi che eseguono Lync Phone Edition. Gli amministratori caricano periodicamente un insieme di regole di aggiornamento dei dispositivi in Lync Server. Dopo essere state verificate e approvate, queste regole vengono scaricate e applicate automaticamente ai dispositivi appropriati non appena tali dispositivi si connettono al sistema. Per impostazione predefinita, i dispositivi ricercano nuove regole di aggiornamento dei dispositivi ogni volta che vengono avviati e connessi a Lync Server. I dispositivi ricercano inoltre gli aggiornamenti ogni 24 ore dopo l'accesso iniziale.

Le regole di aggiornamento dei dispositivi possono essere importate nel servizio servizi Web e a esso applicate. Il cmdlet **Get-CsDeviceUpdateRule** consente di restituire informazioni sulle regole di aggiornamento dei dispositivi importate per l'utilizzo nell'organizzazione.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsDeviceUpdateRule** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsDeviceUpdateRule"}

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
<td><p>Consente l'utilizzo di caratteri jolly per specificare l'identità di una regola di aggiornamento del dispositivo o di una serie di regole. Ad esempio, per restituire tutte le regole di aggiornamento del dispositivo per WebServer:atl-cs-001.litwareinc.com, utilizzare il valore di filtro seguente: &quot;service:WebServer:atl-cs-001.litwareinc.com*&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>L'identità di una regola di aggiornamento dei dispositivi è composta di due parti: l'ambito del servizio nel quale la regola è stata applicata (ad esempio, service:WebServer:atl-cs-001.litwareinc.com) e l'identificatore univoco globale (GUID) preassegnato alla regola (ad esempio, d5ce3c10-2588-420a-82ac-dc2d9b1222ff9). In base a questi dati, l'identità di una data regola di aggiornamento sarà simile a quella seguente: &quot;service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9 &quot;.</p>
<p>I caratteri jolly non sono consentiti quando si specifica un valore Identity. Utilizzare il parametro Filter se si desidera utilizzare i caratteri jolly per specificare una regola.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati delle regole di aggiornamento dei dispositivi dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsDeviceUpdateRule** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsDeviceUpdateRule** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.DeviceUpdate.Rule.

## Esempi

## ESEMPIO 1

Il comando dell'esempio 1 restituisce le informazioni su tutte le regole di aggiornamento dei dispositivi applicate nell'organizzazione. Se si chiama il cmdlet **Get-CsDeviceUpdateRule** senza parametri aggiuntivi, verrà sempre restituita la raccolta completa di regole di aggiornamento dei dispositivi.

    Get-CsDeviceUpdateRule

## ESEMPIO 2

Il comando mostrato nell'esempio 2 restituisce le informazioni sulla regola di aggiornamento del dispositivo con identità "WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9".

    Get-CsDeviceUpdateRule -Identity service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9

## ESEMPIO 3

Nell'esempio 3 vengono restituite le informazioni su tutte le regole di aggiornamento del dispositivo, configurate per il servizio WebServer:atl-cs-001.litwareinc.com. Per eseguire questa attività, il parametro Filter viene utilizzato insieme al valore di filtro "WebServer:atl-cs-001.litwareinc.com\*". Questo filtro circoscrive i dati restituiti alle regole di aggiornamento dei dispositivi con valore Identity che inizia con il valore stringa "service:WebServer:atl-cs-001.litwareinc.com".

    Get-CsDeviceUpdateRule -Filter service:WebServer:atl-cs-001.litwareinc.com*

## ESEMPIO 4

Nell'esempio 4 vengono restituite tutte le regole di aggiornamento dei dispositivi con proprietà Brand uguale a "LG-Nortel". A tale scopo, viene chiamato il cmdlet **Get-CsDeviceUpdateRule** per restituire una raccolta di tutte le regole di aggiornamento dei dispositivi dell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona unicamente le regole con proprietà Brand uguale a "LG-Nortel".

    Get-CsDeviceUpdateRule | Where-Object {$_.Brand -eq "LG-Nortel"}

## ESEMPIO 5

Nell'esempio 5 viene restituita una raccolta di tutte le regole di aggiornamento dei dispositivi che non sono state approvate. A tale scopo, viene utilizzato il cmdlet **Get-CsDeviceUpdateRules** per restituire una raccolta di tutte le regole e quindi tale raccolta viene inviata tramite pipe al cmdlet **Where-Object**. A sua volta, il cmdlet **Where-Object** seleziona solo le regole con proprietà Approved uguale a un valore Null. Se la proprietà Approved è impostata su null, queste regole non sono approvate.

    Get-CsDeviceUpdateRule | Where-Object {$_.ApprovedVersion -eq $Null}

## ESEMPIO 6

Questo comando restituisce una raccolta di tutte le regole di aggiornamento dei dispositivi che soddisfano i due criteri seguenti: la regola è stata approvata ed è correlata ai dispositivi LG-Nortel. A tale scopo, viene chiamato innanzitutto il cmdlet **Get-CsDeviceUpdateRule** per restituire una raccolta di tutte le regole di aggiornamento dei dispositivi dell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che la filtra in base a due criteri: la proprietà Approved non deve essere impostata su null, ovvero deve presentare un valore di qualsiasi tipo, e la proprietà Brand deve essere uguale a "LG-Nortel".

    Get-CsDeviceUpdateRule | Where-Object {$_.ApprovedVersion -ne $Null -and $_.Brand -eq "LG-Nortel"}

## Vedere anche

#### Ulteriori risorse

[Approve-CsDeviceUpdateRule](approve-csdeviceupdaterule.md)  
[Remove-CsDeviceUpdateRule](remove-csdeviceupdaterule.md)  
[Reset-CsDeviceUpdateRule](reset-csdeviceupdaterule.md)  
[Restore-CsDeviceUpdateRule](restore-csdeviceupdaterule.md)

