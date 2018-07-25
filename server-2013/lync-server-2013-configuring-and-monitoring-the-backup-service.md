---
title: 'Lync Server 2013: Configurazione e monitoraggio del servizio di backup'
TOCTitle: Configurazione e monitoraggio del servizio di backup
ms:assetid: c608280e-a7d1-4ae0-a75c-da6b524752fa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205252(v=OCS.15)
ms:contentKeyID: 49301940
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione e monitoraggio del servizio di backup in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

È possibile utilizzare i comandi di Lync Server Management Shell seguenti per configurare e monitorare il servizio di backup.


> [!NOTE]
> RTCUniversalServerAdmins è l'unico gruppo che dispone delle autorizzazioni per eseguire <STRONG>Get-CsBackupServiceStatus</STRONG> per impostazione predefinita. Per utilizzare questo cmdlet, eseguire l'accesso come membro di questo gruppo. In alternativa, è possibile concedere l'accesso a questo comando ad altri gruppi, ad esempio CSAdministrator, utilizzando il cmdlet <STRONG>Set-CsBackupServiceConfiguration</STRONG>.



## Per visualizzare la configurazione del servizio di backup

Eseguire il cmdlet seguente:

    Get-CsBackupServiceConfiguration

Il valore predefinito per SyncInterval è due minuti.

## Per impostare l'intervallo di sincronizzazione del servizio di backup

Eseguire il cmdlet seguente:

    Set-CsBackupServiceConfiguration -SyncInterval interval

Con il comando seguente ad esempio si imposta l'intervallo su tre minuti.

    Set-CsBackupServiceConfiguration -SyncInterval 00:03:00

> [!important]  
> Benché sia possibile utilizzare questo cmdlet per modificare l'intervallo di sincronizzazione predefinito per il servizio di backup, non è consigliabile modificare questo valore a meno che non sia assolutamente necessario, poiché l'intervallo di sincronizzazione ha un effetto significativo sulle prestazioni e sull''obiettivo in termini di punto di ripristino (RPO, Recovery Point Objective) del servizio di backup.

## Per ottenere lo stato del servizio di backup per un pool specifico

Eseguire il cmdlet seguente:

    Get-CsBackupServiceStatus -PoolFqdn <pool-FQDN>


> [!NOTE]
> Lo stato di sincronizzazione del servizio di backup è definito in modo unidirezionale da un pool (P1) per il relativo pool di backup (P2). Lo stato di sincronizzazione da P1 a P2 può essere diverso dallo stato di sincronizzazione da P2 a P1. Per la sincronizzazione da P1 a P2, il servizio di backup è in uno stato "stazionario" se tutte le modifiche apportate a P1 vengono interamente replicate in P2 nell'intervallo di sincronizzazione. Lo stato invece è "finale" se non sono presenti ulteriori modifiche da sincronizzare da P1 a P2. Entrambi gli stati indicano uno snapshot del servizio di backup effettuato al momento dell'esecuzione del cmdlet. Questo non implica che lo stato restituito resti invariato successivamente. In particolare, lo stato "finale" rimarrà tale solo se P1 non genera modifiche dopo l'esecuzione del cmdlet. Questo si verifica in caso di failover di P1 a P2 dopo l'attivazione della modalità di sola lettura per P1 come parte della logica di esecuzione di <STRONG>Invoke-CsPoolfailover</STRONG>.



## Per ottenere informazioni sulla relazione di backup per un pool specifico

Eseguire il cmdlet seguente:

    Get-CsPoolBackupRelationship -PoolFQDN <poolFQDN>

## Per forzare una sincronizzazione del servizio di backup

Eseguire il cmdlet seguente:

    Invoke-CsBackupServiceSync -PoolFqdn <poolFqdn> [-BackupModule  {All|PresenceFocus|DataConf|CMSMaster}]

