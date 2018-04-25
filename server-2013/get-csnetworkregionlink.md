---
title: Get-CsNetworkRegionLink
TOCTitle: Get-CsNetworkRegionLink
ms:assetid: dc5cb988-13e2-4af4-8b36-0aaa58ebf1c5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398972(v=OCS.15)
ms:contentKeyID: 49302202
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkRegionLink

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera uno o più collegamenti tra aree di rete configurate per il servizio Controllo di ammissione di chiamata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsNetworkRegionLink [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkRegionLink [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono recuperati tutti i collegamenti di aree della rete definiti in una distribuzione di Lync Server.

    Get-CsNetworkRegionLink

## ESEMPIO 2

Nell'esempio 2 vengono recuperate informazioni relative (al massimo) a un solo collegamento dell'area della rete e, più specificamente, al collegamento con l'identità NA\_EMEA.

    Get-CsNetworkRegionLink -Identity NA_EMEA

## ESEMPIO 3

In questo esempio viene utilizzato il parametro Filter per recuperare tutti i collegamenti dell'area della rete il cui nome (identità) contiene la stringa EMEA. Notare i caratteri \*, prima e dopo la stringa EMEA. Questo significa che la stringa può essere preceduta o seguita da qualsiasi carattere; l'importante è che l'identità includa la stringa EMEA. In tal modo, verranno recuperati collegamenti con nomi quali, ad esempio, NA\_EMEA, EMEA\_APAC e EMEA2\_SA.

    Get-CsNetworkRegionLink -Filter *EMEA*

## ESEMPIO 4

In questo esempio vengono recuperati tutti i collegamenti area di rete che includono EMEA come una delle due aree da collegare. Nell'esempio viene innanzitutto chiamato il cmdlet **Get-CsNetworkRegionLink** senza alcun parametro. In tal modo, verranno recuperati tutti i collegamenti di aree. La raccolta di collegamenti viene quindi inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** esamina, uno per uno, i membri della raccolta, verificando i valori delle proprietà NetworkRegionID1 e NetworkRegionID2. Se una di queste proprietà è uguale a EMEA, ossia se NetworkRegionID1 è uguale a (-eq) EMEA o (-or) NetworkRegionID2 è uguale a (-eq) EMEA, l'elemento verrà mantenuto nella raccolta e visualizzato.

    Get-CsNetworkRegionLink | Where-Object {$_.NetworkRegionID1 -eq "EMEA" -or $_.NetworkRegionID2 -eq "EMEA"}

## Descrizione dettagliata

Le regioni all'interno di una rete sono collegate tramite connettività fisica WAN. Questo cmdlet recupera uno o più collegamenti di aree definiti nelle impostazioni di configurazione della rete per una distribuzione di Lync Server.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsNetworkRegionLink** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkRegionLink"}

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
<td><p>Accetta una stringa di caratteri jolly che viene utilizzata per recuperare collegamenti di rete in base alla corrispondenza del valore dell'identità con la stringa di caratteri jolly.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>L'identificatore univoco del collegamento delle regioni di rete che si desidera recuperare. I collegamenti delle regioni di rete vengono creati esclusivamente nell'ambito globale, quindi l'identificatore non richiede la specificazione di un ambito. Contiene invece una stringa con un nome univoco che identifica il collegamento. Questo valore è lo stesso di NetworkRegionLinkID.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera le informazioni relative ai collegamenti di aree della rete dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Recupera uno o più oggetti di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType.

## Vedere anche

#### Ulteriori risorse

[New-CsNetworkRegionLink](new-csnetworkregionlink.md)  
[Remove-CsNetworkRegionLink](remove-csnetworkregionlink.md)  
[Set-CsNetworkRegionLink](set-csnetworkregionlink.md)

