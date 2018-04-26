---
title: Get-CsBackupServiceStatus
TOCTitle: Get-CsBackupServiceStatus
ms:assetid: 7f56cc81-534c-48e8-9f74-5741d4534a83
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205032(v=OCS.15)
ms:contentKeyID: 49301120
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsBackupServiceStatus

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sullo stato corrente del servizio di backup per un pool specificato. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsBackupServiceStatus -PoolFqdn <Fqdn> [-Category <UserData | CMS>] [-Force <SwitchParameter>]

## Esempi

## Esempio 1

Il comando seguente restituisce lo stato del servizio di backup per il pool atl-cs-001.litwareinc.com.

    Get-CsBackupServiceStatus -PoolFqdn "atl-cs-001.litwareinc.com"

## Descrizione dettagliata

Il cmdlet **Get-CsBackupServiceStatus** consente agli amministratori di verificare che il servizio di backup di un pool di registrazione specificato sia stato configurato e funzioni correttamente. Si noti che, per impostazione predefinita, solo gli utenti appartenenti al gruppo RTCUniversalServerAdmins sono autorizzati a eseguire questo cmdlet e a controllare lo stato di backup di un pool. Per concedere a ulteriori gruppi l'autorizzazione per l'esecuzione di questo cmdlet, utilizzare il cmdlet **Set-CsBackupServiceConfiguration** per aggiungere tali gruppi alla proprietà AuthorizedUniversalGroups.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsBackupServiceStatus"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsBackupServiceStatus** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Nome di dominio completo del pool del cui servizio di backup viene verificato lo stato. Ad esempio:</p>
<p>-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Category</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Hadr.BackupService.BackupCategory</p></td>
<td><p>Tipo di backup di cui viene verificato lo stato. I valori consentiti sono:</p>
<p>* CMS</p>
<p>* UserData</p>
<p>Se questo parametro non viene specificato, verranno verificati entrambi i tipi di backup.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsBackupServiceStatus** non accetta input tramite pipeline.

## Tipi restituiti

Restituisce informazioni sul servizio di backup.

## Vedere anche

#### Ulteriori risorse

[Get-CsBackupServiceConfiguration](get-csbackupserviceconfiguration.md)

