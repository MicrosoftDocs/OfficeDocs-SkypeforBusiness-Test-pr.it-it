---
title: Invoke-CsCdrDatabasePurge
TOCTitle: Invoke-CsCdrDatabasePurge
ms:assetid: 95eb0faf-49dc-4afb-b98c-15735a4cab13
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205113(v=OCS.15)
ms:contentKeyID: 49301374
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Invoke-CsCdrDatabasePurge

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Elimina manualmente i record dal database di registrazione dettagli chiamata (CDR). Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Invoke-CsCdrDatabasePurge -Identity <XdsIdentity> <COMMON PARAMETERS>

    Invoke-CsCdrDatabasePurge -SqlServerFqdn <String> [-SqlInstanceName <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -PurgeCallDetailDataOlderThanDays <Int32> -PurgeDiagnosticDataOlderThanDays <Int32> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 elimina dal database di monitoraggio atl-sql-001.litwareinc.com tutti i record (sia dei dettagli chiamata sia dei dati diagnostici) che hanno più di 10 giorni.

    Invoke-CsCdrDatabasePurge -Identity "service:MonitoringDatabase:atl-sql-001.litwareinc.com" -PurgeCallDetailDataOlderThanDays 10 -PurgeDiagnosticDataOlderThanDays 10

## Esempio 2

Il comando riportato nell'esempio 2 è una variante del comando riportato nell'esempio 1. In questo caso tuttavia viene aggiunto il parametro Confirm utilizzando la sintassi seguente:

\-Confirm:$False

Tale sintassi consente di evitare le richieste di conferma che verrebbero altrimenti visualizzate durante l'eliminazione dei record CDR.

    Invoke-CsCdrDatabasePurge -Identity "service:MonitoringDatabase:atl-sql-001.litwareinc.com" -PurgeCallDetailDataOlderThanDays 10 -PurgeDiagnosticDataOlderThanDays 10 -Confirm:$False

## Esempio 3

Nell'esempio 3 vengono eliminati tutti i record creati da più di 10 giorni da tutti i database CDR in uso nell'organizzazione. A tale scopo, nel primo comando dell'esempio vengono utilizzati il cmdlet **Get-CsService** e il parametro MonitoringDatabase per restituire una raccolta di tutti i database di monitoraggio. La raccolta viene quindi inviata tramite pipe al cmdlet **ForEach-Object**. A sua volta il cmdlet **ForEach-Object** seleziona ogni database della raccolta e quindi esegue su di esso il cmdlet **Invoke-CsCdrDatabasePurge**, eliminando tutte le registrazioni dettagli chiamata create da più di 10 giorni.

    Get-CsService -MonitoringDatabase | ForEach-Object {Invoke-CsCdrDatabasePurge -Identity $_.Identity -PurgeCallDetailDataOlderThanDays 10 -PurgeDiagnosticDataOlderThanDays 10 -Confirm:$False}

## Descrizione dettagliata

La registrazione dettagli chiamata consente di tenere traccia dell'utilizzo di funzionalità di Lync Server quali chiamate telefoniche VoIP, messaggistica istantanea, trasferimenti di file, conferenze audio/video (A/V) e sessioni di condivisione applicazioni. Con la registrazione dettagli chiamata vengono registrate informazioni sull'utilizzo, come le parti coinvolte nella chiamata, la durata della chiamata, se sono stati trasferiti file e così via. Non viene tuttavia registrata la chiamata stessa.

Con la registrazione dettagli chiamata inoltre viene tenuta traccia delle informazioni relative a errori delle chiamate, ovvero dati di diagnostica dettagliati sia per le sessioni peer-to-peer che per le chiamate al servizio di conferenza.

La registrazione dettagli chiamata viene archiviata nel database di SQL Server LcsCDR. Poiché nel tempo è possibile che questo database raggiunga dimensioni elevate, in Lync Server sono disponibili per gli amministratori due modi per eliminare i record meno recenti dal database: 1) è possibile configurare Lync Server in modo che i dati di registrazione dettagli chiamata meno recenti vengano eliminati automaticamente ogni giorno e/o 2) è possibile utilizzare il cmdlet **Invoke-CsCdrDatabasePurge** in qualsiasi momento per eliminare i dati di registrazione dettagli chiamata dal database LcsCDR. A tale scopo, il cmdlet **Invoke-CsCdrDatabasePurge** chiama la stored procedure di SQL Server RtcCleanupDB.

