---
title: Get-CsPoolFabricState
TOCTitle: Get-CsPoolFabricState
ms:assetid: 9fe6cce5-4142-47b3-94ac-4cb8b94ec215
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619188(v=OCS.15)
ms:contentKeyID: 49301490
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPoolFabricState

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce lo stato Windows Fabric per un pool di Lync Server 2013. Windows Fabric è una tecnologia Microsoft utilizzata per creare applicazioni altamente affidabili, distribuibili e scalabili. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsPoolFabricState -PoolFqdn <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Type <All | MCUFactory | ConferenceDirectory | Routing | LYSS>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando mostrato nell'Esempio 1 restituisce lo stato Fabric del pool atl-cs-001.litwareinc.com. Poiché non è stato specificato il parametro Type, verranno restituite le informazioni sullo stato di tutti i servizi del pool.

    Get-CsPoolFabricState -PoolFqdn "atl-cs-001.litwareinc.com"

## Esempio 2

Nell'Esempio 2 viene restituito lo stato Fabric di un singolo servizio del pool atl-cs-001.litwareinc.com, ovvero il servizio factory MCU. A tale scopo vengono specificati il parametro Type e il valore di parametro "MCU".

    Get-CsPoolFabricState -PoolFqdn "atl-cs-001.litwareinc.com" -Type MCU

## Descrizione dettagliata

Il cmdlet **Get-CsPoolFabricState** restituisce lo stato Windows Fabric per un pool di Lync Server 2013, incluse informazioni sulle istanze di replica Windows Fabric per alcuni o per tutti i servizi seguenti: factory MCU, Directory conferenze, Routing; servizio di archiviazione di Lync Server.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPoolFabricState"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsPoolFabricState** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>PoolFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del pool che si sta verificando. Quando si chiama questo cmdlet è necessario specificare il nome di dominio completo di un pool, ad esempio:</p>
<p>-PoolFqdn &quot;atl-cs-001.litwareinc.com”</p></td>
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
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Type</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.HADR.GetOcsPoolFabricStateCmdlet+FabricEnumerationType</p></td>
<td><p>Specifica il tipo di servizio da restituire. I valori consentiti sono:</p>
<p>* All (restituisce informazioni su tutti i servizi)</p>
<p>* MCUFactory (restituisce informazioni sul servizio factory MCU)</p>
<p>* ConferenceDirectory (restituisce informazioni sul servizio Directory conferenze)</p>
<p>LYSS (restituisce informazioni sul servizio di archiviazione di Lync Server)</p>
<p>È possibile specificare un solo tipo per ogni comando.</p></td>
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

Nessuno. Il cmdlet **Get-CsPoolFabricState** non supporta l'input da pipeline.

## Tipi restituiti

Valore stringa che rappresenta lo stato dell'infrastruttura. Il cmdlet **Get-CsPoolFabricState** non restituisce oggetti.

