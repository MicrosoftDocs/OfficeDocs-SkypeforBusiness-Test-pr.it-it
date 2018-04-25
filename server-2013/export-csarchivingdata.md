---
title: Export-CsArchivingData
TOCTitle: Export-CsArchivingData
ms:assetid: 644bf86e-0e7e-4607-bedf-d491b1c16745
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398452(v=OCS.15)
ms:contentKeyID: 49300792
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Export-CsArchivingData

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di esportare i record archiviati nel database di archiviazione di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Export-CsArchivingData -DBInstance <String> -Identity <XdsIdentity> <COMMON PARAMETERS>

    Export-CsArchivingData -Identity <XdsIdentity> <COMMON PARAMETERS>

    Export-CsArchivingData -DBInstance <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: -OutputFolder <String> -StartDate <DateTime> [-Confirm [<SwitchParameter>]] [-EndDate <DateTime>] [-ExcludeWebConfArchive <SwitchParameter>] [-Force <SwitchParameter>] [-IncludeTrustedApplication <SwitchParameter>] [-Purge <SwitchParameter>] [-UserUri <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 estrae i record dal database di archiviazione contenuto nel server atl-sql-001.litwareinc.com quindi salva il file EML risultante nella cartella C:\\ArchivingExports. La data di inizio specificata del 1° giugno 2012 (-StartDate 6/1/2012) garantisce l'esportazione dei soli elementi registrati nel database dopo il 31/05/2012.

    Export-CsArchivingData -Identity "ArchivingDatabase:atl-sql-001.litwareinc.com" -StartDate 6/1/2012 -OutputFolder "C:\ArchivingExports"

## ESEMPIO 2

L'esempio 2 è una variante del comando riportato nell'esempio 1. In questo caso però vengono esportati solo i record relativi all'utente Ken Myer. Per limitare l'esportazione ai record relativi a un singolo utente, includere il parametro UserUri seguito dall'indirizzo SIP appropriato.

    Export-CsArchivingData -Identity "ArchivingDatabase:atl-sql-001.litwareinc.com" -StartDate 6/1/2012 -OutputFolder "C:\ArchivingExports" -UserUri "kenmyer@litwareinc.com"

## ESEMPIO 3

Nell'esempio 3 viene presentata un'altra variante del comando riportato nell'esempio 1. Nell'esempio 3 però vengono esportati solo gli elementi registrati nel database nel mese di giugno 2012. Per limitare l'esportazione a questo intervallo di tempo, viene incluso il parametro EndDate insieme al parametro StartDate. Utilizzando il 1° giugno 2012 come data di inizio e il 30 giugno 2012 come data di fine, l'esportazione viene effettivamente limitata agli elementi registrati nel mese di giugno 2012.

    Export-CsArchivingData -Identity "ArchivingDatabase:atl-sql-001.litwareinc.com" -StartDate 6/1/2012 -EndDate 6/30/2012 -OutputFolder "C:\ArchivingExports"

## Descrizione dettagliata

Molte organizzazioni trovano utile conservare una trascrizione di tutte le sessioni di messaggistica istantanea svolte dagli utenti. Altre organizzazioni sono obbligate a conservare tali trascrizioni. Ad esempio, molte organizzazioni che operano nel settore finanziario sono obbligate per legge a mantenere copie di tutte le proprie comunicazioni elettroniche.

Indipendentemente dalla ragione, Lync Server offre una notevole flessibilità quando si tratta di archiviare le sessioni di messaggistica istantanea e di conferenza. Se è stato distribuito il server di archiviazione, è possibile utilizzare i diversi cmdlet **CsArchivingConfiguration** per abilitare e disabilitare l'archiviazione di messaggi istantanei e per gestire il database di archiviazione. È inoltre possibile sospendere la messaggistica istantanea in caso di errori di archiviazione, in modo tale da garantire la conservazione di una registrazione di tutte le comunicazioni elettroniche.

Se è stata abilitata l'archiviazione, i record delle comunicazioni elettroniche degli utenti sono archiviati nel database di archiviazione. Se si desidera visualizzare tutti questi record (o un subset selezionato di questi record), è possibile utilizzare il cmdlet **Export-CsArchivingData** per estrarre tali record dal database e salvarli come file EML (Electronic Mail) di Outlook Express.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Export-CsArchivingData** in locale: RTCComponentUniversalServices. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Export-CsArchivingData"}

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
<td><p><em>DBInstance</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Percorso dell'istanza del database SQL Server in cui vengono registrati i dati di archiviazione. Ad esempio: &quot;atl-sql-001\Archinst&quot;.</p>
<p>Questo parametro può essere utilizzato solo con Microsoft Lync Server 2010. Se si utilizza il cmdlet <strong>Export-CsArchivingData</strong> in Lync Server 2013, utilizzare invece il parametro Identity.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identità del servizio del database di archiviazione da esportare, ad esempio:</p>
<p>-Identity &quot;ArchivingDatabase:atl-sql-001.litwareinc.com&quot;</p>
<p>È inoltre possibile specificare il database utilizzando il nome di pool:</p>
<p>-Identity &quot;atl-sql-001.litwareinc.com&quot;</p>
<p>È possibile recuperare le identità del servizio dei database di archiviazione utilizzando il comando seguente:</p>
<p>Get-CsService –ArchivingDatabase | Select-Object Identity</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputFolder</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Percorso completo della cartella in cui devono essere archiviati i dati esportati, ad esempio C:\ArchivingExports. Se la cartella non esiste, viene creata dal cmdlet <strong>Export-CsArchivingData</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>StartDate</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.DateTime</p></td>
<td><p>Indica la data dell'attività meno recente per i record da esportare. Ad esempio, se si imposta la data di avvio sul 6/1/2010 (1 giugno 2010 in inglese americano), qualsiasi elemento registrato nel database prima di quella data (ad esempio gli elementi registrati il 31 maggio 2010) sarà escluso dall'esportazione.</p>
<p>Per l'assegnazione dei valori alle proprietà StartDate ed EndDate, utilizzare i formati data/ora specificati nelle impostazioni internazionali e della lingua.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>EndDate</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.DateTime</p></td>
<td><p>Indica la data dell'attività più recente per i record da esportare. Ad esempio, se si imposta la data di fine sul 6/1/2010 (1 giugno 2010 in inglese americano), qualsiasi elemento registrato nel database dopo quella data (ad esempio gli elementi registrati il 2 giugno 2010) sarà escluso dall'esportazione. Anche se non viene visualizzato un messaggio di errore, l'esportazione non riesce se la data di fine è precedente alla data di inizio (ad esempio se la data di fine è 1/1/2010 e la data di inizio è 6/1/2010).</p>
<p>Per l'assegnazione dei valori alle proprietà StartDate ed EndDate, utilizzare i formati data/ora specificati nelle impostazioni internazionali e della lingua.</p>
<p>Se non viene specificato la data di fine verrà utilizzata la data corrente.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExcludeWebConfArchive</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Indica al cmdlet <strong>Export-CsArchivingData</strong> di esportare solo i record di messaggistica istantanea. Per impostazione predefinita, il cmdlet esporta sia i record dei messaggi istantanei sia i record delle conferenze.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>IncludeTrustedApplication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Quando incluso, indica al cmdlet <strong>Export-CsArchivingData</strong> di includere i dati registrati dalle applicazioni attendibili quando vengono esportati i record.</p></td>
</tr>
<tr class="even">
<td><p><em>Purge</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se incluso, il parametro Purge fa sì che i record esportati correttamente vengano eliminati dal database di archiviazione. Se non si include questo parametro, i record esportati saranno conservati nel database.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di esportare i dati di archiviazione per un singolo utente; questa operazione viene eseguita con il parametro UserUri e specificando l'indirizzo SIP dell'utente. Il parametro UserUri accetta solamente un URI per volta.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
<tr class="odd">
<td><p><em>DBInstance</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Percorso dell'istanza del database SQL Server in cui vengono registrati i dati di archiviazione. Ad esempio: &quot;atl-sql-001\Archinst&quot;.</p>
<p>Questo parametro può essere utilizzato solo con Microsoft Lync Server 2010. Se si utilizza il cmdlet <strong>Export-CsArchivingData</strong> in Lync Server 2013, utilizzare invece il parametro Identity.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identità del servizio del database di archiviazione da esportare, ad esempio:</p>
<p>-Identity &quot;ArchivingDatabase:atl-sql-001.litwareinc.com&quot;</p>
<p>È inoltre possibile specificare il database utilizzando il nome di pool:</p>
<p>-Identity &quot;atl-sql-001.litwareinc.com&quot;</p>
<p>È possibile recuperare le identità del servizio dei database di archiviazione utilizzando il comando seguente:</p>
<p>Get-CsService –ArchivingDatabase | Select-Object Identity</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputFolder</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Percorso completo della cartella in cui devono essere archiviati i dati esportati, ad esempio C:\ArchivingExports. Se la cartella non esiste, viene creata dal cmdlet <strong>Export-CsArchivingData</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>StartDate</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.DateTime</p></td>
<td><p>Indica la data dell'attività meno recente per i record da esportare. Ad esempio, se si imposta la data di avvio sul 6/1/2010 (1 giugno 2010 in inglese americano), qualsiasi elemento registrato nel database prima di quella data (ad esempio gli elementi registrati il 31 maggio 2010) sarà escluso dall'esportazione.</p>
<p>Per l'assegnazione dei valori alle proprietà StartDate ed EndDate, utilizzare i formati data/ora specificati nelle impostazioni internazionali e della lingua.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>EndDate</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.DateTime</p></td>
<td><p>Indica la data dell'attività più recente per i record da esportare. Ad esempio, se si imposta la data di fine sul 6/1/2010 (1 giugno 2010 in inglese americano), qualsiasi elemento registrato nel database dopo quella data (ad esempio gli elementi registrati il 2 giugno 2010) sarà escluso dall'esportazione. Anche se non viene visualizzato un messaggio di errore, l'esportazione non riesce se la data di fine è precedente alla data di inizio (ad esempio se la data di fine è 1/1/2010 e la data di inizio è 6/1/2010).</p>
<p>Per l'assegnazione dei valori alle proprietà StartDate ed EndDate, utilizzare i formati data/ora specificati nelle impostazioni internazionali e della lingua.</p>
<p>Se non viene specificato la data di fine verrà utilizzata la data corrente.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExcludeWebConfArchive</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Indica al cmdlet <strong>Export-CsArchivingData</strong> di esportare solo i record di messaggistica istantanea. Per impostazione predefinita, il cmdlet esporta sia i record dei messaggi istantanei sia i record delle conferenze.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>IncludeTrustedApplication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Quando incluso, indica al cmdlet <strong>Export-CsArchivingData</strong> di includere i dati registrati dalle applicazioni attendibili quando vengono esportati i record.</p></td>
</tr>
<tr class="even">
<td><p><em>Purge</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se incluso, il parametro Purge fa sì che i record esportati correttamente vengano eliminati dal database di archiviazione. Se non si include questo parametro, i record esportati saranno conservati nel database.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di esportare i dati di archiviazione per un singolo utente; questa operazione viene eseguita con il parametro UserUri e specificando l'indirizzo SIP dell'utente. Il parametro UserUri accetta solamente un URI per volta.</p></td>
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

Nessuno. Il cmdlet **Export-CsArchivingData** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Export-CsArchivingData** restituisce i record del database di archiviazione in formato EML.

## Vedere anche

#### Ulteriori risorse

[Get-CsArchivingConfiguration](get-csarchivingconfiguration.md)

