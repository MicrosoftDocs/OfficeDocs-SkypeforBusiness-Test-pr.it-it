---
title: Set-CsClsRegion
TOCTitle: Set-CsClsRegion
ms:assetid: 2599cae9-edef-408f-8987-313c67bfe763
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204746(v=OCS.15)
ms:contentKeyID: 49299952
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClsRegion

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un'area di configurazione esistente della registrazione centralizzata. La registrazione centralizzata consente agli amministratori di abilitare o disabilitare simultaneamente la registrazione degli eventi in più computer. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsClsRegion [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsClsRegion [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-OtherRegionAccess <String>] [-SecurityGroupSuffix <String>] [-Sites <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 cambia il suffisso del gruppo di sicurezza dell'area global/US in USSupport.

    Set-CsClsRegion -Identity "global/US" -SecurityGroupSuffix "USSupport"

## Descrizione dettagliata

Il servizio di registrazione centralizzata, che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010, consente agli amministratori di gestire la registrazione e la traccia per tutti i computer e i pool che eseguono Lync Server 2013. La registrazione centralizzata consente agli amministratori di arrestare, avviare e configurare la registrazione per uno o più pool e computer utilizzando un solo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del Servizio Rubrica in tutti i server della Rubrica. Questo comportamento è diverso rispetto agli strumenti OCSLogger e OCSTracer, che devono essere gestiti singolarmente (avviati e arrestati individualmente) in ogni server. Il servizio di registrazione centralizzata inoltre consente agli amministratori di eseguire ricerche nei log di traccia dal comando utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

Con Skype for Business online, le aree vengono utilizzate per determinare quali utenti hanno accesso alle informazioni che consentono l'identificazione personale dell'utente scritte nei file di log. Le aree vengono create utilizzando il cmdlet [New-CsClsRegion](new-csclsregion.md) e vengono quindi aggiunte a una raccolta di impostazioni di configurazione della registrazione centralizzata. Dopo la creazione delle aree, è possibile modificarne le proprietà utilizzando il cmdlet **Set-CsClsRegion**.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsClsRegion"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Set-CsClsRegion** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco dell'area. Le identità di area sono costituite dall'ambito di configurazione della registrazione centralizzata in cui è stata creata l'area e da un nome di area univoco. Per fare riferimento ad esempio a un'area globale denominata Redmond, utilizzare la sintassi seguente:</p>
<p>-Identity &quot;global/Redmond&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Consente di passare un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>OtherRegionAccess</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di un'area aggiuntiva a cui possono accedere utenti autorizzati per l'area.</p></td>
</tr>
<tr class="even">
<td><p><em>SecurityGroupSuffix</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Suffisso da aggiungere alla fine del nome di un gruppo di sicurezza autorizzato per l'area.</p></td>
</tr>
<tr class="odd">
<td><p><em>Sites</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Siti contenuti in questa area. Corrispondono ai valori dell'attributo SideId nel documento della topologia.</p></td>
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

Il cmdlet **Set-CsClsRegion** accetta le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Region\#Decorated inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsClsRegion** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Region\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsClsRegion](get-csclsregion.md)  
[New-CsClsRegion](new-csclsregion.md)  
[Remove-CsClsRegion](remove-csclsregion.md)

