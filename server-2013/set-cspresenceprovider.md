---
title: Set-CsPresenceProvider
TOCTitle: Set-CsPresenceProvider
ms:assetid: 3f2e30d1-edb5-4839-a24f-11b77b699a1d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204833(v=OCS.15)
ms:contentKeyID: 49300307
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPresenceProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un provider del servizio di presenza configurato per l'utilizzo nell'organizzazione. I provider di questo tipo rappresentano la proprietà PresenceProviders di una raccolta di impostazioni di configurazione di Servizi utente. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsPresenceProvider [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPresenceProvider [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

I comandi riportati nell'esempio 1 illustrano come utilizzare il cmdlet **Set-CsPresenceProvider** per modificare l'FQDN di un provider del servizio di presenza esistente. A tale scopo, il primo comando dell'esempio utilizza il cmdlet **Get-CsPresenceProvider** per creare un riferimento oggetto al provider del servizio di presenza con identità "global/contoso.com". Questo riferimento oggetto viene archiviato nella variabile $x.

Nel secondo comando la proprietà FQDN del riferimento oggetto viene impostata su contoso2.com, il nuovo FQDN del provider del servizio di presenza. Dopo la configurazione della proprietà FQDN, viene utilizzato il cmdlet **Set-CsPresenceProvider** insieme alla proprietà Instance per scrivere queste modifiche nella raccolta globale delle impostazioni di configurazione di Servizi utente.

    $x = Get-CsPresenceProvider -Identity "global/contoso.com" 
    $x.Fqdn = "contoso2.com"
    Set-CsPresenceProvider -Instance $x

## Descrizione dettagliata

I cmdlet **CsPresenceProvider** consentono di gestire la proprietà PresenceProviders inclusa nelle impostazioni di configurazione di Servizi utente. Queste impostazioni vengono utilizzate ad esempio per gestire le informazioni sulla presenza, inclusa una raccolta di provider del servizio di presenza autorizzati. La raccolta viene archiviata nella proprietà PresenceProviders.

Il cmdlet **Set-CsPresenceProvider** può essere utilizzato per modificare l'FQDN di un provider del servizio di presenza attualmente configurato per l'utilizzo nell'organizzazione.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPresenceProvider"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Set-CsPresenceProvider** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Identificatore univoco del provider del servizio di presenza da modificare. L'identità di un provider del servizio di presenza è costituita da due parti: l'ambito (parametro Parent) in cui è stata applicata la regola (ad esempio service:UserServer:atl-cs-001.litwareinc.com) e l'FQDN del provider. Per modificare un provider del servizio di presenza nell'ambito globale, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;global/fabrikam.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Set-CsPresenceProvider** accetta le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PresenceProvider\#Decorated inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsPresenceProvider** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PresenceProvider\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsPresenceProvider](get-cspresenceprovider.md)  
[Get-CsUserServicesConfiguration](get-csuserservicesconfiguration.md)  
[New-CsPresenceProvider](new-cspresenceprovider.md)  
[Remove-CsPresenceProvider](remove-cspresenceprovider.md)

