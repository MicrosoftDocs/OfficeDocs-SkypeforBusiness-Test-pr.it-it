---
title: Get-CsClientAccessLicense
TOCTitle: Get-CsClientAccessLicense
ms:assetid: 435062d3-b7f9-400c-9ce7-fb6b6ffce44a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204853(v=OCS.15)
ms:contentKeyID: 49300367
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClientAccessLicense

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sull'utilizzo delle licenze client nell'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsClientAccessLicense -LicenseBasedType <String> -LicenseName <String> -MonitoringDatabase <String> -StartDate <DateTime> [-DailyUsage <SwitchParameter>] [-EndDate <DateTime>] <COMMON PARAMETERS>

    Get-CsClientAccessLicense -License <SwitchParameter> <COMMON PARAMETERS>

    COMMON PARAMETERS:

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce informazioni sull'utilizzo delle licenze Standard di tipo basato sull'utente (UserBased) registrate nel database di monitoraggio atl-sql-001\\Archinst. Verranno restituite informazioni sull'utilizzo delle licenze per il periodo di tempo compreso tra il 1° giugno 2012 (6/1/2012) e la data corrente.

    Get-CsClientAccessLicense -MonitoringDatabase "atl-sql-001\Archinst" -LicenseName "Standard" -LicenseBasedType "UserBased" -StartDate "6/1/2012"

## Descrizione dettagliata

Il cmdlet **Get-CsClientAccessLicense** consente agli amministratori di monitorare l'utilizzo delle licenze client per Lync. A tale scopo, viene mostrato l'utilizzo delle licenze client (in base alle registrazioni degli utenti) in un determinato periodo di tempo. Si noti che il cmdlet non gestisce automaticamente le licenze client. Non indicherà ad esempio se sono necessarie licenze aggiuntive. Questo cmdlet si limita semplicemente a restituire informazioni sul numero di licenze in uso durante il periodo di tempo specificato.

Non è possibile utilizzare il cmdlet **Get-CsClientAccessLicense** se non sono stati abilitati il servizio di monitoraggio e la registrazione dettagli chiamata perché le informazioni sulla registrazione vengono archiviate nel database di registrazione dettagli chiamata. Si noti inoltre che, come indica il nome, il cmdlet **Get-CsClientAccessLicense** restituisce solo le informazioni sulle licenze client. Se sono necessarie informazioni sulle licenze server, è possibile utilizzare il cmdlet [Get-CsService](get-csservice.md) per restituire i nomi di dominio completi (FQDN) di tutti i database di Lync Server 2013. Se l'FQDN di un Front End Server corrisponde all'FQDN di un database back-end, si dispone di una licenza standard. Se i due FQDN non corrispondono, si dispone di una licenza del tipo "Enterprise license".

È inoltre possibile che il cmdlet **Get-CsClientAccessLicense** restituisca conteggi delle licenze non corretti. Ad esempio:

\* È possibile che il numero di licenze rilevato sia superiore a quello effettivo se un utente mobile esegue l'accesso da più posizioni mediante un client desktop.

\* È possibile che il numero di licenze rilevato sia inferiore a quello effettivo se un utente si connette con un client mobile, perché l'indirizzo IP del dispositivo mobile non può essere identificato. Inoltre, se durante una sessione l'indirizzo IP di un dispositivo mobile viene modificato, verrà contata una licenza in più che non è effettivamente presente.

\* È possibile che le licenze vengano conteggiate due volte per le chiamate PSTN a un client Lync o per una chiamata da un client Lync a un telefono PSTN, perché, quando si determina il numero di licenze impiegate nella sessione, vengono utilizzati sia l'account utente Lync che il numero di telefono PSTN.

\* Non è possibile conteggiare le licenze per i telefoni Lync se il telefono è stato connesso al sistema prima di eseguire la query di utilizzo delle licenze.

\* Se un utente partecipa a una conferenza mediante un telefono PSTN, per questa chiamata verrà registrato l'utilizzo di una sola licenza. Tuttavia, nessuna licenza è effettivamente necessaria per partecipare a una conferenza mediante un telefono PSTN.


> [!NOTE]
> Per ulteriori informazioni e per le soluzioni a questi problemi, vedere le <A href="lync-server-2013-release-notes.md">Note sulla versione per Lync Server 2013</A>.



Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClientAccessLicense"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsClientAccessLicense** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>License</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce i nomi delle licenze disponibili. Questo parametro non può essere utilizzato con altri parametri. L'unica sintassi valida è la seguente:</p>
<p>Get-CsClientAccessLicense -License</p></td>
</tr>
<tr class="even">
<td><p><em>LicenseBasedType</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Indica se la licenza è di tipo UserBased o DeviceBased. Con le licenze UserBased, tutti gli utenti che accedono a Lync Server devono disporre di una licenza CAL (Client Access License), indipendentemente dal numero di dispositivi utilizzati per accedere a Lync Server. Con le licenze DeviceBased, ogni dispositivo utilizzato per accedere a Lync Server necessita di una licenza separata.</p>
<p>Le licenze basate sull'utente sono consigliate in genere per gli utenti che non si trovano sempre in sede e che possono accedere a Lync Server utilizzando molti altri dispositivi. Le licenze basate sul dispositivo invece sono destinate agli utenti in sede che in genere accedono a Lync Server solo mediante dispositivi condivisi, ad esempio il proprio computer desktop.</p></td>
</tr>
<tr class="odd">
<td><p><em>LicenseName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Indica il tipo di licenza da recuperare. I valori validi sono:</p>
<p>* Standard</p>
<p>* Enterprise</p>
<p>* Plus</p></td>
</tr>
<tr class="even">
<td><p><em>MonitoringDatabase</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Istanza di SQL Server del database di monitoraggio. Vengono utilizzati in genere il nome di dominio completo del computer SQL Server e l'istanza di SQL Server del database di monitoraggio, ad esempio:</p>
<p>-MonitoringDatabase &quot;atl-sql-001.litwareinc.com\archinst&quot;</p>
<p>Se il database di monitoraggio è contenuto nell'istanza di SQL Server predefinita, sarà necessario specificare solo l'FQDN del computer che esegue SQL Server:</p>
<p>-MonitoringDatabase &quot;atl-sql-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>StartDate</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.DateTime</p></td>
<td><p>Data di inizio in base alla quale deve essere verificato l'utilizzo della licenza client. Utilizzando ad esempio il formato inglese americano, il parametro StartDate sarà simile al seguente:</p>
<p>-StartDate &quot;1/1/2012&quot;</p>
<p>La data specificata per StartDate deve essere anteriore alla data specificata per EndDate.</p></td>
</tr>
<tr class="even">
<td><p><em>DailyUsage</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se si specifica questo parametro, l'utilizzo della licenza viene suddiviso su base giornaliera per il periodo di tempo specificato. Se invece non si specifica questo parametro, l'utilizzo della licenza viene riepilogato per il periodo di tempo specificato.</p></td>
</tr>
<tr class="odd">
<td><p><em>EndDate</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.DateTime</p></td>
<td><p>Data di fine in base alla quale deve essere verificato l'utilizzo della licenza client, ad esempio:</p>
<p>-EndDate &quot;2/1/2012&quot;</p>
<p>La data specificata per EndDate deve essere successiva alla data specificata per StartDate. Si noti che la data di fine non viene visualizzata nell'output quando si chiama il cmdlet <strong>Get-CsClientAccessLicense</strong>.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsClientAccessLicense** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Get-CsClientAccessLicense** restituisce informazioni sulle licenze.

## Vedere anche

#### Ulteriori risorse

[Get-CsUser](get-csuser.md)

