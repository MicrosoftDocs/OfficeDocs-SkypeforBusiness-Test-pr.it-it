---
title: Backup-CsPool
TOCTitle: Backup-CsPool
ms:assetid: 66ec46de-e1e7-4e33-961d-7ef785059c48
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204955(v=OCS.15)
ms:contentKeyID: 49300820
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Backup-CsPool

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una copia di backup del pool di Lync Server 2013 specificato. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Backup-CsPool -PoolFqdn <Fqdn> [-Category <UserData | CMS>] [-Confirm [<SwitchParameter>]] [-FailedOverPoolOnly <SwitchParameter>] [-Force <SwitchParameter>] [-FullBackup <SwitchParameter>] [-LocalStore <SwitchParameter>] [-Report <String>] [-RetryCount <Int32>] [-SteadyState <SwitchParameter>] [-WaitTime <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 crea una copia di backup del pool atl-cs-001.litwareinc.com.

    Backup-CsPool -PoolFqdn "atl-cs-001.litwareinc.com"

## Esempio 2

Nell'esempio 2 viene creata una copia di backup con "stato stabile" (SteadyState) del pool atl-cs-001.litwareinc.com.

    Backup-CsPool -PoolFqdn "atl-cs-001.litwareinc.com" -SteadyState

## Descrizione dettagliata

Il cmdlet **Backup-CsPool** consente agli amministratori di copiare i dati degli utenti e i dati delle conferenze di un pool di registrazione in un pool di backup specificato. Se si verifica un errore del pool principale o tale pool diventa comunque non disponibile, è possibile spostare nel pool di backup tramite "failover" gli utenti che risiedono nel pool principale. Questi utenti possono quindi accedere a Lync Server tramite il pool di backup e continuare a utilizzare tale pool finché non verrà ripristinato il pool principale.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli di controllo di accesso basato sui ruoli creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente: Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Backup-CsPool"}

**Pannello di controllo di Lync Server**: le funzioni eseguite dal cmdlet **Backup-CsPool** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>PoolFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del pool di cui viene eseguito il backup, ad esempio:</p>
<p>-SourcePoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Category</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Hadr.BackupService.BackupCategory</p></td>
<td><p>Consente di selezionare i moduli di Lync Server di cui verrà eseguito il backup. Se non si specifica questo parametro, verrà eseguito il backup di tutti i moduli. I valori consentiti sono:</p>
<p>* CMS</p>
<p>* UserData</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>FailedOverPoolOnly</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se si specifica questo parametro, il backup verrà eseguito solo se il pool è nello stato di failover. Se si utilizza questo parametro, è necessario utilizzare anche il parametro FullBackup.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>FullBackup</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se si specifica questo parametro, il backup verrà avviato solo dopo che il servizio di backup ha raggiunto lo stato finale. Non è possibile utilizzare i parametri FullBackup e SteadyState nello stesso comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera le informazioni sulla topologia dalla replica locale dell'archivio di gestione centrale anziché direttamente dall'archivio di gestione centrale.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Percorso del file di log creato quando viene eseguito il cmdlet, ad esempio:</p>
<p>-Report &quot;C:\Logs\BackupPool.html&quot;</p>
<p>Se il file esiste già, viene sovrascritto durante l'esecuzione del cmdlet.</p>
<p>Per impostazione predefinita, i rapporti vengono scritti nella cartella AppData\Local\Temp nel profilo utente.</p></td>
</tr>
<tr class="odd">
<td><p><em>RetryCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Numero massimo di tentativi di chiamata al servizio di backup da parte di Backup-CsPool prima che si verifichi un errore.</p></td>
</tr>
<tr class="even">
<td><p><em>SteadyState</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se si specifica questo parametro, il backup verrà avviato solo dopo che il servizio di backup ha raggiunto lo stato stabile. Lo &quot;stato stabile&quot; viene raggiunto quando il pool passa alla modalità di sola lettura o di failover/failback e non produce più nuovi dati di cui deve essere eseguito il backup.</p></td>
</tr>
<tr class="odd">
<td><p><em>WaitTime</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Numero di secondi di attesa da parte del cmdlet prima che venga controllato se il servizio di backup è nello stato completo o stabile.</p></td>
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

Nessuno. Il cmdlet **Backup-CsPool** non accetta dati da pipeline.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Get-CsBackupServiceConfiguration](get-csbackupserviceconfiguration.md)  
[Get-CsBackupServiceStatus](get-csbackupservicestatus.md)  
[Get-CsPoolBackupRelationship](get-cspoolbackuprelationship.md)

