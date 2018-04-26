---
title: Remove-CsNetworkConfiguration
TOCTitle: Remove-CsNetworkConfiguration
ms:assetid: d6945015-67f7-4f04-87ae-7cb977650d96
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398938(v=OCS.15)
ms:contentKeyID: 49302110
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Ripristina i valori predefiniti di tutte le impostazioni di configurazione di rete per una distribuzione di Lync Server. In questo modo vengono eliminate un'intera distribuzione del servizio Controllo di ammissione di chiamata e la configurazione del servizio di chiamate di emergenza E9-1-1 correlata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsNetworkConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio vengono rimosse tutte le impostazioni del servizio Controllo di ammissione di chiamata, di posizione, di rete del servizio di chiamate di emergenza e del bypass degli elementi multimediali. Il parametro Confirm viene utilizzato per visualizzare un prompt che richiede di confermare l'operazione prima che abbia luogo l'eliminazione.

    Remove-CsNetworkConfiguration -Identity Global -Confirm

## Descrizione dettagliata

AVVISO: l'esecuzione di questo cmdlet eliminerà un'intera configurazione di rete, inclusi il servizio Controllo di ammissione di chiamata, i siti e le aree del servizio di chiamate di emergenza e il bypass degli elementi multimediali.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsNetworkConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkConfiguration"}

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
<td><p>Sarà sempre Global.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando. È consigliabile utilizzare sempre questo parametro con il cmdlet.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings. Accetta l'input da pipeline di un oggetto di configurazione di rete.

## Tipi restituiti

Questo cmdlet non restituisce un oggetto. Rimuove un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings.

## Vedere anche

#### Ulteriori risorse

[Set-CsNetworkConfiguration](set-csnetworkconfiguration.md)  
[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

