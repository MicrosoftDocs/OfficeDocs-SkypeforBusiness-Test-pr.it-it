---
title: Invoke-CsArchivingDatabasePurge
TOCTitle: Invoke-CsArchivingDatabasePurge
ms:assetid: 02310b08-736d-4ce9-91d8-5a6c8f323d7c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204627(v=OCS.15)
ms:contentKeyID: 49299497
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Invoke-CsArchivingDatabasePurge

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Elimina manualmente record dal database di archiviazione. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Invoke-CsArchivingDatabasePurge -Identity <XdsIdentity> <COMMON PARAMETERS>

    Invoke-CsArchivingDatabasePurge -SqlServerFqdn <String> [-SqlInstanceName <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -PurgeArchivingDataOlderThanHours <Int32> -PurgeExportedArchivesOnly <$true | $false> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-MaxArchivingRecordsToDelete <Int32>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 elimina dal database di archiviazione in atl-sql-001.litwareinc.com tutti i record presenti da più di 24 ore. Per garantire che vengano eliminati tutti i record, inclusi quelli che non sono stati esportati, il parametro PurgeExportedArchivesOnly viene impostato su False ($False).

    Invoke-CsArchivingDatabasePurge -Identity "service:ArchivingDatabase:atl-sql-001.litwareinc.com" -PurgeArchivingDataOlderThanHours 24 -PurgeExportedArchivesOnly $False

## Esempio 2

Il comando riportato nell'esempio 2 è una variante del comando dell'esempio 1. In questo caso tuttavia viene aggiunto il parametro Confirm con la sintassi seguente:

\-Confirm:$False

Con questa sintassi vengono eliminate le richieste di conferma, che altrimenti verrebbero visualizzate durante l'eliminazione di record di archiviazione.

    Invoke-CsArchivingDatabasePurge -Identity "service:ArchivingDatabase:atl-sql-001.litwareinc.com" -PurgeArchivingDataOlderThanHours 24 -PurgeExportedArchivesOnly $False -Confirm:$False

## Esempio 3

Nell'esempio 3 vengono eliminati da tutti i database di archiviazione in uso nell'organizzazione tutti i record presenti da più di 24 ore. A tale scopo, il primo comando nell'esempio utilizza il cmdlet **Get-CsService** e il parametro ArchivingDatabase per restituire una raccolta di tutti i database di archiviazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **ForEach-Object**, che a sua volta seleziona tutti i database della raccolta e quindi esegue il cmdlet **Invoke-CsArchivingDatabasePurge** su ogni database, eliminando tutti i record presenti da più di 24 ore.

    Get-CsService -ArchivingDatabase | ForEach-Object {Invoke-CsArchivingDatabasePurge -Identity $_.Identity -PurgeArchivingDataOlderThanHours 24 -PurgeExportedArchivesOnly $False -Confirm:$False}

## Descrizione dettagliata

Per molte organizzazioni è utile conservare una trascrizione di tutte le sessioni di messaggistica istantanea eseguite dai propri utenti o da un sottoinsieme di utenti selezionati. Altre organizzazioni invece sono obbligate a conservare trascrizioni di questo tipo. Ad esempio, molte organizzazioni che operano nel settore finanziario sono tenute per legge a conservare copie di tutte le comunicazioni elettroniche.

Se è stata abilitata l'archiviazione nell'organizzazione e si è scelto di utilizzare Lync Server come server back-end di archiviazione, i record di archiviazione verranno archiviati nel database di SQL Server LcsLog. In alternativa, questi record possono essere archiviati utilizzando invece Microsoft Exchange. Per ulteriori informazioni, vedere nella Guida l'argomento relativo al cmdlet **New-CsArchivingConfiguration**. Poiché nel tempo è possibile che il database di archiviazione raggiunga dimensioni elevate, in Lync Server sono disponibili per gli amministratori due modi per eliminare i record meno recenti dal database: 1) è possibile configurare Lync Server in modo che i record di archiviazione meno recenti vengano eliminati automaticamente ogni giorno e/o 2) è possibile utilizzare il cmdlet **Invoke-CsArchivingDatabasePurge** in qualsiasi momento per eliminare i record di archiviazione dal database LcsLog. A tale scopo, il cmdlet **Invoke-CsArchivingDatabasePurge** chiama le stored procedure di SQL Server RtcCleanupTempConference e RtcCleanupDB, nonché il contenuto archiviato delle riunioni che è stato eliminato.

Quando si chiama il cmdlet **Invoke-CsArchivingDatabasePurge**, è necessario specificare la posizione del servizio del database di archiviazione in cui si trovano i record di archiviazione, ad esempio ArchivingDatabase:atl-sql-001.litwareinc.com. È necessario inoltre indicare la durata minima (in ore) dei record di archiviazione da eliminare. Se ad esempio si specifica una durata minima di 24 ore, verranno eliminati dal database tutti i record di archiviazione creati da più di 24 ore.

Questi record verranno eliminati anche se per il database specificato è stata disabilitata l'eliminazione, ovvero se nelle impostazioni di configurazione dell'archiviazione la proprietà EnablePurging è stata impostata su False. La proprietà EnablePurging controlla solo l'eliminazione automatica dei record di archiviazione e non ha effetto sul cmdlet **Invoke-CsArchivingDatabasePurge**.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Invoke-CsArchivingDatabasePurge"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Invoke-CsArchivingDatabasePurge** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Identità del servizio del database di archiviazione da eliminare. È possibile recuperare le identità dei database di archiviazione eseguendo il comando:</p>
<p>Get-CsService –ArchivingDatabase</p>
<p>Si noti che non è possibile utilizzare i parametri Identity e SqlServerFqdn nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>PurgeArchivingDataOlderThanHours</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Int32</p></td>
<td><p>Specifica la durata (in ore) dei record di archiviazione da eliminare dal database. I record presenti da un numero di ore superiore al valore specificato verranno eliminati. La proprietà PurgeArchivingDataOlderThanHours può essere impostata su un valore intero compreso tra 1 e 2147483647, estremi inclusi.</p></td>
</tr>
<tr class="odd">
<td><p><em>PurgeExportedArchivesOnly</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se questo parametro viene specificato, i record verranno eliminati dal database di archiviazione solo se sono stati esportati (e di conseguenza se sono stati contrassegnati per l'eliminazione). I record che non sono stati esportati verranno mantenuti nel database, anche se presenti da più ore rispetto al valore specificato dalla proprietà PurgeArchivingDataOlderThanHours.</p></td>
</tr>
<tr class="even">
<td><p><em>SqlServerFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del computer in cui è contenuto il database di archiviazione, ad esempio:</p>
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
<td><p><em>MaxArchivingRecordsToDelete</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Specifica il numero massimo di record di archiviazione da eliminare dal database. Se si imposta questo valore su 99 e nel database sono presenti 100 record che soddisfano il criterio definito da PurgeArchivingDataOlderThanHours, verranno eliminati solo i 99 record meno recenti.</p>
<p>La proprietà MaxArchivingRecordsToDelete può essere impostata su un valore intero compreso tra 1 e 2147483647, estremi inclusi.</p></td>
</tr>
<tr class="even">
<td><p><em>SqlInstanceName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome dell'istanza di SQL Server per il database di archiviazione, ad esempio:</p>
<p>-SqlInstanceName &quot;archinst&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Invoke-CsArchivingDatabasePurge** accetta le istanze della classe Microsoft.Rtc.Management.Xds.DisplayArchivingDatabase\#Decorated inviate tramite pipeline.

## Tipi restituiti

Il cmdlet Invoke-CsArchivingDatabasePurge restituisce istanze della classe Microsoft.Rtc.Management.Purge.ArchDataPurgeStatistics.

## Vedere anche

#### Ulteriori risorse

[New-CsArchivingConfiguration](new-csarchivingconfiguration.md)  
[Set-CsArchivingConfiguration](set-csarchivingconfiguration.md)