Quando si chiama il cmdlet **Invoke-CsCdrDatabasePurge**, è necessario specificare la posizione del servizio del database di monitoraggio in cui sono archiviati i dati di registrazione dettagli chiamata, ad esempio MonitoringDatabase:atl-sql-001.litwareinc.com. È necessario inoltre indicare la durata minima (in giorni) dei dati di diagnostica e dei dettagli chiamata da eliminare. Se ad esempio si specifica una durata minima di 10 giorni per la registrazione dettagli chiamata, verranno eliminati dal database tutti i record creati da più di 10 giorni.

Questi record verranno eliminati anche se per il database specificato è stata disabilitata l'eliminazione, ovvero se nelle impostazioni di configurazione della registrazione dettagli chiamata la proprietà EnablePurging è stata impostata su False. La proprietà EnablePurging controlla solo l'eliminazione automatica della registrazione dettagli chiamata e non ha effetto sul cmdlet **Invoke-CsCdrDatabasePurge**.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Invoke-CsCdrDatabasePurge"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Invoke-CsCdrDatabasePurge** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Identità del servizio del database di monitoraggio da eliminare. È possibile recuperare le identità dei database di monitoraggio eseguendo questo comando:</p>
<p>Get-CsService –MonitoringDatabase</p>
<p>Si noti che non è possibile utilizzare i parametri Identity e SqlServerFqdn nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>PurgeCallDetailDataOlderThanDays</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Int32</p></td>
<td><p>Specifica la validità (in giorni) delle registrazioni dettagli chiamata da eliminare dal database. Verrà eliminato qualsiasi record meno recente di tale valore. Le registrazioni dettagli chiamata rappresentano rapporti su utenti/sessioni. Si differenziano dai rapporti con dati diagnostici, che sono invece log diagnostici caricati da applicazioni client come Lync 2013.</p>
<p>PurgeCallDetailDataOlderThanDays può essere impostato su qualsiasi valore intero compreso tra 1 e 2147483647 (inclusi).</p></td>
</tr>
<tr class="odd">
<td><p><em>PurgeDiagnosticDataOlderThanDays</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Int32</p></td>
<td><p>Specifica l'età (in giorni) dei record dei dati diagnostici da eliminare dal database. Verrà eliminato qualsiasi record più vecchio di tale valore. I rapporti con i dati diagnostici sono log diagnostici caricati dalle applicazioni client come Lync 2013.</p>
<p>PurgeDiagnosticDataOlderThanHours può essere impostato su qualsiasi valore intero compreso tra 1 e 2147483647 (inclusi).</p></td>
</tr>
<tr class="even">
<td><p><em>SqlServerFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del computer in cui è contenuto il database di registrazione dettagli chiamata, ad esempio:</p>
<p>-SqlServerFqdn &quot;atl-sql-001.litwareinc.com&quot;</p>
<p>Si noti che non è possibile utilizzare i parametri Identity e SqlServerFqdn nello stesso comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>SqlInstanceName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome dell'istanza di SQL Server per il database di registrazione dettagli chiamata, ad esempio:</p>
<p>-SqlInstanceName &quot;archinst&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Invoke-CsCdrDatabasePurge** accetta istanze della classe Microsoft.Rtc.Management.Xds.DisplayMonitoringDatabase\#Decorated inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Invoke-CsCdrDatabasePurge** restituisce istanze della classe Microsoft.Rtc.Management.Purge.CdrDataPurgeStatistics.

## Vedere anche

#### Ulteriori risorse

[New-CsCdrConfiguration](new-cscdrconfiguration.md)  
[Set-CsCdrConfiguration](set-cscdrconfiguration.md)

