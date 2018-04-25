---
title: Get-CsLisSwitch
TOCTitle: Get-CsLisSwitch
ms:assetid: 2b09e8f1-4930-4ac2-8f6f-48c08cd890c5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425769(v=OCS.15)
ms:contentKeyID: 49300020
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsLisSwitch

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera uno o più commutatori di rete dal database delle configurazioni delle località. È possibile associare ogni commutatore a una località, nel qual caso questo cmdlet recupera anche le informazioni sulle località dei commutatori. Questa associazione è utilizzata in un'implementazione di VoIP aziendale con il servizio di chiamate di emergenza Enhanced 9-1-1 (E9-1-1) per segnalare la località del chiamante all'operatore del servizio di emergenza. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsLisSwitch

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono recuperati tutti i commutatori LIS (Location Information Server) definiti nella distribuzione di Lync Server.

    Get-CsLisSwitch

## ESEMPIO 2

In questo esempio vengono recuperate tutte le informazioni di tutti i commutatori con ChassisID uguale a 99-99-99-99-99-99. Poiché il valore ChassisID deve essere univoco, questo comando recupererà al massimo una località commutatore. Il comando innanzitutto chiama il cmdlet **Get-CsLisSwitch** per recuperare tutte le associazioni tra commutatori e località. Questa raccolta di località commutatore viene quindi inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** verifica la proprietà ChassisID di ogni elemento della raccolta e restituisce l'elemento con il valore ChassisID uguale a 99-99-99-99-99-99.

    Get-CsLisSwitch | Where-Object {$_.ChassisID -eq "99-99-99-99-99-99"}

## ESEMPIO 3

In questo esempio vengono recuperate tutte le informazioni di tutti i commutatori associati a una località corrispondente alla città di Redmond. Il comando innanzitutto chiama il cmdlet **Get-CsLisSwitch** per recuperare tutte le associazioni tra commutatori e località. Questa raccolta di località commutatore viene quindi inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** verifica la proprietà City di ogni elemento della raccolta per stabilire se il valore è uguale a (-eq) Redmond.

    Get-CsLisSwitch | Where-Object {$_.City -eq "Redmond"}

## Descrizione dettagliata

Enhanced 9-1-1 consente all'operatore del servizio di emergenza di identificare la località di un chiamante senza dover richiedere questa informazione al chiamante. Nel caso in cui una persona stia chiamando tramite una connessione VoIP (Voice over Internet Protocol), queste informazioni possono essere dedotte da diversi elementi della connessione. L'amministratore della connessione VoIP deve configurare una mappa delle località (chiamata wiremap) che consente di determinare la località di un chiamante. Questo cmdlet consente di recuperare le informazioni sulle associazioni tra le località fisiche e lo switch di rete tramite il quale è connesso il client.

Questo cmdlet non utilizza altri parametri (oltre a quelli comuni di Windows PowerShell). Il cmdlet recupererà tutte le istanze delle associazioni tra commutatori e località. Per limitare la quantità di informazioni restituite, è necessario inviare tramite pipe l'output di questo cmdlet a un altro cmdlet di Windows PowerShell, ad esempio **Where-Object** o **Select-Object**

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsLisSwitch** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsLisSwitch"}

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

[Remove-CsLisSwitch](remove-cslisswitch.md)  
[Set-CsLisSwitch](set-cslisswitch.md)

