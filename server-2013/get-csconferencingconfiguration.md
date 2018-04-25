---
title: Get-CsConferencingConfiguration
TOCTitle: Get-CsConferencingConfiguration
ms:assetid: db4ab3bc-071c-4f73-a3a0-62dc8aed48a1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398965(v=OCS.15)
ms:contentKeyID: 49302170
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConferencingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle impostazioni di configurazione delle conferenze dell'organizzazione. Tali impostazioni determinano aspetti quali la dimensione massima consentita per il contenuto e gli stampati delle conferenze, il periodo di tolleranza (ovvero per quanto tempo il contenuto resterà archiviato prima di essere eliminato) e gli URL per i download interni ed esterni del client supportato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsConferencingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsConferencingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituite informazioni su tutte le impostazioni di configurazione per conferenze attualmente in uso nell'organizzazione. A tale scopo, il cmdlet **Get-CsConferencingConfiguration** viene chiamato senza alcun parametro.

    Get-CsConferencingConfiguration

## ESEMPIO 2

Nell'esempio 2 vengono fornite informazioni di configurazione per conferenze per il sito Redmond (-Identity site:Redmond). Poiché le identità devono essere univoche, il comando restituirà al massimo una raccolta di impostazioni di configurazione per conferenze.

    Get-CsConferencingConfiguration -Identity site:Redmond

## ESEMPIO 3

Il comando mostrato nell'esempio 3 restituisce informazioni su tutte le impostazioni di configurazione per conferenze che sono state applicate all'ambito del sito. A tale scopo, il cmdlet **Get-CsConferencingConfiguration** viene chiamato con il parametro Filter. Il valore di filtro "site:\*" garantisce che vengano restituite solo le impostazioni il cui valore Identity inizia con il valore stringa "site:\*".

    Get-CsConferencingConfiguration -Filter "site:*"

## ESEMPIO 4

Nell'esempio 4 vengono restituite informazioni relative a tutte le impostazioni di configurazione per conferenze in cui l'organizzazione non è impostata su Litwareinc. Per eseguire questa attività, viene innanzitutto chiamato il cmdlet **Get-CsConferencingConfiguration** senza alcun parametro. In tal modo, viene restituita una raccolta di tutte le impostazioni di configurazione delle conferenze utilizzate nell'organizzazione. La raccolta risultante viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni la cui proprietà Organization non è uguale a Litwareinc.

    Get-CsConferencingConfiguration | Where-Object {$_.Organization -ne "Litwareinc"}

## ESEMPIO 5

Nell'esempio 5 vengono restituite informazioni relative alle sole impostazioni di configurazione per conferenze in cui lo spazio di archiviazione massimo dei contenuti è maggiore di 100 megabyte. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsConferencingConfiguration** senza alcun parametro per restituire una raccolta di tutte le impostazioni di configurazione delle conferenze. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona le impostazioni in cui lo spazio di archiviazione del contenuto è maggiore di 100 megabyte.

    Get-CsConferencingConfiguration | Where-Object {$_.MaxContentStorageMB -gt 100}

## Descrizione dettagliata

Per le conferenze, la gestione e l'amministrazione vengono controllate da due insiemi di cmdlet distinti. Se si desidera stabilire le operazioni che gli utenti possono o non possono eseguire (ad esempio, se possono invitare partecipanti anonimi a una conferenza oppure offrire la condivisione di applicazioni o trasferire file durante una conferenza), sarà necessario utilizzare i cmdlet **CsConferencingPolicy**.

Oltre alle attività degli utenti, gli amministratori devono gestire il servizio Web Conferencing di Lync Server. Devono ad esempio poter eseguire operazioni quali specificare la quantità massima di spazio di archiviazione del contenuto assegnata a una singola conferenza e il periodo di tolleranza consentito prima dell'eliminazione automatica del contenuto della conferenza. Devono inoltre poter specificare le porte utilizzate per attività quali la condivisione di applicazioni e il trasferimento di file.

Tali attività possono essere gestite tramite i cmdlet **CsConferencingConfiguration**. Questi cmdlet consentono di gestire i server veri e propri. I cmdlet **CsConferencingConfiguration** (che possono essere applicati all'ambito globale, del sito e del servizio) non vengono infatti utilizzati per specificare se un utente può condividere applicazioni durante una conferenza. Se la condivisione delle applicazioni è consentita, tali cmdlet consentono tuttavia di indicare quali porte utilizzare per questa attività. Analogamente, i cmdlet consentono di specificare aspetti quali i limiti di archiviazione e i periodi di scadenza, nonché i puntatori agli URL interni ed esterni da cui gli utenti possono ottenere assistenza e risorse per le conferenze.

Il cmdlet **Get-CsConferencingConfiguration** consente agli amministratori di restituire informazioni relative a tutte le impostazioni di configurazione delle conferenze attualmente in uso nell'organizzazione.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsConferencingConfiguration** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsConferencingConfiguration"}

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
<td><p>Consente di utilizzare i caratteri jolly per specificare l'identità delle impostazioni di configurazione delle conferenze da restituire. Ad esempio, la sintassi che segue restituisce tutte le informazioni configurate nell'ambito del sito: -Filter &quot;site:*&quot;. La seguente sintassi restituisce tutte le impostazioni configurate nell'ambito del servizio: -Filter &quot;service:*&quot;.</p>
<p>Si noti che non è possibile utilizzare i parametri Identity e Filter nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>L'identificatore univoco per la raccolta di impostazioni di configurazione per conferenze da recuperare. Per recuperare le impostazioni globali, utilizzare la seguente sintassi: -Identity global. Per recuperare le impostazioni configurate nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity &quot;site:Redmond&quot;. Per recuperare le impostazioni configurate nell'ambito del servizio, utilizzare una sintassi simile alla seguente: -Identity &quot;service:ConferencingServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>Se questo parametro non viene incluso, il cmdlet <strong>Get-CsConferencingConfiguration</strong> restituirà tutte le impostazioni di configurazione delle conferenze attualmente in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione delle conferenze dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsConferencingConfiguration** non accetta input inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsConferencingConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConfSettings.

## Vedere anche

#### Ulteriori risorse

[New-CsConferencingConfiguration](new-csconferencingconfiguration.md)  
[Remove-CsConferencingConfiguration](remove-csconferencingconfiguration.md)  
[Set-CsConferencingConfiguration](set-csconferencingconfiguration.md)

