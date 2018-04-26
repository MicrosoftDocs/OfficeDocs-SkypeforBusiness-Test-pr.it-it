---
title: New-CsArchivingConfiguration
TOCTitle: New-CsArchivingConfiguration
ms:assetid: 66cab8b7-c3b3-4c1b-a77a-28f295ff6010
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398471(v=OCS.15)
ms:contentKeyID: 49300818
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsArchivingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo insieme di impostazioni di archiviazione per la messaggistica istantanea. È possibile utilizzare queste impostazioni per abilitare o disabilitare il salvataggio automatico delle sessioni di messaggistica istantanea. Queste impostazioni consentono inoltre di bloccare i messaggi istantanei che non possono essere archiviati. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsArchivingConfiguration -Identity <XdsIdentity> [-ArchiveDuplicateMessages <$true | $false>] [-BlockOnArchiveFailure <$true | $false>] [-CachePurgingInterval <UInt32>] [-Confirm [<SwitchParameter>]] [-EnableArchiving <None | ImOnly | ImAndWebConf>] [-EnableExchangeArchiving <$true | $false>] [-EnablePurging <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-KeepArchivingDataForDays <UInt32>] [-PurgeExportedArchivesOnly <$true | $false>] [-PurgeHourOfDay <UInt32>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di creare una nuova raccolta di impostazioni di archiviazione e di applicarle al sito Redmond. Se si aggiunge il parametro EnableArchiving e lo si imposta su "ImOnly", il comando abilita anche l'archiviazione delle sessioni di messaggistica istantanea (ma non delle sessioni di conferenza via Web) per il sito Redmond.

    New-CsArchivingConfiguration -Identity site:Redmond -EnableArchiving "ImOnly"

## ESEMPIO 2

Nell'esempio 2 viene illustrato l'utilizzo del parametro InMemory per creare una raccolta di impostazioni di configurazione dell'archiviazione inizialmente presenti solo in memoria. A tale scopo, nell'esempio viene creata una nuova raccolta di impostazioni (con Identity site:Redmond) che viene archiviata in una variabile denominata $x. Si noti che, dopo l'esecuzione del primo comando, la raccolta è presente solo in memoria. Se si esegue il cmdlet **Get-CsArchivingConfiguration**, non sarà possibile visualizzare alcuna voce per site:Redmond.

Nel secondo comando la proprietà EnableArchiving per questa raccolta virtuale viene impostata su "ImOnly" e ciò consente l'archiviazione della sessione di messaggistica istantanea. L'ultimo comando infine utilizza il cmdlet **Set-CsArchivingConfiguration** per trasformare le impostazioni di archiviazione virtuali in una raccolta di impostazioni effettive applicate al sito Redmond. Se non si chiama il cmdlet **Set-CsArchivingConfiguration**, queste impostazioni rimangono solo nella memoria e pertanto sono destinate a scomparire al termine della sessione di Windows PowerShell o se la variabile $x viene eliminata.

    $x = New-CsArchivingConfiguration -Identity site:Redmond -InMemory
    $x.EnableArchiving = "ImOnly"
    Set-CsArchivingConfiguration -Instance $x

## Descrizione dettagliata

Molte organizzazione ritengono utile conservare una trascrizione di tutte le sessioni di messaggistica istantanea effettuate dai loro utenti. Per altre organizzazioni, è obbligatorio conservare tali trascrizioni; ad esempio, molte organizzazioni del settore finanziario sono obbligate per legge a conservare copia di tutte le loro comunicazioni elettroniche.

Lync Server garantisce la massima flessibilità nell'archiviazione delle sessioni di messaggistica istantanea e delle conferenze Web. Se è stato distribuito il server di archiviazione, è possibile utilizzare i diversi cmdlet **CsArchivingConfiguration** per abilitare e disabilitare l'archiviazione delle sessioni di messaggistica istantanea e per gestire il database di archiviazione. Se l'archiviazione non dovesse riuscire, è inoltre possibile interrompere la messaggistica istantanea. Questo consente di conservare una registrazione di tutte le comunicazioni elettroniche.

Quando si installa Lync Server, viene creata automaticamente una raccolta di impostazioni di archiviazione globale. Queste impostazioni verranno applicate all'intera organizzazione per impostazione predefinita. In alternativa, è possibile utilizzare il cmdlet **New-CsArchivingConfiguration** per creare impostazioni di configurazione personalizzate sito per sito.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsArchivingConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsArchivingConfiguration"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco da assegnare alla nuova raccolta di impostazioni di archiviazione. In Lync Server 2013 è possibile creare nuove raccolte nell'ambito del sito o del servizio, mentre in Microsoft Lync Server 2010 queste impostazioni possono essere create solo nell'ambito del sito. Per creare nuove impostazioni nell'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>Per creare impostazioni nell'ambito del servizio (solo per il servizio di Registrazione avanzata), utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>ArchiveDuplicateMessages</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Consente di specificare il metodo di archiviazione dei messaggi istantanei scambiati tra pool diversi. Ad esempio, Ken Myer (con un account in Pool 1) invia un messaggio istantaneo a Pilar Ackerman (che ha un account in Pool 2). Pilar, a sua volta, invia una risposta al messaggio istantaneo di Ken. Se ArchiveDuplicateMessages è impostato su False, la trascrizione della sessione (in base a un algoritmo predefinito) viene registrata nel Pool 1 o nel Pool 2, ma non in entrambi. Se ArchiveDuplicateMessages è impostato su True (il valore predefinito), la trascrizione verrà registrata in entrambi i pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>BlockOnArchiveFailure</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, il servizio di messaggistica istantanea verrà sospeso ogni volta che le sessioni di messaggistica istantanea non possono essere archiviate. Se impostato su False (il valore predefinito), la messaggistica istantanea continuerà anche se le sessioni non possono essere archiviate.</p></td>
</tr>
<tr class="even">
<td><p><em>CachePurgingInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica la frequenza (in ore) con la quale le trascrizioni vengono cancellate dal sistema, nei casi in cui nessuno dei partecipanti è stato abilitato per l'archiviazione. Per impostazione predefinita, tutte le sessioni di messaggistica istantanea di gruppo e le sessioni di conferenza vengono registrate nel momento in cui hanno luogo. All'intervallo di tempo specificato, il sistema stabilisce se qualcuno dei partecipanti a queste sessioni è stato abilitato per l'archiviazione. Se il sistema rileva una sessione nella quale nessuno dei partecipanti è stato abilitato per l'archiviazione, la relativa trascrizione viene cancellata dall'archivio.</p>
<p>La proprietà CachePurgeInterval può essere impostata su qualsiasi numero intero compreso tra 4 e 168, inclusi. Il valore predefinito è 24.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableArchiving</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Archiving.EnableArchiving</p></td>
<td><p>Indica quali elementi (qualora ve ne siano) devono essere salvati nell'archivio. I valori validi sono:</p>
<p>None. Nessun elemento viene salvato nell'archivio. Questo è il valore predefinito.</p>
<p>ImOnly. Le sessioni di messaggistica istantanea vengono salvate nell'archivio.</p>
<p>ImAndWebConf. Vengono archiviate sia le sessioni di messaggistica istantanea sia le sessioni di conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableExchangeArchiving</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, le trascrizioni della messaggistica istantanea e delle conferenze di Lync Server 2013 vengono archiviate in Microsoft Exchange Server 2013 anziché in un database di SQL Server separato. Se si abilita l'archiviazione di Exchange, gli utenti verranno gestiti dai criteri di archiviazione di Exchange e non di Lync Server.</p>
<p>Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePurging</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, i messaggi istantanei archiviati verranno periodicamente rimossi dall'archivio, a condizione che essi: 1) siano precedenti al valore specificato nella proprietà KeepArchivingDataForDays; oppure 2) siano stati esportati e selezionati per l'eliminazione.</p>
<p>Se impostato su False, i messaggi istantanei non verranno automaticamente eliminati dall'archivio.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>KeepArchivingDataForDays</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Il numero di giorni (tra 1 e 2562) per cui i messaggi istantanei vengono conservati nell'archivio prima di essere automaticamente eliminati. Il valore predefinito è 14.</p>
<p>Questa proprietà ha effetto solo se EnablePurging è impostato su True.</p></td>
</tr>
<tr class="even">
<td><p><em>PurgeExportedArchivesOnly</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, il sistema cancella solo i messaggi istantanei che sono stati esportati e, di conseguenza, selezionati per l'eliminazione. I messaggi istantanei che non sono stati esportati rimangono nell'archivio, anche nel caso in cui siano precedenti al valore specificato nella proprietà KeepArchivingDataForDays.</p></td>
</tr>
<tr class="odd">
<td><p><em>PurgeHourOfDay</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica l'ora in cui i record scaduti vengono eliminati dall'archivio. L'ora è specificata nel formato 24 ore, dalle ore 0 (mezzanotte) alle ore 23. Si noti che è possibile specificare solo l'ora. Ciò significa che è possibile pianificare l'eliminazione per 4:00 ma non, ad esempio, alle 4:30 o alle 4:15. Il valore predefinito è 2.</p>
<p>La cancellazione dall'archivio avviene solo la proprietà EnablePurging è impostata su True.</p></td>
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

Nessuno. Il cmdlet **New-CsArchivingConfiguration** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsArchivingConfiguration** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Archiving.ArchivingSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsArchivingConfiguration](get-csarchivingconfiguration.md)  
[Remove-CsArchivingConfiguration](remove-csarchivingconfiguration.md)  
[Set-CsArchivingConfiguration](set-csarchivingconfiguration.md)  
[Set-CsArchivingServer](set-csarchivingserver.md)

