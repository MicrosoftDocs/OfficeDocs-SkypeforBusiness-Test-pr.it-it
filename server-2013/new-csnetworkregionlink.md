---
title: New-CsNetworkRegionLink
TOCTitle: New-CsNetworkRegionLink
ms:assetid: 61a6a7be-8078-4d59-a78a-2f241f6bf800
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398437(v=OCS.15)
ms:contentKeyID: 49300754
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkRegionLink

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un collegamento tra due aree configurate per il servizio Controllo di ammissione di chiamata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsNetworkRegionLink -NetworkRegionLinkID <String> <COMMON PARAMETERS>

    New-CsNetworkRegionLink -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -NetworkRegionID1 <String> -NetworkRegionID2 <String> [-BWPolicyProfileID <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene creato un nuovo collegamento di aree di rete denominato NA\_EMEA per collegare le aree NorthAmerica ed EMEA. Il nome del collegamento di aree è specificato come valore per il parametro Identity. Questo valore viene assegnato automaticamente anche a NetworkRegionLinkID. Le due aree di rete da collegare sono parametri obbligatori per la creazione del collegamento, in questo caso le aree denominate NorthAmerica ed EMEA. In questo esempio è stato anche assegnato un valore al parametro BWPolicyProfile. In questo modo i limiti di larghezza di banda definiti nel profilo dei criteri di larghezza di banda (LowBWLimits) verranno assegnati alle connessioni tra queste aree. Se non viene specificato alcun valore BWPolicyProfileID, non verranno applicati limiti di larghezza di banda per le connessioni tra queste due aree. Potrebbero esistere comunque limiti tra i siti. Per informazioni dettagliate, vedere l'argomento relativo al cmdlet **New-CsNetworkSite** nella Guida.

    New-CsNetworkRegionLink -Identity NA_EMEA -NetworkRegionID1 NorthAmerica -NetworkRegionID2 EMEA -BWPolicyProfileID LowBWLimits

## Descrizione dettagliata

Le regioni all'interno di una rete sono collegate tramite connessioni WAN (Wide Area Network) fisiche. Questo cmdlet consente di definire un collegamento tra due regioni e di impostare i limiti della larghezza di banda per le connessioni audio e video tra queste due regioni.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsNetworkRegionLink** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkRegionLink"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Un identificatore univoco per il collegamento di rete tra regioni appena creato. I collegamenti di rete tra regioni vengono creati solo nell'ambito globale, per cui in questo identificatore non è necessario specificare un ambito. L'identificatore contiene invece una stringa che costituisce il nome univoco di quello specifico collegamento.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID1</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>L'identità (NetworkRegionID) della regione collegata alla regione identificata dal parametro NetworkRegionID2.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionID2</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>L'identità (NetworkRegionID) della regione collegata alla regione identificata dal parametro NetworkRegionID1.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionLinkID</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Questo valore è uguale all'identità. Non è possibile specificare valori diversi per Identity e NetworkRegionLinkID; il valore immesso per l'uno verrà automaticamente utilizzato anche per l'altro.</p></td>
</tr>
<tr class="odd">
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>L'identità del profilo dei criteri di larghezza di banda che definisce i limiti della larghezza di banda per questo collegamento. È possibile recuperare un elenco di profili disponibili utilizzando il cmdlet <strong>Get-CsNetworkBandwidthPolicyProfile</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Questo cmdlet consente di creare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType.

## Vedere anche

#### Ulteriori risorse

[Remove-CsNetworkRegionLink](remove-csnetworkregionlink.md)  
[Set-CsNetworkRegionLink](set-csnetworkregionlink.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkSite](new-csnetworksite.md)

