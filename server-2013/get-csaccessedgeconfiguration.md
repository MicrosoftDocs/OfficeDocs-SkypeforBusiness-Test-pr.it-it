---
title: Get-CsAccessEdgeConfiguration
TOCTitle: Get-CsAccessEdgeConfiguration
ms:assetid: 75a8a7e9-728f-4abd-87e9-593713ae39ee
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398574(v=OCS.15)
ms:contentKeyID: 49301005
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAccessEdgeConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle impostazioni di configurazione per i computer che eseguono il servizio Access Edge nell'organizzazione (noti anche come Access Edge Server). Gli Access Edge Server consentono agli utenti al di fuori della rete interna di comunicare con gli utenti all'interno di tale rete. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsAccessEdgeConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsAccessEdgeConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene illustrato l'utilizzo di base del cmdlet **Get-CsAccessEdgeConfiguration**: se si chiama il cmdlet senza alcun parametro, vengono restituiti tutti i valori delle proprietà per l'implementazione degli Access Edge Server. Si noti che non è necessario includere il parametro Identity o Filter, poiché esiste un solo insieme di dati di configurazione degli Access Edge Server.

    Get-CsAccessEdgeConfiguration

## ESEMPIO 2

Nell'esempio 2 vengono restituiti solo tre valori di proprietà per la configurazione degli Access Edge Server, ovvero AllowAnonymousUsers, AllowFederatedUsers e AllowOutsideUsers. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsAccessEdgeConfiguration** per restituire tutti i valori delle proprietà degli Access Edge Server. Tali informazioni vengono quindi inviate tramite pipe al cmdlet **Select-Object**, che seleziona solo le proprietà che iniziano con il valore stringa "Allow". Questi valori sono gli unici valori delle proprietà visualizzati.

    Get-CsAccessEdgeConfiguration | Select-Object Allow*

## ESEMPIO 3

Il comando riportato nell'esempio 3 restituisce il valore di una singola proprietà di configurazione degli Access Edge Server: EnablePartnerDiscovery. A tale scopo, viene chiamato innanzitutto il cmdlet **Get-CsAccessEdgeConfiguration** per ottenere tutti i valori delle proprietà di configurazione degli Access Edge Server. La chiamata al cmdlet **Get-CsAccessEdgeConfiguration** è racchiusa tra parentesi. In questo modo Windows PowerShell esegue questo comando prima di qualsiasi altra operazione. Dopo aver ottenuto tutti i valori delle proprietà, viene utilizzata la "notazione del punto" standard (nome dell'oggetto seguito da un punto seguito dal nome della proprietà) per visualizzare il valore di una singola proprietà, ovvero EnablePartnerDiscovery.

    (Get-CsAccessEdgeConfiguration).EnablePartnerDiscovery

## Descrizione dettagliata

Gli Access Edge Server (noti anche come server proxy di accesso) consentono di estendere le funzionalità di Lync Server a persone non connesse alla rete interna. Ad esempio, nel caso di utenti remoti, vale a dire utenti autenticati che accedono a Lync Server tramite Internet anziché tramite la rete interna, sarà necessario configurare un Access Edge Server. Gli Edge Server sono inoltre necessari se si desidera stabilire una federazione con un'altra organizzazione oppure se si desidera concedere ai propri utenti il diritto di comunicare con persone che hanno i propri account presso un servizio di messaggistica istantanea pubblico, come Yahoo\!, AOL o MSN. Gli Access Edge Server risiedono sulla rete perimetrale e vengono utilizzati per stabilire e convalidare le connessioni SIP tra utenti che si trovano all'interno e all'esterno della rete interna.

In Lync Server gli Access Edge Server vengono gestiti utilizzando un'unica raccolta globale di impostazioni di configurazione. Il cmdlet **Get-CsAccessEdgeConfiguration** consente di ottenere le informazioni relative a queste impostazioni globali. Si noti che i valori delle proprietà restituiti dal cmdlet **Get-CsAccessEdgeConfiguration** variano a seconda del tipo di routing configurato per i server perimetrali. Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet **Set-CsAccessEdgeConfiguration**.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsAccessEdgeConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAccessEdgeConfiguration"}

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
<td><p>Consente di utilizzare i caratteri jolly per specificare le impostazioni di configurazione degli Access Edge Server da ottenere. Poiché esiste una sola istanza globale di queste impostazioni, il parametro Filter non è necessario. Tuttavia, se lo si preferisce, è possibile utilizzare una sintassi simile alla seguente per recuperare le impostazioni globali: -Identity &quot;g*&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni di configurazione dell'Access Edge Server da ottenere. Poiché può esistere una sola istanza globale di queste impostazioni, non è necessario includere il parametro Identity quando si chiama il cmdlet <strong>Get-CsAccessEdgeConfiguration</strong>. È tuttavia, possibile utilizzare la sintassi seguente per recuperare le impostazioni globali: -Identity global.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati di configurazione di Access Edge Server dalla copia locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsAccessEdgeConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsAccessEdgeConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayAccessEdgeSettingsDnsSrvRouting o dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayAccessEdgeSettingsDefaultRoute.

## Vedere anche

#### Ulteriori risorse

[Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)

