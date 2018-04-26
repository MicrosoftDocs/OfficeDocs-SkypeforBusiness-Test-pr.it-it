---
title: Get-CsLisCivicAddress
TOCTitle: Get-CsLisCivicAddress
ms:assetid: 6538b811-6b74-4c57-95f7-e1496df62e7f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398459(v=OCS.15)
ms:contentKeyID: 49300794
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsLisCivicAddress

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera solo la parte dell'indirizzo di una o più posizioni nel database di configurazione delle posizioni per il servizio di chiamate di emergenza Enhanced 9-1-1 (E9-1-1). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsLisCivicAddress

## Esempi

## ESEMPIO 1

Con questo esempio vengono recuperati tutti gli indirizzi civici dal database delle posizioni. Il cmdlet **Get-CsLisCivicAddress** non accetta parametri (se non i parametri comuni di Windows PowerShell come Verbose). Di conseguenza, qualsiasi chiamata al cmdlet **Get-CsLisCivicAddress** restituirà sempre tutti gli indirizzi civici. Vedere l'esempio 2 per un comando che consente di recuperare risultati più specifici.

    Get-CsLisCivicAddress

## ESEMPIO 2

Con questo esempio vengono recuperati tutti gli indirizzi civici nella città di Redmond. L'esempio inizia con una chiamata al cmdlet **Get-CsLisCivicAddress** per recuperare una raccolta di tutti gli indirizzi civici definiti nel database delle posizioni. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che restituisce solo gli elementi nella raccolta per cui la proprietà City equivale (-eq) a Redmond.

    Get-CsLisCivicAddress | Where-Object {$_.City -eq "Redmond"}

## ESEMPIO 3

Con l'esempio 3 vengono recuperati tutti gli indirizzi civici LIS convalidati rispetto allo stradario informatico.

    Get-CsLisCivicAddress | Where-Object {$_.MSAGValid -eq $true}

## Descrizione dettagliata

Il servizio E9-1-1 consente a chi risponde alle chiamate di emergenza di determinare la posizione geografica del chiamante senza dovergli richiedere tali informazioni. In Lync Server la posizione viene determinata in base al mapping di porta, subnet, commutatore o punto di accesso wireless del chiamante a una posizione specifica. Questo cmdlet recupera uno o più indirizzi associati a queste posizioni.

Questo cmdlet differisce dal cmdlet **Get-CsLisLocation** in quanto restituisce solo indirizzi univoci. Non restituisce il nome della società o il nome della posizione, ma solo le informazioni sull'indirizzo. Restituisce inoltre un flag (MSAGValid) che specifica se l'indirizzo è stato convalidato rispetto allo stradario informatico. Questo flag può essere automaticamente aggiornato eseguendo il cmdlet **Test-CsLisCivicAddress**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Get-CsLisCivicAddress** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsLisCivicAddress"}

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
<td><p>Questo cmdlet fornisce unicamente i parametri comuni di Windows PowerShell.</p></td>
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

[Test-CsLisCivicAddress](test-csliscivicaddress.md)  
[Get-CsLisLocation](get-cslislocation.md)

