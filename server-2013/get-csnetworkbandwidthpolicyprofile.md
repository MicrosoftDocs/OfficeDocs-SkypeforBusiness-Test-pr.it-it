---
title: Get-CsNetworkBandwidthPolicyProfile
TOCTitle: Get-CsNetworkBandwidthPolicyProfile
ms:assetid: 31784852-0cf4-4114-bf92-5eef6f346c47
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425815(v=OCS.15)
ms:contentKeyID: 49300100
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkBandwidthPolicyProfile

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera uno o più profili criteri larghezza di banda della rete. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsNetworkBandwidthPolicyProfile [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkBandwidthPolicyProfile [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Se si chiama il cmdlet **Get-CsNetworkBandwidthPolicyProfile** senza alcun parametro, verranno recuperati tutti i profili dei criteri di larghezza di banda definiti nella distribuzione di Lync Server.

    Get-CsNetworkBandwidthPolicyProfile

## ESEMPIO 2

In questo esempio viene recuperato il profilo dei criteri di larghezza di banda con Identity LowBWProfile. Poiché le identità devono essere univoche, il comando restituirà al massimo un profilo.

    Get-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile

## ESEMPIO 3

In questo esempio viene utilizzato il parametro Filter, per specificare uno o più profili da recuperare in base a una stringa di caratteri jolly. È stata utilizzata la stringa \*50MB\*, che indica che si desidera recuperare tutti i profili dei criteri di larghezza di banda in cui i valori Identity contengono la stringa 50MB in qualsiasi posizione. Ad esempio, questo parametro consente di recuperare profili con identità simili a "BW profile for 50MB links", "50MB audio limit" e "video limits of 50MB".

    Get-CsNetworkBandwidthPolicyProfile -Filter *50MB*

## Descrizione dettagliata

Nel servizio Controllo di ammissione di chiamata i criteri larghezza di banda vengono utilizzati per definire le limitazioni di larghezza di banda per alcune modalità. In Lync Server è possibile assegnare limitazioni di larghezza di banda solo alle modalità audio e video. Questo cmdlet recupera uno o più profili contenitore per tali criteri.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsNetworkBandwidthPolicyProfile** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkBandwidthPolicyProfile"}

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
<td><p>Una stringa contenente caratteri jolly utilizzata per recuperare i profili dei criteri di larghezza di banda in cui i valori Identity corrispondono al modello di caratteri jolly.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Valore stringa che identifica in modo univoco il profilo dei criteri di larghezza di banda che si desidera recuperare. Se si specifica un'identità, viene recuperato al massimo un profilo.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera il profilo dei criteri di larghezza di banda della rete dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Restituisce un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType.

## Vedere anche

#### Ulteriori risorse

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Remove-CsNetworkBandwidthPolicyProfile](remove-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)

