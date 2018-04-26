---
title: Get-CsRgsConfiguration
TOCTitle: Get-CsRgsConfiguration
ms:assetid: a3667917-cfbf-47c1-8b48-e936594b5357
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412762(v=OCS.15)
ms:contentKeyID: 49301540
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsRgsConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle impostazioni di configurazione per l'applicazione Response Group. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsRgsConfiguration -Identity <RgsIdentity>

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituite le impostazioni di configurazione di Response Group per il servizio ApplicationServer:atl-cs-001.litwareinc.com. Poiché può esserci soltanto una raccolta di impostazioni per ogni servizio, questo comando non restituirà più di un singolo elemento.

    Get-CsRgsConfiguration -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com"

## ESEMPIO 2

Il comando mostrato nell'esempio 2 restituisce il valore di una singola proprietà, DisableCallContext, delle impostazioni di configurazione di Response Group trovate nel servizio ApplicationServer:atl-cs-001.litwareinc.com. Per ottenere questo risultato, viene innanzitutto utilizzato **Get-CsRgsConfiguration** per recuperare tutti i valori delle proprietà delle impostazioni di configurazione di Response Group per ApplicationServer:atl-cs-001.litwareinc.com. Questo comando è racchiuso tra parentesi allo scopo di garantire che Windows PowerShell restituisca tutti i valori delle proprietà prima di eseguire qualsiasi operazione.

Dopo che i valori della proprietà sono stati restituiti, viene utilizzato lo standard "dot notation" per visualizzare il valore della proprietà DisableCallContext (e solo il valore di tale proprietà). Lo standard "dot notation" consiste in un oggetto seguito da un punto (dot), seguito a sua volta dal nome della proprietà da visualizzare. Ad esempio, per visualizzare il valore della proprietà AgentRingbackGracePeriod (e solo il valore di tale proprietà), è possibile utilizzare questo comando:

(Get-CsRgsConfiguration -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com").AgentRingbackGracePeriod.

    (Get-CsRgsConfiguration -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com").DisableCallContext

## ESEMPIO 3

Il comando mostrato nell'esempio 3 illustra come restituire informazioni di configurazione di Response Group da tutti i computer che eseguono il Servizio applicazione e che ospitano un'istanza dell'applicazione Response Group. A tale scopo, nel comando vengono innanzitutto utilizzati il cmdlet **Get-CsService** e il parametro ApplicationServer per restituire le informazioni relative a tutti i server dell'organizzazione in cui è in esecuzione il Servizio applicazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i server la cui proprietà Applications contiene l'applicazione "urn:application:RGS". Tale valore indica che l'applicazione Response Group è in esecuzione nel server.

Tali server vengono quindi inviati tramite pipe al cmdlet **ForEach-Object**, che individua i singoli server presenti nella raccolta e utilizza **Get-CsRgsConfiguration** per restituire le informazioni di configurazione di Response Group relative a ciascun server.

    Get-CsService -ApplicationServer | Where-Object {$_.Applications -contains "urn:application:RGS"} | ForEach-Object {Get-CsRgsConfiguration -Identity $_.Identity}

## Descrizione dettagliata

L'applicazione Response Group consente di instradare automaticamente le chiamate telefoniche a entità come il supporto tecnico o la linea del servizio clienti. Quando qualcuno chiama un numero di telefono designato, la chiamata può essere instradata direttamente all'insieme appropriato di agenti di Response Group. In alternativa, la chiamata può essere innanzitutto instradata a una coda del sistema IVR (Interactive Voice Response). In questa coda verrà posta una serie di domande (ad esempio, "Sta chiamando per un ordine ﻿in corso?") e quindi il chiamante, in base alle risposte date, verrà instradato alla coda appropriata di Response Group.

Il cmdlet **Get-CsRgsConfiguration** consente di restituire informazioni su come è stata configurata l'applicazione Response Group. Per impostazione predefinita, tale cmdlet restituisce informazioni solo da un'istanza dell'applicazione Response Group alla volta. Ad esempio, in presenza di installazioni separate dell'applicazione Response Group, una in ApplicationServer:atl-cs-001.litwareinc.com e una in ApplicationServer:dublin-cs-001.litwareinc.com, di solito sarà necessario effettuare chiamate distinte a **Get-CsRgsConfiguration** per restituire informazioni per ciascuna di queste istanze di Response Group. Nella sezione relativa agli esempi di questo argomento viene tuttavia mostrato come ovviare al problema.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsRgsConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsRgsConfiguration"}

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
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>Nome del servizio che ospita le impostazioni di configurazione di Response Group. Ad esempio: -Identity &quot;service:ApplicationServer:atl-cs-001.litwareinc.com&quot;. Se non si include questo parametro, <strong>Get-CsRgsConfiguration</strong> richiederà di fornire un'identità.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa. **Get-CsRgsConfiguration** accetta un valore stringa che rappresenta l'identità delle impostazioni di configurazione di Response Group.

## Tipi restituiti

**Get-CsRgsConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.ServiceSettings.

## Vedere anche

#### Ulteriori risorse

[Move-CsRgsConfiguration](move-csrgsconfiguration.md)  
[Set-CsRgsConfiguration](set-csrgsconfiguration.md)

