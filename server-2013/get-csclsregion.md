---
title: Get-CsClsRegion
TOCTitle: Get-CsClsRegion
ms:assetid: 4f38e966-8e92-4549-8124-097c236c0165
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204879(v=OCS.15)
ms:contentKeyID: 49300540
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClsRegion

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle aree di configurazione della registrazione centralizzata in uso nell'organizzazione. La registrazione centralizzata consente agli amministratori di abilitare o disabilitare la traccia eventi in più computer contemporaneamente. Le aree di registrazione centralizzata possono essere utilizzate con Skype for Business online.

Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsClsRegion [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsClsRegion [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce informazioni su tutte le aree di registrazione centralizzata configurate per l'utilizzo nell'organizzazione.

    Get-CsClsRegion

## Esempio 2

Nell'esempio 2 vengono restituite solo le informazioni sull'area di registrazione centralizzata con identità (Identity) global/US.

    Get-CsClsRegion -Identity "global/US"

## Esempio 3

Nell'esempio 3 vengono restituite informazioni su tutte le aree di registrazione centralizzata configurate nell'ambito globale. A tale scopo, viene chiamato il cmdlet **Get-CsClsRegion** con il parametro Filter. Il valore di filtro "global/\*" restituisce solo i dati relativi alle aree configurate nell'ambito globale.

    Get-CsClsRegion -Filter "global/*"

## Esempio 4

Il comando riportato nell'esempio 4 restituisce informazioni su tutte le aree di registrazione centralizzata che consentono all'area Europe di accedere. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsClsRegion** per restituire una raccolta di tutte le aree di registrazione centralizzata attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le aree in cui la proprietà OtherRegionAccess include il valore stringa "Europe".

    Get-CsClsRegion | Where-Object {$_.OtherRegionAccess -match "Europe"}

## Descrizione dettagliata

Il servizio di registrazione centralizzata, che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010, consente agli amministratori di gestire la registrazione e la traccia per tutti i computer e i pool che eseguono Lync Server 2013. La registrazione centralizzata consente agli amministratori di arrestare, avviare e configurare la registrazione per uno o più pool e computer utilizzando un solo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del Servizio Rubrica in tutti i server della Rubrica. Questo comportamento è diverso rispetto agli strumenti OCSLogger e OCSTracer, che devono essere gestiti singolarmente (avviati e arrestati individualmente) in ogni server. Il servizio di registrazione centralizzata inoltre consente agli amministratori di eseguire ricerche nei log di traccia dal comando utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

Con la versione Office 365 di Lync Server, le aree vengono utilizzate per determinare quali utenti hanno accesso alle informazioni che consentono l'identificazione personale dell'utente scritte nei file di log. Le aree vengono create utilizzando il cmdlet [New-CsClsRegion](new-csclsregion.md) e vengono quindi aggiunte a una raccolta di impostazioni di configurazione della registrazione centralizzata. È possibile restituire informazioni sulle aree di registrazione centralizzata utilizzando il cmdlet **Get-CsClsRegion**.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClsRegion"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsClsRegion** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Consente di utilizzare i caratteri jolly per restituire una o più aree di registrazione centralizzata. Per restituire ad esempio una raccolta di tutte le impostazioni configurate nell'ambito globale, utilizzare la sintassi seguente:</p>
<p>-Filter &quot;global/*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco dell'area di registrazione centralizzata da restituire. L'identità di un'area è costituita dall'ambito in cui è stata creata l'area seguito dal nome dell'area. Per restituire ad esempio un'area denominata US creata nell'ambito globale, utilizzare la sintassi seguente:</p>
<p>-Identity &quot;global/US&quot;</p>
<p>Se non si specifica questo parametro, il cmdlet <strong>Get-CsClsRegion</strong> restituirà informazioni su tutte le aree di registrazione centralizzata.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione della registrazione centralizzata dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsClsRegion** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsClsRegion** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Region\#Decorated.

## Vedere anche

#### Ulteriori risorse

[New-CsClsRegion](new-csclsregion.md)  
[Remove-CsClsRegion](remove-csclsregion.md)  
[Set-CsClsRegion](set-csclsregion.md)

