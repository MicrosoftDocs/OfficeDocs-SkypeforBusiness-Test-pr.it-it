---
title: Get-CsPoolUpgradeReadinessState
TOCTitle: Get-CsPoolUpgradeReadinessState
ms:assetid: 127c718e-8949-4bcd-b954-5182b8730820
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204689(v=OCS.15)
ms:contentKeyID: 49299742
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPoolUpgradeReadinessState

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni che indicano se i pool di registrazione di Skype for Business online sono pronti o meno per l'aggiornamento. Lo stato di idoneità all'aggiornamento di un pool si basa sui domini di aggiornamento configurati per il pool. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsPoolUpgradeReadinessState [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce lo stato di idoneità all'aggiornamento del pool di registrazione locale. Questo comando deve essere eseguito in un Front End Server contenuto nel pool.

    Get-CsPoolUpgradeReadinessState

## Descrizione dettagliata

Il cmdlet **Get-CsPoolUpgradeReadinessState** restituisce informazioni sull'idoneità all'aggiornamento di un pool di Lync Server 2013. Tra le informazioni restituite sono inclusi il numero di Front End Server assegnati al pool, il numero di Front End Server attualmente attivi, il nome del dominio di aggiornamento e un valore True/False che indica se lo stato corrente del pool consente l'aggiornamento. Si noti che questo cmdlet deve essere eseguito localmente in un Front End Server nel pool che viene verificato. Non sono disponibili opzioni che consentono di eseguire il cmdlet **Get-CsPoolUpgradeReadinessState** da postazione remota.

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsPoolUpgradeReadinessState** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
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

Nessuno. Il cmdlet **Get-CsPoolUpgradeReadinessState** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Get-CsPoolUpgradeReadinessState** restituisce un'istanza dell'oggetto Microsoft.Rtc.Management.Hadr.PoolUpgradeState.

