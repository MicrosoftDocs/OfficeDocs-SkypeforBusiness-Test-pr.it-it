---
title: Set-CsNetworkInterSitePolicy
TOCTitle: Set-CsNetworkInterSitePolicy
ms:assetid: 973979bc-db2c-47a6-909e-5949a927f51c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398772(v=OCS.15)
ms:contentKeyID: 49301389
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkInterSitePolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un criterio tra siti di rete esistente che definisce le limitazioni della larghezza di banda tra i siti direttamente collegati in una configurazione di Controllo di ammissione di chiamata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsNetworkInterSitePolicy [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkInterSitePolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfileID <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-NetworkSiteID1 <String>] [-NetworkSiteID2 <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio viene modificato il criterio di sito con Identity Reno\_Portland. Si utilizza il parametro BWPolicyProfileID per modificare il profilo del criterio di larghezza di banda associato a questo criterio di sito in HighBWLimits.

    Set-CsNetworkInterSitePolicy -Identity Reno_Portland -BWPolicyProfileID HighBWLimits

## Descrizione dettagliata

Se due siti di rete condividono un collegamento diretto, è possibile definire dei limiti della larghezza di banda per le connessioni audio e video tra tali siti. Questo cmdlet modifica un criterio inter-sito di rete che associa un criterio di limitazione della larghezza di banda a due siti connessi in modo diretto.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsNetworkInterSitePolicy** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkInterSitePolicy"}

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
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'identità del profilo del criterio di larghezza di banda che definisce i limiti del criterio di sito. È possibile recuperare un elenco dei profili disponibili chiamando il cmdlet <strong>Get-CsNetworkBandwidthPolicyProfile</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>Identificatore univoco del criterio di sito da modificare. I criteri di sito vengono creati solo con ambito globale, pertanto questo identificatore non richiede di specificare un ambito. Contiene invece una stringa composta da un nome univoco che identifica il criterio di sito.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>InterNetworkSitePolicyType</p></td>
<td><p>Un riferimento oggetto a un criterio di sito modificato in memoria. Questo oggetto deve essere di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType e può essere recuperato chiamando il cmdlet <strong>Get-CsNetworkInterSitePolicy</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkSiteID1</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'identità (NetworkSiteID) di uno dei due siti associati a questo criterio. La combinazione di NetworkSiteID1 e NetworkSiteID2 deve essere univoca (ad esempio, non è possibile definire due criteri di sito che collegano Reno e Portland).</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID2</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'identità (NetworkSiteID) di uno dei due siti associati a questo criterio. La combinazione di NetworkSiteID1 e NetworkSiteID2 deve essere univoca (ad esempio, non è possibile definire due criteri di sito che collegano Reno e Portland).</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType. Accetta l'input da pipeline di oggetti criterio inter-sito di rete.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Modificare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType.

## Vedere anche

#### Ulteriori risorse

[New-CsNetworkInterSitePolicy](new-csnetworkintersitepolicy.md)  
[Remove-CsNetworkInterSitePolicy](remove-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)

