---
title: Get-CsPersistentChatState
TOCTitle: Get-CsPersistentChatState
ms:assetid: 598086c9-a8c7-4b81-84ba-1807f1183024
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204915(v=OCS.15)
ms:contentKeyID: 49300636
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPersistentChatState

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce lo stato di uno o più pool del servizio Chat persistente. Un pool di Chat persistente può essere associato a uno dei due stati seguenti: Normal, in cui il pool utilizza i database primari, oppure FailedOver, in cui il pool utilizza i database di backup definiti nella topologia. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsPersistentChatState [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPersistentChatState [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce lo stato di tutti i server Chat persistente configurati per l'utilizzo nell'organizzazione.

    Get-CsPersistentChatState

## Esempio 2

    Get-CsPersistentChatState -Identity "PersistentChatServer:atl-gc-001.litwareinc.com"

## Esempio 3

Nell'esempio 3 vengono restituite informazioni sullo stato di tutti i server Chat persistente del dominio litwareinc.com. A tale scopo, viene incluso il parametro Filter con il valore "\*.litwareinc.com". Questo valore di filtro garantisce che il cmdlet **Get-CsPersistentChatState** restituisca informazioni su tutti i server Chat persistente la cui identità termina con il valore stringa ".litwareinc.com".

    Get-CsPersistentChatState -Filter "*.litwareinc.com"

## Esempio 4

Il comando riportato nell'esempio 4 restituisce informazioni sullo stato di tutti i server Chat persistente attualmente sottoposti a failover. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsPersistentChatState** senza parametri, in modo da restituire una raccolta di tutti i server Chat persistente dell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i server in cui la proprietà PoolState è uguale a (-eq) "FailedOver".

    Get-CsPersistentChatState | Where-Object {$_.PoolState -eq "FailedOver"}

## Descrizione dettagliata

Il cmdlet **Get-CsPersistentChatState** restituisce lo stato di uno o più pool di Chat persistente. Un pool di Chat persistente può avere lo stato Normal (e utilizzare i database primari) oppure lo stato FailedOver (e utilizzare i database di backup). È possibile utilizzare il cmdlet [Set-CsPersistentChatState](set-cspersistentchatstate.md) per cambiare lo stato di un pool di Chat persistente. Quando si cambia lo stato del pool, Lync Server 2013 cambia automaticamente lo stato dei singoli server del pool.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPersistentChatState"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsPersistentChatState** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Consente di utilizzare i caratteri jolly per recuperare uno o più stati di Chat persistente. Per restituire ad esempio tutti gli stati di Chat persistente del dominio litwareinc.com, utilizzare la sintassi seguente:</p>
<p>-Filter &quot;*.litwareinc.com&quot;</p>
<p>Non è possibile utilizzare i parametri Filter e Identity nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco del pool di Chat persistente, ad esempio:</p>
<p>–Identity &quot;PersistentChatServer:atl-gc-001.litwareinc.com&quot;</p>
<p>Se si omette questo parametro, il cmdlet <strong>Get-CsPersistentChatState</strong> restituirà informazioni su tutti gli stati di Chat persistente.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati sullo stato di Chat persistente dalla replica locale dell'archivio di gestione centrale anziché direttamente dall'archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsPersistentChatState** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsPersistentChatState** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatState.

## Vedere anche

#### Ulteriori risorse

[Set-CsPersistentChatState](set-cspersistentchatstate.md)

