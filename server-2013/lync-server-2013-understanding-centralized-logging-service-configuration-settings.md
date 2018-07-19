---
title: Informazioni sulle impostazioni di configurazione del servizio di registrazione centralizzato
TOCTitle: Informazioni sulle impostazioni di configurazione del servizio di registrazione centralizzato
ms:assetid: 3c34e600-0b91-43dc-b4cc-90b6a70ee12e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688029(v=OCS.15)
ms:contentKeyID: 49887523
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Informazioni sulle impostazioni di configurazione del servizio di registrazione centralizzato

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il servizio di registrazione centralizzato viene configurato per definire le informazioni che deve raccogliere, la modalità di raccolta, la posizione in cui dovrà raccoglierle e le impostazioni del log. Queste impostazioni possono essere definite a livello globale, ovvero per l'intera distribuzione, o a livello di un sito denominato all'interno di una distribuzione. Per tutte le attività di registrazione definite verranno utilizzate le impostazioni adatte all'identità utilizzata per i comandi di avvio, interruzione, scaricamento e ricerca dei log.

## Per visualizzare la configurazione corrente del servizio di registrazione centralizzato

Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

Digitare quanto segue al prompt della riga di comando:

    Get-CsClsConfiguration

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>È possibile limitare o espandere l'ambito delle impostazioni di configurazione restituite definendo <code>-Identity</code> e un ambito come &quot;Site:Redmond&quot; in modo da restituire solo CsClsConfiguration per il sito di Redmond. Per ottenere i dettagli relativi a una determinata parte della configurazione, è possibile memorizzare l'output in un altro cmdlet Windows PowerShell. Per ottenere ad esempio i dettagli sugli scenari definiti nella configurazione per il sito di &quot;Redmond&quot;, digitare: <code>Get-CsClsConfiguration -Identity &quot;site:Redmond&quot; | Select-Object -ExpandPropery Scenarios</code></td>
</tr>
</tbody>
</table>


![Output di esempio di Get-CsClsConfiguration.](images/JJ688029.23f98ddc-fc48-499a-b6c5-752611f2a0b0(OCS.15).jpg "Output di esempio di Get-CsClsConfiguration.")

Il risultato del cmdlet visualizza la configurazione corrente del servizio di registrazione centralizzato.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Impostazione di configurazione</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Identity</strong></p></td>
<td><p>Identifica l'ambito e il nome della configurazione corrente. Esistono una sola configurazione a livello globale e una sola per sito.</p></td>
</tr>
<tr class="even">
<td><p><strong>Scenari</strong></p></td>
<td><p>Elenco di tutti gli scenari definiti per questa configurazione.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SearchTerms</strong></p></td>
<td><p>Termini di ricerca definiti per la configurazione. Office 365, senza distribuzioni locali.</p></td>
</tr>
<tr class="even">
<td><p><strong>SecurityGroups</strong></p></td>
<td><p>Gruppi di sicurezza definiti che controllano gli utenti, ovvero i membri dei gruppi di sicurezza, che possono vedere i computer in base al sito in cui si trovano. Il sito in questo contesto è quello definito nel Generatore di topologie.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Regions</strong></p></td>
<td><p>Le aree definite vengono utilizzate per raccogliere i SecurityGroups in un'area, ad esempio EMEA.</p></td>
</tr>
<tr class="even">
<td><p><strong>EtlFileFolder</strong></p></td>
<td><p>Percorso definito della posizione nei computer in cui vengono scritti i file di log. CLSAgent scrive i file di log e viene eseguito nel contesto del servizio di rete. In tal caso, %TEMP% si espande in %WINDIR%\ServiceProfiles\NetworkService\AppData\Local</p></td>
</tr>
<tr class="odd">
<td><p><strong>EtlFileRolloverSizeMB</strong></p></td>
<td><p>Il parametro indica le dimensioni massime del file di log prima che venga creato un nuovo file di log traccia eventi (.etl). Viene creato un nuovo file di log quando si raggiungono le dimensioni definite anche se non è stato ancora esaurito il tempo massimo impostato in EtlFileRolloverMinutes.</p></td>
</tr>
<tr class="even">
<td><p><strong>EtlFileRolloverMinutes</strong></p></td>
<td><p>Periodo di tempo massimo definito, espresso in minuti, che può trascorrere per un log prima che venga creato un nuovo file con estensione etl. Viene creato un nuovo file di log quando il timer scade anche se non sono ancora state raggiunte le dimensioni massime impostate in EtlFileRolloverSizeMB.</p></td>
</tr>
<tr class="odd">
<td><p><strong>TmfFileSearchPath</strong></p></td>
<td><p>Posizione in cui cercare i file TMF (Trace Message Format). I file TMF vengono utilizzati per convertire i file binari in un formato leggibile.</p></td>
</tr>
<tr class="even">
<td><p><strong>CacheFileLocalFolders</strong></p></td>
<td><p>Percorso definito della posizione nei computer in cui vengono scritti i file di cache. CLSAgent scrive i file di cache e viene eseguito nel contesto del servizio di rete. In questo caso, %TEMP% si espande in %WINDIR%\ServiceProfiles\NetworkService\AppData\Local. Per impostazione predefinita, i file di cache e di log vengono scritti nella stessa directory.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CacheFileNetworkFolder</strong></p></td>
<td><p>È possibile definire un percorso UNC (Universal Naming Convention) per ricevere i file di cache durante le operazioni di registrazione.</p></td>
</tr>
<tr class="even">
<td><p><strong>CacheFileLocalRetentionPeriod</strong></p></td>
<td><p>Definito come tempo massimo, espresso in giorni, di mantenimento dei file di cache.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CacheFileMaxDiskUsage</strong></p></td>
<td><p>Definito come percentuale dello spazio su disco che può essere utilizzato dai file di cache.</p></td>
</tr>
<tr class="even">
<td><p><strong>ComponentThrottleLimit</strong></p></td>
<td><p>Definito come numero massimo di tracce al secondo che un componente può produrre prima che venga attivato il limite di velocità automatico.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ComponentThrottleSample</strong></p></td>
<td><p>Numero di volte nell'arco di 60 secondi in cui è possibile superare ComponentThrottleLimit.</p></td>
</tr>
<tr class="even">
<td><p><strong>MinimumClsAgentServiceVersion</strong></p></td>
<td><p>Versione minima di CLSAgent di cui è consentita l'esecuzione. Questo elemento è destinato a Office 365.</p></td>
</tr>
</tbody>
</table>


## Vedere anche

#### Concetti

[Panoramica del servizio di registrazione centralizzato](lync-server-2013-overview-of-the-centralized-logging-service.md)  

#### Ulteriori risorse

[Set-CsClsConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClsConfiguration)  
[Remove-CsClsConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsClsConfiguration)  
[New-CsClsConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClsConfiguration)  
[Get-CsClsConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsClsConfiguration)

