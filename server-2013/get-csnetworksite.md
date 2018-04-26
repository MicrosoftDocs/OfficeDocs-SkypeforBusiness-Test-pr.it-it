---
title: Get-CsNetworkSite
TOCTitle: Get-CsNetworkSite
ms:assetid: 9627869d-101f-4668-bee2-01fce1d84cbd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398766(v=OCS.15)
ms:contentKeyID: 49301381
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkSite

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera uno o più siti di rete definiti per il servizio Controllo di ammissione di chiamata o per la funzionalità per le chiamate di emergenza Enhanced 9-1-1 (E 9-1-1). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsNetworkSite [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkSite [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Chiamando il cmdlet **Get-CsNetworkSite** senza alcun parametro, verranno restituiti tutti i siti di rete configurati per il servizio Controllo di ammissione di chiamata o per la funzionalità per le chiamate di emergenza E9-1-1 nella distribuzione di Lync Server.

    Get-CsNetworkSite

## ESEMPIO 2

Questo comando consente di recuperare il sito con Identity Redmond (per definizione, NetworkSiteID).

    Get-CsNetworkSite -Identity Redmond

## ESEMPIO 3

Il comando mostrato nell'esempio 3 chiama il cmdlet **Get-CsNetworkSite** con il parametro Filter. Il valore del parametro Filter è NA\* e indica che questo comando recupererà tutti i siti con valore Identity che inizia con la stringa NA seguita da un numero qualsiasi di caratteri. In questo modo verranno restituiti siti quali NARedmond, NAVancouver e NAChicago.

    Get-CsNetworkSite -Filter NA*

## ESEMPIO 4

Nell'esempio 4 vengono utilizzati due cmdlet, **Get-CsNetworkSite** e **Where-Object**, per recuperare tutti i siti che fanno parte dell'area NorthAmerica. Il comando chiama innanzitutto il cmdlet **Get-CsNetworkSite** senza parametri per recuperare tutti i siti della rete. La raccolta di siti viene quindi inviata tramite pipe al cmdlet **Where-Object**, che la filtra ricercando tutti i siti con proprietà NetworkRegionID uguale a (-eq) NorthAmerica.

    Get-CsNetworkSite | Where-Object {$_.NetworkRegionID -eq "NorthAmerica"}

## Descrizione dettagliata

I siti di rete sono gli uffici o le postazioni configurate in ogni area di una distribuzione di Controllo di ammissione di chiamata o della funzionalità per le chiamate di emergenza. Questo cmdlet consente di recuperare le impostazioni per uno o più siti esistenti.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsNetworkSite** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkSite"}

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
<td><p>Una stringa di caratteri jolly che consente di recuperare più siti in base alla corrispondenza fra l'identità del sito e il valore Filter.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificatore univoco del sito della rete che si desidera recuperare. I siti vengono creati solo nell'ambito globale, pertanto non è necessario specificare un ambito. Al contrario, è richiesto di specificare l'ID sito. Si noti che questo valore equivale a NetworkSiteID per il sito della rete.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera le informazioni relative al sito di rete dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Recupera un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType.

## Vedere anche

#### Ulteriori risorse

[New-CsNetworkSite](new-csnetworksite.md)  
[Remove-CsNetworkSite](remove-csnetworksite.md)  
[Set-CsNetworkSite](set-csnetworksite.md)

