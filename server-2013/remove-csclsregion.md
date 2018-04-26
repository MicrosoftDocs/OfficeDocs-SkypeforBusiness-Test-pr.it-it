---
title: Remove-CsClsRegion
TOCTitle: Remove-CsClsRegion
ms:assetid: 6ab1596e-0e27-44e7-8cbc-efd4064ba58b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204971(v=OCS.15)
ms:contentKeyID: 49300873
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsClsRegion

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una o più aree di configurazione della registrazione centralizzata. La registrazione centralizzata consente agli amministratori di abilitare o disabilitare simultaneamente la registrazione degli eventi in più computer. Le aree di registrazione centralizzata devono essere utilizzate con Skype for Business online.

Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsClsRegion -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 rimuove l'area della registrazione centralizzata con identità (Identity) global/US.

    Remove-CsClsRegion -Identity "global/US"

## Esempio 2

Nell'esempio 2 vengono rimosse tutte le aree della registrazione centralizzata configurate nell'ambito globale. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsClsRegion** insieme al parametro Filter. Il valore di filtro "global/\*" restituisce solo i dati relativi alle aree configurate nell'ambito globale. Queste aree vengono quindi inviate tramite pipe al cmdlet **Remove-CsClsRegion**, che le elimina.

    Get-CsClsRegion -Filter "global/*" | Remove-CsClsRegion 

## Esempio 3

Nell'esempio 3 vengono eliminate tutte le aree della registrazione centralizzata con suffisso di gruppo di sicurezza EMEA. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsClsRegion** senza parametri. In questo modo viene restituita una raccolta di tutte le aree della registrazione centralizzata configurate per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet Where-Object, che seleziona solo le aree in cui la proprietà SecurityGroupSuffix è uguale a (-eq) EMEA. La sottoraccolta di aree viene quindi inviata tramite pipe al cmdlet **Remove-CsClsRegion**, che elimina ogni area della sottoraccolta.

    Get-CsClsRegion | Where-Object {$_.SecurityGroupSuffix -eq "EMEA" | Remove-CsClsRegion

## Descrizione dettagliata

Il servizio di registrazione centralizzata, che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010, consente agli amministratori di gestire la registrazione e la traccia per tutti i computer e i pool che eseguono Skype for Business online. La registrazione centralizzata consente agli amministratori di arrestare, avviare e configurare la registrazione per uno o più pool e computer utilizzando un solo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del servizio Rubrica in tutti i server della Rubrica. Questo comportamento è diverso rispetto agli strumenti OCSLogger e OCSTracer, che devono essere gestiti singolarmente (avviati e arrestati individualmente) in ogni server. Il servizio di registrazione centralizzata inoltre consente agli amministratori di eseguire ricerche nei log di traccia dal comando utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

Con Skype for Business online, le aree vengono utilizzate per determinare quali utenti hanno accesso alle informazioni che consentono l'identificazione personale dell'utente scritte nei file di log. Le aree vengono create utilizzando il cmdlet [New-CsClsRegion](new-csclsregion.md) e vengono quindi aggiunte a una raccolta di impostazioni di configurazione della registrazione centralizzata. Le aree aggiunte a una di queste raccolte possono essere successivamente rimosse utilizzando il cmdlet **Remove-CsClsRegion**.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli del controllo di accesso basato sui ruoli creati personalmente), al prompt di Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsClsRegion"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Remove-CsClsRegion** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Identificatore univoco dell'area di registrazione centralizzata da rimuovere. L'identità di un'area è costituita dall'ambito in cui è stata creata l'area seguito dal nome dell'area. Per eliminare ad esempio un'area denominata US creata nell'ambito globale, utilizzare la sintassi seguente:</p>
<p>-Identity &quot;global/US&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Remove-CsClsRegion** accetta istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Region\#Decorated inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsClsRegion** invece elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Region\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsClsRegion](get-csclsregion.md)  
[New-CsClsRegion](new-csclsregion.md)  
[Set-CsClsRegion](set-csclsregion.md)

