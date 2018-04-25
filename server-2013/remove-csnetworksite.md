---
title: Remove-CsNetworkSite
TOCTitle: Remove-CsNetworkSite
ms:assetid: 07b543a6-3aa0-4fce-85f9-9ddc75d7b14f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398135(v=OCS.15)
ms:contentKeyID: 49299586
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkSite

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un sito di rete che è stato definito per il servizio Controllo di ammissione di chiamata o per servizio di chiamate di emergenza Enhanced 9-1-1 (E9-1-1). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsNetworkSite -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene rimosso il sito con identità Vancouver dalla configurazione CAC o E911.

    Remove-CsNetworkSite -Identity Vancouver

## ESEMPIO 2

Nell'esempio 2 vengono rimossi tutti i siti che utilizzano il profilo dei criteri di larghezza di banda denominato LowBWProfile dalla configurazione del controllo di ammissione di chiamata (CAC) o del servizio per chiamate di emergenza (E9-1-1). In questo esempio viene innanzitutto chiamato il cmdlet **Get-CsNetworkSite** per recuperare tutti i siti di rete. Questa raccolta viene inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i siti in cui la proprietà BWPolicyProfileID è uguale a (-eq) LowBWProfile. Questa nuova raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsNetworkSite**, che rimuove tali siti.

    Get-CsNetworkSite | Where-Object {$_.BWPolicyProfileID -eq "LowBWProfile"} | Remove-CsNetworkSite

## Descrizione dettagliata

I siti di rete sono gli uffici o le località configurate in ciascuna regione di un CAC o distribuzione E9-1-1. Questo cmdlet rimuove un sito dalla configurazione CAC o E9-1-1.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Remove-CsNetworkSite** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkSite"}

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
<td><p>L'identificatore univoco delle sito di rete che si desidera rimuovere. I siti vengono creati solo in ambito globale, perciò non è necessario specificare un ambito. Si deve, invece, specificare solo l'ID del sito.</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType. Accetta input tramite pipeline da oggetti sito di rete.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Consente di rimuovere un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType.

## Vedere anche

#### Ulteriori risorse

[New-CsNetworkSite](new-csnetworksite.md)  
[Set-CsNetworkSite](set-csnetworksite.md)  
[Get-CsNetworkSite](get-csnetworksite.md)

