---
title: Set-CsPersistentChatState
TOCTitle: Set-CsPersistentChatState
ms:assetid: 9b82fe41-214d-4376-b026-bb1434d04118
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205109(v=OCS.15)
ms:contentKeyID: 49301441
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPersistentChatState

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica lo stato di un pool del servizio Chat persistente. Un pool di Chat persistente può essere associato a uno dei due stati seguenti: Normal, in cui il pool utilizza i database primari, oppure FailedOver, in cui il pool utilizza i database di backup definiti nella topologia. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsPersistentChatState [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPersistentChatState [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-PoolState <FailedOver | Normal>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 imposta su FailedOver lo stato del pool del server Chat persistente atl-gc-001.litwareinc.com.

    Set-CsPersistentChatState -Identity "PersistentChatServer:atl-gc-001.litwareinc.com" -PoolState "FailedOver"

## Descrizione dettagliata

Il cmdlet [Get-CsPersistentChatState](get-cspersistentchatstate.md) restituisce lo stato di uno o più pool Chat persistente. Un pool Chat persistente può essere associato allo stato Normal, in cui vengono utilizzati i database primari, oppure allo stato FailedOver, in cui vengono utilizzati i database di backup. È possibile utilizzare il cmdlet **Set-CsPersistentChatState** per cambiare lo stato di un pool Chat persistente. Quando si cambia lo stato del pool, Lync Server 2013 cambia automaticamente lo stato di ogni singolo server del pool. Per cambiare lo stato di un singolo server di chat, utilizzare il cmdlet [Set-CsPersistentChatActiveServer](set-cspersistentchatactiveserver.md).

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPersistentChatState"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Set-CsPersistentChatState** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identità del servizio del pool di Chat persistente in cui verrà applicato il nuovo stato del servizio. Ad esempio:</p>
<p>-Identity PersistentChatServer:atl-persistentchat-001.litwareinc.com</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>PoolState</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PoolState</p></td>
<td><p>Stato corrente del pool di Chat persistente. I valori validi sono:</p>
<p>* Normal</p>
<p>* FailedOver</p>
<p>Il valore predefinito è Normal.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Set-CsPersistentChatState** accetta istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatstate inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsPersistentChatState** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatState.

## Vedere anche

#### Ulteriori risorse

[Get-CsPersistentChatState](get-cspersistentchatstate.md)  
[Set-CsPersistentChatActiveServer](set-cspersistentchatactiveserver.md)

