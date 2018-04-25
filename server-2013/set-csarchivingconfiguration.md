---
title: Set-CsArchivingConfiguration
TOCTitle: Set-CsArchivingConfiguration
ms:assetid: f5202dc2-b3b4-48ae-93d2-d19e71847994
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413030(v=OCS.15)
ms:contentKeyID: 49302491
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsArchivingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta esistente di impostazioni di archiviazione della messaggistica istantanea. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsArchivingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsArchivingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ArchiveDuplicateMessages <$true | $false>] [-BlockOnArchiveFailure <$true | $false>] [-CachePurgingInterval <UInt32>] [-Confirm [<SwitchParameter>]] [-EnableArchiving <None | ImOnly | ImAndWebConf>] [-EnableExchangeArchiving <$true | $false>] [-EnablePurging <$true | $false>] [-Force <SwitchParameter>] [-KeepArchivingDataForDays <UInt32>] [-PurgeExportedArchivesOnly <$true | $false>] [-PurgeHourOfDay <UInt32>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1, il cmdlet **Set-CsArchivingConfiguration** viene utilizzato per modificare due proprietà delle impostazioni di configurazione dell'archiviazione con identità site:Redmond. Il comando imposta prima la proprietà ArchiveDuplicateMessages su False per impedire che il server archivi la stessa sessione di messaggistica istantanea più volte. Viene utilizzato anche il parametro KeepArchivingDataForDays per configurare il server in modo da conservare i messaggi istantanei per 30 giorni.

    Set-CsArchivingConfiguration -Identity site:Redmond -ArchiveDuplicateMessages $False -KeepArchivingDataForDays 30

## ESEMPIO 2

L'esempio 2 è una variazione del comando mostrato nel primo esempio: in questo caso i valori delle proprietà ArchiveDuplicateMessages e KeepArchivingDataForDays vengono tuttavia modificati per tutte le impostazioni di archiviazione che sono state configurate nell'ambito del sito. Per eseguire questa operazione, il comando utilizza per prima cosa il cmdlet **Get-CsArchivingConfiguration** e il parametro Filter per restituire una raccolta di tutte le impostazioni di archiviazione configurate nell'ambito del sito; il valore di filtro "site:\*" garantisce che vengano restituite solo le impostazioni la cui identità inizia con i caratteri "site:". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsArchivingConfiguration**, che modifica i valori delle due proprietà per ogni elemento nella raccolta.

    Get-CsArchivingConfiguration -Filter "site:*" | Set-CsArchivingConfiguration -ArchiveDuplicateMessages $False -KeepArchivingDataForDays 30

## ESEMPIO 3

Nell'esempio 3, tutte le impostazioni di configurazione dell'archiviazione che consentono l'archiviazione sia delle sessioni di messaggistica istantanea che delle conferenze Web vengono modificate. Quando il comando viene completato, tali impostazioni consentiranno l'archiviazione solo delle sessioni di messaggistica istantanea. Per questo scopo, viene chiamato prima il cmdlet **Get-CsArchivingConfiguration** senza parametri per restituire una raccolta di tutte le impostazioni di configurazione dell'archiviazione attualmente in uso nell'organizzazione. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che sceglie solo le impostazioni in cui la proprietà EnableArchiving è uguale a (-eq) "ImAndWebConf". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsArchivingConfiguration**, che modifica il valore di EnableArchiving in "ImOnly" per ogni elemento della raccolta.

    Get-CsArchivingConfiguration | Where-Object {$_.EnableArchiving -eq "ImAndWebConf"} | Set-CsArchivingConfiguration -EnableArchiving "ImOnly"

## Descrizione dettagliata

Molte organizzazioni trovano utile trascrivere tutte le sessioni di messaggistica istantanea e le conferenze a cui partecipano gli utenti dell'organizzazione. In altri casi tali trascrizioni sono obbligatorie, ad esempio molte organizzazioni del settore finanziario sono tenute per legge a conservare copie di tutte le comunicazioni elettroniche.

Per poter archiviare la messaggistica istantanea, è necessario configurare almeno un server di archiviazione. Una volta configurato il server di archiviazione, è necessario eseguire due passaggi ulteriori. È innanzitutto necessario abilitare l'archiviazione per l'ambito globale (per informazioni dettagliate vedere l'argomento della Guida relativo al cmdlet **Set-CsArchivingConfiguration**). Facoltativamente, è anche possibile configurare le impostazioni di archiviazione personalizzate per altri siti.

In secondo luogo, è necessario utilizzare i criteri di archiviazione per indicare gli utenti le cui sessioni di messaggistica istantanea verranno archiviate. le sessioni di messaggistica istantanea non verranno archiviate se non è presente un criterio che richiede l'archiviazione di tali sessioni.

Quando si installa Lync Server, viene creata automaticamente una raccolta di impostazioni di configurazione dell'archiviazione globali. Per impostazione predefinita, tali impostazioni verranno applicate all'intera organizzazione. In alternativa, è possibile utilizzare il cmdlet **New-CsArchivingConfiguration** per creare impostazioni di configurazione personalizzate per i singoli siti. In entrambi i casi, è possibile utilizzare il cmdlet **Set-CsArchivingConfiguration** per modificare i valori delle proprietà di una raccolta o delle impostazioni di configurazione dell'archiviazione.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsArchivingConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsArchivingConfiguration"}

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
<td><p><em>ArchiveDuplicateMessages</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Specifica la modalità di archiviazione dei messaggi istantanei relativi a più pool. Si consideri un semplice esempio: Davide Garghentini, che ha un account nel pool 1, invia un messaggio istantaneo a Pilar Ackerman, che ha un account nel 2. Pilar, a sua volta, invia una risposta al messaggio istantaneo di Ken. Se ArchiveDuplicateMessages è impostato su False, in base a un algoritmo predefinito la trascrizione della sessione verrà registrata nel pool 1 o nel pool 2, ma non in entrambi. Se ArchiveDuplicateMessages è impostato su True, ovvero il valore predefinito, la trascrizione verrà registrata in entrambi i pool.</p></td>
</tr>
<tr class="even">
<td><p><em>BlockOnArchiveFailure</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, il servizio di messaggistica istantanea verrà sospeso ogni volta che i messaggi istantanei non possono essere archiviati. Se impostato su False, ovvero il valore predefinito, la messaggistica istantanea continuerà anche se non è possibile archiviare i messaggi istantanei.</p></td>
</tr>
<tr class="odd">
<td><p><em>CachePurgingInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica con quale frequenza, in ore, vengono cancellate le trascrizioni quando l'archiviazione non è stata abilitata per nessuno dei partecipanti. Per impostazione predefinita, tutti i gruppi di sessioni di messaggistica istantanea e di conferenze vengono registrati nel momento in cui si svolgono. All'intervallo specificato, il sistema valuta se l'archiviazione è stata abilitata per qualche partecipante delle sessioni. Se viene rilevata una sessione in cui l'archiviazione non è stata abilitata per alcun partecipante, la trascrizione corrispondente verrà eliminata dal database.</p>
<p>La proprietà CachePurgingInterval può essere impostata su qualsiasi valore intero compreso tra 4 e 168, inclusi. Il valore predefinito è 24.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableArchiving</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Archiving.EnableArchiving</p></td>
<td><p>Indica quali termini vengono salvati nel database di archiviazione. I valori validi sono:</p>
<p>None. Nessun elemento viene archiviato nel database. Questo è il valore predefinito.</p>
<p>ImOnly. Le sessioni di messaggistica istantanea vengono archiviate nel database.</p>
<p>ImAndWebConf. Sia le sessioni di messaggistica istantanea che quelle di conferenze Web vengono archiviate nel database.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableExchangeArchiving</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando è impostato su True, le trascrizioni di conferenze e messaggi immediati di Lync Server 2013 vengono archiviate in Microsoft Exchange Server 2013 anziché in database di SQL Server separato. Notare che se si abilita l'archiviazione di Exchange, gli utenti verranno gestiti dai criteri di archiviazione di Exchange anziché dai criteri di archiviazione di Lync Server 2013.</p>
<p>Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePurging</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, i messaggi istantanei archiviati verranno rimossi periodicamente dal database, nei seguenti casi: 1) i messaggi istantanei risalgono a una data precedente al valore specificato nella proprietà KeepArchivingDataForDays; oppure 2) sono stati esportati e contrassegnati per l'eliminazione.</p>
<p>Se impostato su False, i messaggi istantanei non verranno eliminati automaticamente dal database.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Rappresenta l'identificatore univoco della raccolta di impostazioni di archiviazione da modificare. Per modificare le impostazioni globali, escludere questo parametro o utilizzare la sintassi seguente: -Identity global. Per modificare le impostazioni nell'ambito del sito, utilizzare il prefisso &quot;site:&quot; seguito dal nome del sito. Ad esempio: -Identity &quot;site:Redmond&quot;.</p>
<p>Per modificare le impostazioni assegnate a un singolo pool di registrazione (funzionalità disponibile solo in Lync Server 2013), utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto ArchivingSettings</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>KeepArchivingDataForDays</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Numero di giorni, compreso tra 1 e 2562, durante i quali i messaggi istantanei vengono conservati nel database prima di essere eliminati automaticamente. Il valore predefinito è 14.</p>
<p>Questa proprietà viene applicata solo se EnablePurging è impostato su True.</p></td>
</tr>
<tr class="even">
<td><p><em>PurgeExportedArchivesOnly</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, verranno cancellati solo i messaggi istantanei che sono stato esportati, e pertanto contrassegnati per l'eliminazione. I messaggi istantanei che non sono stati esportati resteranno nel database, anche se risalgono a una data precedente al valore specificato nella proprietà KeepArchivingDataForDays.</p></td>
</tr>
<tr class="odd">
<td><p><em>PurgeHourOfDay</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il momento del giorno in cui i record scaduti vengono eliminati dal database di archiviazione. L'ora del giorno viene specificata nel formato 24 ore; 0 rappresenta la mezzanotte, 23 rappresenta le 11 di sera. È possibile specificare solo l'ora del giorno. Pertanto è possibile pianificare la cancellazione per le 4.00 ma non per le 4.30 o le 4.15. Il valore predefinito è 2 (2.00).</p>
<p>La cancellazione del database si verifica solo se la proprietà EnablePurging è impostata su True.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Archiving.ArchivingSettings. Il cmdlet **Set-CsArchivingConfiguration** accetta input inviato tramite pipe degli oggetti di configurazione dell'archiviazione.

## Tipi restituiti

Il cmdlet **Set-CsArchivingConfiguration** non restituisce un valore o un oggetto. Il cmdlet configura invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Archiving.ArchivingSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsArchivingConfiguration](get-csarchivingconfiguration.md)  
[New-CsArchivingConfiguration](new-csarchivingconfiguration.md)  
[Remove-CsArchivingConfiguration](remove-csarchivingconfiguration.md)  
[Set-CsArchivingServer](set-csarchivingserver.md)

