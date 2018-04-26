---
title: Set-CsClsConfiguration
TOCTitle: Set-CsClsConfiguration
ms:assetid: 6cebd908-e829-4dee-82fd-1164bc8999ee
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619182(v=OCS.15)
ms:contentKeyID: 49300900
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClsConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta esistente di impostazioni di configurazione della registrazione centralizzata. Quest'ultima consente agli amministratori di abilitare o disabilitare contemporaneamente la traccia su più computer. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsClsConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsClsConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-CacheFileLocalFolders <String>] [-CacheFileLocalMaxDiskUsage <UInt32>] [-CacheFileLocalRetentionPeriod <UInt32>] [-CacheFileNetworkFolder <String>] [-ComponentThrottleLimit <UInt32>] [-ComponentThrottleSample <UInt32>] [-Confirm [<SwitchParameter>]] [-EtlFileFolder <String>] [-EtlFileRolloverMinutes <UInt32>] [-EtlFileRolloverSizeMB <UInt32>] [-Force <SwitchParameter>] [-MinimumClsAgentServiceVersion <UInt32>] [-Regions <PSListModifier>] [-Scenarios <PSListModifier>] [-SearchTerms <PSListModifier>] [-SecurityGroups <PSListModifier>] [-TmfFileSearchPath <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Nell'Esempio 1 la raccolta globale di impostazioni di configurazione della registrazione centralizzata viene modificata in modo da impostare la dimensione massima di un file ETL su 40 MB.

    Set-CsClsConfiguration -Identity "global" -EtlRolloverFileSizeMB 40

## Esempio 2

Il comando mostrato nell'esempio 2 modifica la dimensione massima del file ETL per tutte le impostazioni di configurazione della registrazione centralizzata in uso nell'organizzazione. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsClsConfiguration** per restituire una raccolta di tutte le impostazioni di registrazione centralizzata. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsClsConfiguration**, che modifica il valore della proprietà EtlRolloverFileSizeMB di ogni elemento della raccolta impostandolo su 40 MB.

    Get-CsClsConfiguration | Set-CsClsConfiguration -EtlRolloverFileSizeMB 40

## Descrizione dettagliata

Il servizio di registrazione centralizzata, che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010, consente agli amministratori di gestire la registrazione e la traccia per tutti i computer e i pool che eseguono Lync Server 2013. La registrazione centralizzata consente agli amministratori di arrestare, avviare e configurare la registrazione per uno o più pool e computer utilizzando un solo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del servizio Rubrica in tutti i server della Rubrica. Questo comportamento è diverso rispetto agli strumenti OCSLogger e OCSTracer, che devono essere gestiti singolarmente (avviati e arrestati individualmente) in ogni server. Il servizio di registrazione centralizzata inoltre consente agli amministratori di eseguire ricerche nei log di traccia dal comando utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

La registrazione centralizzata si basa su una serie di scenari predefiniti che offrono un approccio più mirato alla registrazione rispetto alle versioni precedenti di Lync Server. Tali scenari prevedono componenti server e registrazione predefiniti per l'utente e di conseguenza un amministratore che abilita lo scenario RGS può essere sicuro che registrerà solo informazioni dei log rilevanti per il servizio Response Group e non, ad esempio, per il servizio del provider di servizi di audioconferenza.

È anche possibile definire scenari personalizzati utilizzando il cmdlet [New-CsClsScenario](new-csclsscenario.md).

