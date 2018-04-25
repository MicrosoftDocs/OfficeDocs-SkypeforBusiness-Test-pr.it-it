---
title: Invoke-CsPoolFailBack
TOCTitle: Invoke-CsPoolFailBack
ms:assetid: 4e58d0b5-4353-4de8-b242-2a4553c3371e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204873(v=OCS.15)
ms:contentKeyID: 49300500
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Invoke-CsPoolFailBack

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Richiama il processo di failback per un pool di Lync Server 2013. Il failback viene eseguito dopo il failover di un pool e lo spostamento tramite "failover" dei relativi utenti in un pool di backup. Questo significa semplicemente che gli utenti che hanno eseguito l'accesso al pool in cui si è verificato l'errore vengono automaticamente connessi al pool di backup. Dopo il ripristino del pool in cui si è verificato l'errore, il processo di failback connette di nuovo gli utenti sottoposti a failover al pool originale. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Invoke-CsPoolFailBack -PoolFqdn <Fqdn> [-Confirm [<SwitchParameter>]] [-DisasterMode <SwitchParameter>] [-Force <SwitchParameter>] [-WaitTime <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Nell'esempio 1 viene richiamato il failback per il pool atl-cs-001.litwareinc.com.

    Invoke-CsPoolFailback -PoolFqdn "atl-cs-001.litwareinc.com"

## Descrizione dettagliata

Il processo di failover di un pool consente agli amministratori di ripristinare rapidamente il servizio per gli utenti qualora il pool di registrazione a cui si sono connessi non sia più disponibile. Se si verifica un problema in un pool, gli utenti verranno automaticamente disconnessi da Lync Server 2013. Se tentano di riaccedere immediatamente, verranno reindirizzati al pool di backup specificato.

Per ripristinare il servizio per questi utenti, gli amministratori possono eseguire il cmdlet **Invoke-CsPoolFailOver** nel pool attualmente non disponibile. In questo modo si consente agli utenti di accedere a Lync Server utilizzando il pool di backup designato e si concede a questi utenti l'accesso a tutti i servizi e le funzionalità di Lync Server. Si noti che a questi utenti non verrà assegnata una nuova posizione nel pool di backup. Verrà semplicemente consentito loro di eseguire l'accesso e di utilizzare tale pool finché non verrà ripristinato il pool principale. Se ad esempio si verifica un problema nel pool A, gli utenti potranno accedere al pool B (con funzionalità complete) finché non verrà ripristinato il pool A.

Quando il pool in cui si è verificato il problema è di nuovo operativo, gli amministratori possono eseguire il cmdlet **Invoke-CsPoolFailBack** per sottoporre gli utenti del pool a "failback". Se un utente è attualmente connesso al pool di backup, verrà reindirizzato al pool principale dopo il ripristino del servizio.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Invoke-CsPoolFailback"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Invoke-CsPoolFailback** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Nome di dominio completo del pool di cui viene eseguito il failback, ad esempio:-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p>
<p>L'FQDN del pool utilizzato durante il failback deve essere uguale a quello utilizzato durante il failover.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisasterMode</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente agli amministratori di richiamare il failback del pool anche se il pool di backup non è attualmente disponibile. Quando si utilizza questo parametro, i dati generati dagli utenti sottoposti a failover nel pool di backup andranno persi.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Impedisce la visualizzazione di eventuali messaggi di errore non irreversibili che potrebbero verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>WaitTime</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Specifica il tempo massimo di attesa prima che il cmdlet sincronizzi i dati. I valori temporali devono essere espressi nel formato ore:minuti:secondi. La sintassi seguente ad esempio imposta il tempo di attesa su 1 minuto e 30 secondi (00 ore:01:minuto:30 secondi):</p>
<p>00:01:30</p>
<p>Il valore predefinito è 15 secondi.</p></td>
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

Nessuno. Il cmdlet **Invoke-CsPoolFailBack** non accetta input inviato tramite pipe.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Invoke-CsPoolFailOver](invoke-cspoolfailover.md)

