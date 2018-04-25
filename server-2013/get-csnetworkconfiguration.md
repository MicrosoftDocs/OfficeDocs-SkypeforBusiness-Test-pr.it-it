---
title: Get-CsNetworkConfiguration
TOCTitle: Get-CsNetworkConfiguration
ms:assetid: 08bc8eca-b244-4d5e-b089-1cc95605ba14
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398140(v=OCS.15)
ms:contentKeyID: 49299604
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera le impostazioni globali del servizio Controllo di ammissione di chiamata, del servizio di chiamate di emergenza Enhanced 9-1-1 (E9-1-1) e del bypass multimediale. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsNetworkConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Con questo esempio viene recuperata la configurazione di rete. Queste impostazioni sono definite solo in ambito globale, pertanto verrà restituito solo un elemento.

    Get-CsNetworkConfiguration

## ESEMPIO 2

Esiste un solo set di impostazioni per il bypass multimediale e viene applicato globalmente. Queste impostazioni vengono archiviate come parte della configurazione di rete generale. Questo comando recupera innanzitutto tale configurazione chiamando il cmdlet **Get-CsNetworkConfiguration** e quindi recupera la proprietà MediaBypassSettings della configurazione.

    (Get-CsNetworkConfiguration).MediaBypassSettings

## Descrizione dettagliata

L'oggetto configurazione di rete include tutte le impostazioni globali del bypass multimediale e dell'intera configurazione del servizio Controllo di ammissione di chiamata in una distribuzione di Lync Server, compresa l'indicazione dell'abilitazione o disabilitazione della configurazione. È possibile utilizzare questo cmdlet per recuperare tali configurazioni e impostazioni. Oltre a EnableBandwidthPolicyCheck e MediaBypassSettings, è tuttavia consigliabile utilizzare cmdlet specifici per il tipo di oggetto in modo da recuperare le impostazioni di configurazione del servizio Controllo di ammissione di chiamata. Per recuperare ad esempio le aree di rete, di solito sarà più semplice chiamare il cmdlet **Get-CsNetworkRegion** anziché il cmdlet **Get-CsNetworkConfiguration** e quindi recuperare la proprietà NetworkRegions di tale configurazione.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsNetworkConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkConfiguration"}

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
<td><p>Poiché ci sarà sempre solo una configurazione di rete, questo parametro non è necessario per questo cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Sarà sempre globale.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare la configurazione di rete dalla replica locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet **Get-CsNetworkConfiguration** restituisce un'istanza dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings.

## Vedere anche

#### Ulteriori risorse

[Remove-CsNetworkConfiguration](remove-csnetworkconfiguration.md)  
[Set-CsNetworkConfiguration](set-csnetworkconfiguration.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

