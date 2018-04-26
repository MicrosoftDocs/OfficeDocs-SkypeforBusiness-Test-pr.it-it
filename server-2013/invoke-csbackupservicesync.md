---
title: Invoke-CsBackupServiceSync
TOCTitle: Invoke-CsBackupServiceSync
ms:assetid: f3de25c2-a1ef-4781-8b33-74f5dc1e6f8d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205374(v=OCS.15)
ms:contentKeyID: 49302467
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Invoke-CsBackupServiceSync

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Richiama manualmente la sincronizzazione di backup tra un pool di Lync Server 2013 e un pool di backup designato, consentendo così agli amministratori di sincronizzare i dati senza attendere la replica di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Invoke-CsBackupServiceSync -PoolFqdn <Fqdn> [-BackupModule <String>] [-Force <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 sincronizza i servizi di backup per il pool atl-cs-001.litwareinc.com.

    Invoke-CsBackupServiceSync -PoolFqdn "atl-cs-001.litwareinc.com"

## Descrizione dettagliata

Il cmdlet **Invoke-CsBackupServiceSync** consente agli amministratori di sincronizzare i dati tra un pool di registrazione e il relativo pool di backup. Il cmdlet **Invoke-CsBackupServiceSync** copierà solo i dati necessari per sincronizzare i due pool.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi eventuali ruoli RBAC personalizzati creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Invoke-CsBackupServiceSync"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Invoke-CsBackupServiceSync** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Nome di dominio completo del pool in cui viene richiamata la sincronizzazione del servizio di backup. Ad esempio:</p>
<p>-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>BackupModule</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indica il tipo di dati da sincronizzare. I valori validi sono:</p>
<p>* UserServices.PresenceFocus</p>
<p>* ConfServices.DataConf</p>
<p>* CentralMgmt.CMSMaster</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Impedisce la visualizzazione di eventuali messaggi di errore non irreversibili che potrebbero verificarsi durante l'esecuzione del comando.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Valore di stringa. Il cmdlet **Invoke-CsBackupServiceSync** può accettare un valore di stringa da pipeline che rappresenta un nome di dominio completo di un pool Lync Server 2013.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Backup-CsPool](backup-cspool.md)

