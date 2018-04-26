---
title: Eliminazione manuale dei database di Registrazione dettagli chiamata e Qualità percepita dagli utenti
TOCTitle: Eliminazione manuale dei database di Registrazione dettagli chiamata e Qualità percepita dagli utenti
ms:assetid: 3a3a965b-b861-41a4-b9a8-27184d622c17
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204812(v=OCS.15)
ms:contentKeyID: 49300254
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminazione manuale dei database di Registrazione dettagli chiamata e Qualità percepita dagli utenti

 

_**Ultima modifica dell'argomento:** 2014-07-07_

Come segnalato nella sezione precedente, gli amministratori possono configurare i database Registrazione dettagli chiamata (CDR) e/o Quality of Experience (QoE) in modo che dal database vengano eliminati i record meno recenti. Ciò si verifica se per il database specificato (CDR o QoE) è stata abilitata l'eliminazione e se nel database sono rimasti record per un periodo di tempo più lungo di quello specificato. Ad esempio gli amministratori potrebbero configurare il sistema in modo che ogni giorno all'1.00 vengano eliminati i record QoE che si trovano nel database da più di 60 giorni.

Oltre all'eliminazione automatica, a Microsoft Lync Server 2013sono stati aggiunti due nuovi cmdlet: Invoke-CsCdrDatabasePurge e Invoke-CsQoEDatbasePurge. Questi cmdlet consentono agli amministratori di eliminare manualmente i record dai database CDR e QoE in qualsiasi momento. Ad esempio, per eliminare manualmente dal database CDR tutti i record più vecchi di 10 giorni, è possibile usare un comando simile al seguente:

    Invoke-CsCdrDatabasePurge -Identity MonitoringDatabase:atl-sql-001.litwareinc.com -PurgeCallDetailDataOlderThanDays 10 -PurgeDiagnosticDataOlderThanDays 10

Nel comando precedente tutti i record dettagli di chiamata e tutti i record dati diagnostici più vecchi di 10 giorni vengono eliminati dal database di monitoraggio in atl-sql-001.litwareinc.com. I record dettagli di chiamata sono rapporti utente/sessione. I record dati diagnostici sono registri diagnostici caricati dalle applicazioni client come Lync 2013.

Come mostrato sopra, quando si esegue il cmdlet Invoke-CsCdrDatabasePurge, è necessario includere sia il parametro PurgeCallDetaiDataOlderThanDays sia il parametro PurgeDiagnosticDataOlderThanDays. Questi parametri non devono tuttavia essere impostati sullo stesso valore. Ad esempio è possibile eliminare i record dettagli chiamata più vecchi di 10 giorni ma lasciare nel database tutti i record dati diagnostici. A questo scopo, impostare il parametro PurgeCallDetailDataOlderThanDays su 10 e il parametro PurgeDiagnosticDataOlderThanDays su 0. Ad esempio:

    Invoke-CsCdrDatabasePurge -Identity MonitoringDatabase:atl-sql-001.litwareinc.com -PurgeCallDetailDataOlderThanDays 10 -PurgeDiagnosticDataOlderThanDays 0

Per impostazione predefinita, se si esegue Invoke-CsCdrDatabasePurge, viene visualizzata una richiesta simile alla seguente per ogni tabella di database che deve essere eliminata:

    Confirm
    Are you sure you want to perform this action?
    Performing operation "Stored procedure: RtcCleanupDiag" on Target "Target SQL Server:atl-sql-001.litwareinc.com\archinst Database: lcscdr".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All [S] Suspend  [?] Help (default is "Y"):

Per eliminare i record dal database, è necessario immettere Y (Sì) o A (Sì a tutti). Queste richieste di conferma si possono eliminare aggiungendo il parametro seguente a Invoke-CsCdrDatabasePurge alla fine della chiamata:

    -Confirm:$False

Ad esempio:

    Invoke-CsCdrDatabasePurge -Identity MonitoringDatabase:atl-sql-001.litwareinc.com -PurgeCallDetailDataOlderThanDays 10 -PurgeDiagnosticDataOlderThanDays 10 -Confirm:$False

In questo modo le richieste di conferma non verranno visualizzate e l'eliminazione verrà eseguita immediatamente.

Per eliminare i record dal database QoE, usare il cmdlet Invoke-CsQoEDatabasePurge e specificare la durata (in giorni) dei record da eliminare:

    Invoke-CsQoEDatabasePurge -Identity MonitoringDatabase:atl-sql-001.litwareinc.com -PurgeQoEDataOlderThanDays 10

