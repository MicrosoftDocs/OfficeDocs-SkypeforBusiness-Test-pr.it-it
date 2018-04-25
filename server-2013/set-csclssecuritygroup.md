---
title: Set-CsClsSecurityGroup
TOCTitle: Set-CsClsSecurityGroup
ms:assetid: 14e7d927-8d3e-4b36-867c-d4742101e751
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204700(v=OCS.15)
ms:contentKeyID: 49299774
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClsSecurityGroup

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un gruppo di sicurezza di configurazione della registrazione centralizzata. La registrazione centralizzata consente agli amministratori di abilitare o disabilitare simultaneamente la registrazione degli eventi in più computer. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsClsSecurityGroup [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsClsSecurityGroup [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AccessLevel <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 modifica il gruppo di sicurezza della registrazione centralizzata con identità (Identity) global/HelpDesk. In questo esempio la proprietà AccessLevel è impostata su Tier3.

    Set-CsClsSecurityGroup -Identity "global/HelpDesk" -AccessLevel "Tier3"

## Esempio 2

Nell'esempio 2 viene modificato il livello di accesso per tutti i gruppi di sicurezza della registrazione centralizzata configurati nell'ambito globale. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsClsSecurityGroup** con il parametro Filter. Il valore di filtro "global/\*" restituisce solo i dati relativi ai gruppi di sicurezza configurati nell'ambito globale. Questi gruppi vengono quindi inviati tramite pipe al cmdlet **Set-CsClsSecurityGroup**, che imposta la proprietà AccessLevel di ogni gruppo su Tier3.

    Get-CsClsSecurityGroup -Filter "global/*" | Set-CsClsSecurityGroup-AccessLevel "Tier3"

## Esempio 3

Nell'esempio 3 viene illustrato come utilizzare un singolo comando per modificare il livello di accesso per tutti i gruppi di sicurezza della registrazione centralizzata che condividono un livello di accesso esistente. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsClsSecurityGroup** senza parametri in modo da restituire una raccolta di tutti i gruppi di sicurezza della registrazione centralizzata. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i gruppi con AccessLevel uguale a (-eq) GlobalAccess. Questi gruppi vengono a loro volta inviati tramite pipe al cmdlet **Set-CsClsSecurityGroup**, che seleziona ogni gruppo e modifica la proprietà AccessLevel impostandola su Tier3.

    Get-CsClsSecurityGroup | Where-Object {$_.AccessLevel -eq "GlobalAccess"} | Set-CsClsSecurityGroup -AccessLevel "Tier3"

## Descrizione dettagliata

Il servizio di registrazione centralizzata, che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010, consente agli amministratori di gestire la registrazione e la traccia per tutti i computer e i pool che eseguono Lync Server 2013. La registrazione centralizzata consente agli amministratori di arrestare, avviare e configurare la registrazione per uno o più pool e computer utilizzando un solo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del Servizio Rubrica in tutti i server della Rubrica. Questo comportamento è diverso rispetto agli strumenti OCSLogger e OCSTracer, che devono essere gestiti singolarmente (avviati e arrestati individualmente) in ogni server. Il servizio di registrazione centralizzata inoltre consente agli amministratori di eseguire ricerche nei log di traccia dal comando utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

Con la versione Office 365 di Lync Server, i gruppi di sicurezza vengono utilizzati per determinare quali utenti hanno accesso alle informazioni che consentono l'identificazione personale dell'utente scritte nei file di log. I gruppi di sicurezza vengono creati utilizzando il cmdlet [New-CsClsSecurityGroup](new-csclssecuritygroup.md) e vengono quindi aggiunti a una raccolta di impostazioni di configurazione della registrazione centralizzata. Dopo la creazione di questi gruppi, è possibile modificare i valori delle relative proprietà utilizzando il cmdlet **Set-CsClsSecurityGroup**.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt di Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsClsSecurityGroup"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Set-CsClsSecurityGroup** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>AccessLevel</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Valore stringa che specifica il livello di accesso assegnato al gruppo. I livelli di accesso sono assegnati dagli amministratori e utilizzati per classificare i gruppi di sicurezza, ad esempio:</p>
<p>-AccessLevel &quot;Tier3&quot;</p>
<p>Più gruppi possono condividere lo stesso livello di accesso. I soli valori ad avere attualmente significato sono &quot;Tier3&quot;, &quot;Tier2&quot;, &quot;Product&quot;, &quot;Ops&quot; e &quot;Pii&quot;.</p></td>
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
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco del gruppo di sicurezza della registrazione centralizzata da modificare. L'identità di un gruppo di sicurezza è costituita dell'ambito in cui è stato creato il gruppo seguito dal nome del gruppo. Per modificare ad esempio un gruppo denominato HelpDesk creato nell'ambito globale, utilizzare la sintassi seguente:</p>
<p>-Identity &quot;global/HelpDesk&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Consente di passare un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
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

Il cmdlet **Set-CsClsSecurityGroup** accetta le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.SecurityGroup\#Decorated inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsClsSecurityGroup** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.SecurityGroup\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsClsSecurityGroup](get-csclssecuritygroup.md)  
[New-CsClsSecurityGroup](new-csclssecuritygroup.md)  
[Remove-CsClsSecurityGroup](remove-csclssecuritygroup.md)