La registrazione centralizzata viene gestita utilizzando raccolte di impostazioni di configurazione del servizio di registrazione centralizzata. Quando si installa Lync Server 2013, viene installato un insieme globale di queste impostazioni di configurazione. Gli amministratori possono inoltre aggiungere raccolte di impostazioni personalizzate nell'ambito del sito, nonché utilizzare il cmdlet **Set-CsClsConfiguration** per modificare tali impostazioni.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsClsConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Set-CsClsConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>CacheFileLocalFolders</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Uno o più percorsi completi delle cartelle locali in cui verranno archiviati i file di cache. Il valore predefinito è %TEMP%\Tracing. Se vengono specificati più percorsi, separarli con punto e virgola.</p></td>
</tr>
<tr class="even">
<td><p><em>CacheFileLocalMaxDiskUsage</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Quantità massima di spazio su disco (in percentuale) utilizzabile per i file della cache. Il valore predefinito è 80.</p></td>
</tr>
<tr class="odd">
<td><p><em>CacheFileLocalRetentionPeriod</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Numero massimo di giorni durante i quali i file della cache vengono conservati in locale. Il valore predefinito è 14.</p></td>
</tr>
<tr class="even">
<td><p><em>CacheFileNetworkFolder</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Percorso UNC completo della cartella della cache di rete. Non è previsto alcun valore predefinito.</p></td>
</tr>
<tr class="odd">
<td><p><em>ComponentThrottleLimit</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Velocità massima a cui un componente può generare record di traccia prima che la traccia venga limitata. Il valore predefinito è 5000 chiamate di traccia al secondo.</p>
<p>Il valore predefinito è 5000.</p></td>
</tr>
<tr class="even">
<td><p><em>ComponentThrottleSample</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Numero massimo di volte il cui è possibile superare il ComponentThrottleLimit entro un intervallo di un minuto. Il valore predefinito è 3.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>EtlFileFolder</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Percorso completo della cartella in cui verranno archiviati di file di traccia del registro eventi. Il valore predefinito è %TEMP%\Tracing. Si noti che %TEMP% viene valutato nei contenuti del servizio CLS in modo che venga effettivamente espanso in %WINDIR%\ServiceProfiles\NetworkService\AppData\Local.</p></td>
</tr>
<tr class="odd">
<td><p><em>EtlFileRolloverMinutes</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Massimo intervallo di tempo (espresso in minuti) che può trascorrere prima che venga creato un nuovo file di traccia del registro eventi. Tale nuovo file verrà creato anche se il file di traccia esistente non ha raggiunto la dimensione di rollover specificata. Il valore predefinito è 60.</p></td>
</tr>
<tr class="even">
<td><p><em>EtlFileRolloverSizeMB</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Dimensione massima (in MB) che un file di log traccia eventi può raggiungere prima che venga creato un nuovo file. Il valore predefinito è 20.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni di configurazione della registrazione centralizzata da modificare. Per fare riferimento alle impostazioni globali, utilizzare la sintassi seguente:</p>
<p>-Identity global</p>
<p>Per fare riferimento alle impostazioni del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity site:Redmond</p>
<p>Non è possibile utilizzare caratteri jolly per specificare il parametro Identity.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Consente di passare un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>MinimumClsAgentServiceVersion</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Specifica la versione minima dell'agente del servizio di registrazione centralizzata da utilizzare per la registrazione dei dati. Tutti i computer con una versione inferiore a quella minima verranno esclusi dalle operazioni di registrazione. Il valore predefinito è 6, che indicaLync Server 2013. Questo parametro è destinato principalmente all'utilizzo con Skype for Business online.</p></td>
</tr>
<tr class="odd">
<td><p><em>Regions</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Raccolta di aree definite per le impostazioni di configurazione della registrazione centralizzata. Tali aree vengono definite utilizzando il cmdlet New-CsClsRegion.</p>
<p>Questo parametro è destinato all'utilizzo con Skype for Business online.</p></td>
</tr>
<tr class="even">
<td><p><em>Scenarios</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Raccolta di componenti/situazioni che è possibile tracciare utilizzando la registrazione centralizzata. Gli scenari vengono gestiti mediante i cmdlet <strong>CsClsScenario</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>SearchTerms</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Raccolta di termini utili per stabilire le informazioni che consentono di identificare l'utente, disponibili per il personale del supporto tecnico che effettua ricerche nei file di registrazione centralizzata. I termini di ricerca vengono gestiti mediante i cmdlet <strong>CsClsSearchTerm</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>SecurityGroups</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Gruppi di sicurezza ai quali è consentito l'accesso ai file di log.</p>
<p>Questo parametro è destinato all'utilizzo con Skype for Business online.</p></td>
</tr>
<tr class="odd">
<td><p><em>TmfFileSearchPath</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Percorso di ricerca per i file TMF (Trace Message Format). Tali file convertono i messaggi di traccia binari in un formato leggibile.</p></td>
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

Il cmdlet **Set-CsClsConfiguration** accetta istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.CentralizedLoggingConfiguration inviato tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsClsConfiguration** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.CentralizedLoggingConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsClsConfiguration](get-csclsconfiguration.md)  
[New-CsClsConfiguration](new-csclsconfiguration.md)  
[Remove-CsClsConfiguration](remove-csclsconfiguration.md)

