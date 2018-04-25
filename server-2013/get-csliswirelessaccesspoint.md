---
title: Get-CsLisWirelessAccessPoint
TOCTitle: Get-CsLisWirelessAccessPoint
ms:assetid: 060ea753-2fa8-4473-8e90-cb3e0fd91e63
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398117(v=OCS.15)
ms:contentKeyID: 49299560
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsLisWirelessAccessPoint

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera uno o più punti di accesso wireless (WAP) dal database delle configurazioni delle località. È possibile associare ogni WAP a una località, nel qual caso questo cmdlet recupera anche le informazioni sulle località dei punti WAP. Questa associazione è utilizzata in un'implementazione di VoIP aziendale con il servizio di chiamate di emergenza Enhanced 9-1-1 (E9-1-1) per segnalare la località del chiamante all'operatore del servizio di emergenza. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsLisWirelessAccessPoint

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono recuperati tutti i WAP LIS (Location Information Server) definiti nella distribuzione di Lync Server.

    Get-CsLisWirelessAccessPoint

## ESEMPIO 2

In questo esempio vengono recuperate tutte le informazioni di tutti i WAP che hanno un identificatore BSSID (Basic Service Set Identifier) uguale a 99-99-99-99-99-99. Poiché gli identificatori BSSID devono essere univoci, questo comando potrà recuperare al massimo una località WAP. Il comando innanzitutto chiama il cmdlet **Get-CsLisWirelessAccessPoint** per recuperare tutte le associazioni WAP-località. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** verifica la proprietà BSSID di ogni elemento nella raccolta e restituisce l'elemento con BSSID uguale a 99-99-99-99-99-99.

    Get-CsLisWirelessAccessPoint | Where-Object {$_.BSSID -eq "99-99-99-99-99-99"}

## ESEMPIO 3

In questo esempio vengono recuperate tutte le informazioni di tutti i WAP associati a una località nella città di Redmond. Il comando innanzitutto utilizza il cmdlet **Get-CsLisWirelessAccessPoint** per recuperare tutte le associazioni WAP-località. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** verifica la proprietà City di ogni elemento nella raccolta per stabilire se il valore è uguale a (-eq) Redmond.

    Get-CsLisWirelessAccessPoint | Where-Object {$_.City -eq "Redmond"}

## Descrizione dettagliata

Enhanced 9-1-1 consente all'operatore del servizio di emergenza di identificare la località di un chiamante senza dover richiedere questa informazione al chiamante. Nel caso in cui una persona stia chiamando tramite una connessione VoIP (Voice over Internet Protocol), queste informazioni possono essere dedotte da diversi elementi della connessione. L'amministratore della connessione VoIP deve configurare una mappa delle località (chiamata wiremap) che consente di stabilire la località di un chiamante. Questo cmdlet consente di recuperare le informazioni sulle associazioni tra le località fisiche e il WAP tramite il quale è connesso il client.

Questo cmdlet non utilizza altri parametri (oltre a quelli comuni di Windows PowerShell). Il cmdlet recupererà tutte le istanze delle associazioni tra WAP e località. Per limitare la quantità di informazioni recuperate, è necessario inviare l'output tramite pipe da questo cmdlet a un altro cmdlet di Windows PowerShell, come ad esempio il cmdlet **Where-Object** o il cmdlet **Select-Object**

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsLisWirelessAccessPoint** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsLisWirelessAccessPoint"}

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
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Questo cmdlet fornisce solo i parametri comuni di Windows PowerShell.</p></td>
<td><p></p></td>
<td><p></p></td>
<td> </td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Questo cmdlet consente di recuperare uno o più oggetti di tipo System.Management.Automation.PSCustomObject.

## Vedere anche

#### Ulteriori risorse

[Remove-CsLisWirelessAccessPoint](remove-csliswirelessaccesspoint.md)  
[Set-CsLisWirelessAccessPoint](set-csliswirelessaccesspoint.md)

