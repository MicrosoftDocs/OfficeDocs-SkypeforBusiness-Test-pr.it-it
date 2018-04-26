---
title: Get-CsClsConfiguration
TOCTitle: Get-CsClsConfiguration
ms:assetid: 5fef2e35-e23c-453d-97e5-cb9c4e7bfef7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619179(v=OCS.15)
ms:contentKeyID: 49300730
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClsConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle impostazioni di configurazione della registrazione centralizzata in uso nell'organizzazione. La registrazione centralizzata consente agli amministratori di abilitare o disabilitare simultaneamente la traccia eventi su più computer.Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsClsConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsClsConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce informazioni su tutte le impostazioni di configurazione della registrazione centralizzata in uso nell'organizzazione.

    Get-CsClsConfiguration

## Esempio 2

Nell'esempio 2 vengono restituite informazioni relative a una sola raccolta di impostazioni di configurazione della registrazione centralizzata: la raccolta applicata al sito di Redmond.

    Get-CsClsConfiguration -Identity "site:Redmond"

## Esempio 3

L'esempio 3 riporta informazioni dettagliate sugli scenari di registrazione centralizzata disponibili per il sito di Redmond. A questo scopo, il comando prima recupera tutti i valori delle proprietà di registrazione centralizzata per il sito di Redmond. Tali valori di proprietà vengono quindi inoltrati tramite pipe al cmdlet Select-Object, che utilizza il parametro ExpandProperty per "espandere" i valori trovati nella proprietà Scenarios. Quando si espande una proprietà non si fa che visualizzare tutte le informazioni archiviate in essa in modo che risultino facilmente leggibili.

    Get-CsClsConfiguration -Identity "site:Redmond" | Select-Object -ExpandProperty Scenarios

## Esempio 4

Nell'esempio 4 vengono restituite informazioni per tutte le impostazioni di configurazione della registrazione centralizzata in cui l'intervallo di rollover del file ETL è maggiore di un'ora. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsClsConfiguration** senza parametri. Viene restituita una raccolta di tutte le impostazioni di configurazione della registrazione centralizzata dell'organizzazione. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà EtlFileRolloverMinutes è maggiore di (-gt) 60 minuti.

    Get-CsClsConfiguration | Where-Object {$_.EtlFileRolloverMinutes -gt 60}

## Esempio 5

Il comando riportato nell'esempio 5 è simile a quello dell'esempio 4. In questo caso però vengono restituite informazioni solo per le impostazioni di configurazione della registrazione centralizzata che includono uno scenario "HybridVoice". A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsClsConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione della registrazione centralizzata. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni che prevedono almeno uno scenario in cui la proprietà Name include (-match) il valore stringa "HybridVoice".

    Get-CsClsConfiguration | Where-Object {$_.Scenarios.Name -match "HybridVoice"}

## Descrizione dettagliata

Il servizio di registrazione centralizzata, che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010, consente agli amministratori di gestire le funzioni di registrazione e traccia per tutti i computer e i pool che eseguono Lync Server 2013. Il servizio consente infatti di interrompere, avviare e configurare la registrazione per uno o più pool e computer con un solo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del servizio Rubrica in tutti i server della Rubrica. Questa procedura non è invece eseguibile con gli strumenti OCSLogger e OCSTracer, che devono essere gestiti singolarmente (e anche arrestati e avviati singolarmente) in ogni server. Il servizio di registrazione centralizzata inoltre consente agli amministratori di eseguire ricerche nei log di traccia dal comando utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

La registrazione centralizzata si basa su una serie di scenari predefiniti che assicurano un approccio alla registrazione più mirato di quello garantito dalle precedenti versioni diLync Server. Questi scenari predeterminano i componenti server e la registrazione e quindi un amministratore che abiliti lo scenario RGS può star certo che registrerà solo le informazioni attinenti al Response Group Service e non quelle concernenti, ad esempio, il servizio provider di servizi di audioconferenza.

È inoltre possibile definire scenari personalizzati usando il cmdlet [New-CsClsScenario](new-csclsscenario.md).

La registrazione centralizzata viene gestita utilizzando raccolte di impostazioni di configurazione. Quando si installaMicrosoft Lync Server 2013, viene installato un insieme globale di queste impostazioni di configurazione. Gli amministratori inoltre possono aggiungere raccolte di impostazioni personalizzate nell'ambito del sito. Il cmdlet **Get-CsClsConfiguration** consente agli amministratori di restituire informazioni su tutte le impostazioni di configurazione della registrazione centralizzata in uso nell'organizzazione.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli del controllo di accesso basato sui ruoli creati personalmente), al prompt di Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClsConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsClsConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Consente di utilizzare caratteri jolly per restituire una o più raccolte di impostazioni di configurazione della registrazione centralizzata. Per restituire, ad esempio, una raccolta di tutte le impostazioni configurate nell'ambito del sito, utilizzare la sintassi seguente:</p>
<p>-Filter &quot;site:*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica l'identificatore univoco della raccolta di impostazioni di configurazione della registrazione centralizzata che si desidera restituire. Per fare riferimento alle impostazioni globali, utilizzare la sintassi seguente:</p>
<p>-Identity &quot;global&quot;</p>
<p>Per far riferimento a una raccolta configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>Si noti che non è possibile utilizzare caratteri jolly quando si specifica un parametro Identity. Se tuttavia è necessario utilizzare caratteri jolly, includere il parametro Filter.</p>
<p>Se questo parametro non è specificato, il cmdlet <strong>Get-CsClsConfiguration</strong> restituisce una raccolta di tutte le impostazioni di configurazione della registrazione centralizzata in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione della registrazione centralizzata dalla replica locale dell'archivio di gestione centrale invece che dall'archivio stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsClsConfiguration** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsClsConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.CentralizedLoggingConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsClsConfiguration](new-csclsconfiguration.md)  
[Remove-CsClsConfiguration](remove-csclsconfiguration.md)  
[Set-CsClsConfiguration](set-csclsconfiguration.md)

