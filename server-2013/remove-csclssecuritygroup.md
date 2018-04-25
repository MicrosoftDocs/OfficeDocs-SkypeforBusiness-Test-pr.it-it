---
title: Remove-CsClsSecurityGroup
TOCTitle: Remove-CsClsSecurityGroup
ms:assetid: 67778239-9338-4717-abeb-8b87e8cb7a9a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204958(v=OCS.15)
ms:contentKeyID: 49300827
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsClsSecurityGroup

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un gruppo di sicurezza di configurazione della registrazione centralizzata. La registrazione centralizzata consente agli amministratori di abilitare o disabilitare simultaneamente la registrazione degli eventi in più computer. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsClsSecurityGroup -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 elimina il gruppo di sicurezza della registrazione centralizzata con identità (Identity) global/HelpDesk.

    Remove-CsClsSecurityGroup -Identity "global/HelpDesk"

## Esempio 2

Nell'esempio 2 vengono eliminati tutti i gruppi di sicurezza della registrazione centralizzata attualmente in uso nell'organizzazione. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsClsSecurityGroup** senza parametri in modo da restituire una raccolta di tutti i gruppi di sicurezza della registrazione centralizzata. La raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsClsSecurityGroup**, che elimina ogni gruppo della raccolta.

    Get-CsClsSecurityGroup | Remove-CsClsSecurityGroup

## Esempio 3

Nell'esempio 3 viene illustrato come eliminare tutti i gruppi di sicurezza della registrazione centralizzata con livello di accesso RedmondSupport. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsClsSecurityGroup** per restituire una raccolta di tutti i gruppi di sicurezza della registrazione centralizzata. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i gruppi in cui la proprietà AccessLevel è impostata su Tier3. Questi gruppi vengono a loro volta inviati tramite pipe al cmdlet **Remove-CsClsSecurityGroup**, che li rimuove.

    Get-CsClsSecurityGroup | Where-Object {$_.AccessLevel -eq "Tier3"} | Remove-CsClsSecurityGroup

## Descrizione dettagliata

Il servizio di registrazione centralizzata, che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010, consente agli amministratori di gestire le funzioni di registrazione e traccia per tutti i computer e i pool che eseguono Microsoft Lync Server 2013. Il servizio consente infatti di interrompere, avviare e configurare la registrazione per uno o più pool e computer con un solo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del servizio Rubrica in tutti i server della Rubrica. Questa procedura non è invece eseguibile con gli strumenti OCSLogger e OCSTracer, che devono essere gestiti singolarmente (e anche arrestati e avviati singolarmente) in ogni server. Il servizio di registrazione centralizzata inoltre consente agli amministratori di eseguire ricerche nei log di traccia dal comando utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

Con Skype for Business online, i gruppi di sicurezza vengono utilizzati per determinare quali utenti hanno accesso alle informazioni che consentono l'identificazione personale dell'utente scritte nei file di log. I gruppi di sicurezza vengono creati utilizzando il cmdlet [New-CsClsSecurityGroup](new-csclssecuritygroup.md) e vengono quindi aggiunti a una raccolta di impostazioni di configurazione della registrazione centralizzata. Questi gruppi possono essere successivamente rimossi utilizzando il cmdlet **Remove-CsClsSecurityGroup**.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli del controllo di accesso basato sui ruoli creati personalmente), al prompt di Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsClsSecurityGroup"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Remove-CsClsSecurityGroup** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Identificatore univoco del gruppo di sicurezza della registrazione centralizzata da rimuovere. L'identità di un gruppo di sicurezza è costituita dell'ambito in cui è stato creato il gruppo seguito dal nome del gruppo. Per rimuovere ad esempio un gruppo denominato HelpDesk creato nell'ambito globale, utilizzare la sintassi seguente:</p>
<p>-Identity &quot;global/HelpDesk&quot;</p></td>
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

Il cmdlet **Remove-CsClsSecurityGroup** accetta istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.SecurityGroup\#Decorated inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsClsSecurityGroup** invece elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.SecurityGroup\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsClsSecurityGroup](get-csclssecuritygroup.md)  
[New-CsClsSecurityGroup](new-csclssecuritygroup.md)  
[Set-CsClsSecurityGroup](set-csclssecuritygroup.md)

