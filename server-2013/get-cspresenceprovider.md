---
title: Get-CsPresenceProvider
TOCTitle: Get-CsPresenceProvider
ms:assetid: 15f7a7d0-d6d6-491e-a2e3-04fd2d6528d5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204705(v=OCS.15)
ms:contentKeyID: 49299790
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPresenceProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui provider del servizio di presenza configurati per l'utilizzo nell'organizzazione. I provider di questo tipo rappresentano la proprietà PresenceProviders di una raccolta di impostazioni di configurazione di Servizi utente. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsPresenceProvider [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPresenceProvider [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce informazioni relative a tutti i provider del servizio di presenza configurati per l'utilizzo nell'organizzazione.

    Get-CsPresenceProvider

## Esempio 2

Nell'esempio 2 vengono restituite informazioni su un singolo provider del servizio di presenza, ovvero il provider con identità (Identity) global/fabrikam.com.

    Get-CsPresenceProvider -Identity "global/fabrikam.com"

## Esempio 3

Nell'esempio 3 vengono restituite informazioni su tutti i provider del servizio di presenza configurati nell'ambito del sito. Per ottenere questo risultato, viene utilizzato il parametro Filter con valore "site:\*". Questo valore di filtro restituisce solo i dati relativi ai provider del servizio di presenza con identità (Identity) che inizia con il valore stringa "site:".

    Get-CsPresenceProvider -Filter "site:*"

## Esempio 4

Nell'esempio 4 vengono restituiti tutti i provider del servizio di presenza con valore stringa "fabrikam.com" nella proprietà Fqdn. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsPresenceProvider** per restituire una raccolta di tutti i provider del servizio di presenza configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i provider la cui proprietà Fqdn include (-match) il valore stringa "fabrikam.com".

    Get-CsPresenceProvider | Where-Object {$_.Fqdn -match "fabrikam.com"}

## Descrizione dettagliata

I cmdlet **CsPresenceProvider** vengono utilizzati per gestire la proprietà PresenceProviders presente nelle impostazioni di configurazione di Servizi utente. Queste impostazioni vengono utilizzate ad esempio per gestire le informazioni sulla presenza, inclusa una raccolta di provider del servizio di presenza autorizzati. La raccolta viene archiviata nella proprietà PresenceProviders. Il cmdlet Get-CsPresenceProvider consente di restituire informazioni sui provider del servizio di presenza che sono stati autorizzati per l'utilizzo nell'organizzazione.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPresenceProvider"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsPresenceProvider** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Consente di utilizzare i caratteri jolly per specificare l'identità del o dei provider del servizio di presenza da restituire. Per restituire ad esempio tutti i provider del servizio di presenza configurati nell'ambito del servizio, utilizzare il valore di filtro seguente:</p>
<p>-Filter &quot;service:*&quot;</p>
<p>Non è possibile utilizzare i parametri Filter e Identity nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco del provider del servizio di presenza. L'identità di un provider del servizio di presenza è costituita da due parti: l'ambito (parametro Parent) in cui è stato applicato il provider (ad esempio service:UserServer:atl-cs-001.litwareinc.com) e il nome di dominio completo del provider. Per recuperare ad esempio un singolo provider del servizio di presenza, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;global/fabrikam.com&quot;</p>
<p>Per restituire tutti i provider del servizio di presenza per un elemento padre specifico, è sufficiente specificare l'ambito. La sintassi seguente ad esempio restituisce tutti i provider del servizio di presenza configurati per l'ambito globale:</p>
<p>-Identity &quot;global&quot;</p>
<p>Se non vengono inclusi né il parametro Identity né il parametro Filter, il cmdlet <strong>Get-CsPresenceProvider</strong> restituirà informazioni su tutti i provider.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i domini consentiti dalla replica locale dell'archivio di gestione centrale anziché direttamente dall'archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsPresenceProvider** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsPresenceProvider** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PresenceProvider\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsUserServicesConfiguration](get-csuserservicesconfiguration.md)  
[New-CsPresenceProvider](new-cspresenceprovider.md)  
[Remove-CsPresenceProvider](remove-cspresenceprovider.md)  
[Set-CsPresenceProvider](set-cspresenceprovider.md)

