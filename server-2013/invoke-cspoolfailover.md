---
title: Invoke-CsPoolFailOver
TOCTitle: Invoke-CsPoolFailOver
ms:assetid: b5c30438-0553-41f4-b856-68c1ec0deff7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205189(v=OCS.15)
ms:contentKeyID: 49301730
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Invoke-CsPoolFailOver

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Richiama il processo di failover per un pool di Lync Server 2013. Il failover è il processo che viene eseguito quando si verifica un problema in un pool e i relativi utenti correnti vengono quindi connessi a un pool di backup. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Invoke-CsPoolFailOver -PoolFqdn <Fqdn> [-Confirm [<SwitchParameter>]] [-DisasterMode <SwitchParameter>] [-FlushStorageService <SwitchParameter>] [-Force <SwitchParameter>] [-WaitTime <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 richiama il failover per il pool atl-cs-001.litwareinc.com.

    Invoke-CsPoolFailOver -PoolFqdn "atl-cs-001.litwareinc.com"

## Esempio 2

Nell'esempio 2 viene richiamato il failover per la modalità di emergenza per il pool atl-cs-001.litwareinc.com.

    Invoke-CsPoolFailOver -PoolFqdn "atl-cs-001.litwareinc.com" -DisasterMode

## Descrizione dettagliata

Il processo di failover di un pool consente agli amministratori di ripristinare rapidamente il servizio per gli utenti qualora il pool di registrazione a cui si sono connessi non sia più disponibile. Se si verifica un problema in un pool, gli utenti verranno automaticamente disconnessi da Lync Server 2013. Se tentano di riaccedere immediatamente, verranno reindirizzati al pool di backup specificato.

Per ripristinare il servizio per questi utenti, gli amministratori possono eseguire il cmdlet **Invoke-CsPoolFailOver** nel pool attualmente non disponibile. In questo modo si consente agli utenti di accedere a Lync Server utilizzando il pool di backup designato e si concede a questi utenti l'accesso a tutti i servizi e le funzionalità di Lync Server. Si noti che a questi utenti non verrà assegnata una nuova posizione nel pool di backup. Verrà semplicemente consentito loro di eseguire l'accesso e di utilizzare tale pool finché non verrà ripristinato il pool principale. Se ad esempio si verifica un problema nel pool A, gli utenti potranno accedere al pool B (con funzionalità complete) finché non verrà ripristinato il pool A.

Quando il pool in cui si è verificato il problema è di nuovo operativo, gli amministratori possono eseguire il cmdlet **Invoke-CsPoolFailBack** per sottoporre gli utenti del pool a "failback". Se un utente è attualmente connesso al pool di backup, verrà reindirizzato al pool principale dopo il ripristino del servizio.

Il failover di un pool può essere richiamato solo se è stato assegnato un pool di backup al pool in cui si è verificato il problema.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Invoke-CsPoolFailover"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Invoke-CsPoolFailOver** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Nome di dominio completo (FQDN) del pool da cui viene eseguito il failover. Ad esempio:</p>
<p>-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
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
<td><p>Se questo parametro è presente, indica che il failover viene eseguito in &quot;modalità di emergenza&quot;. Se un pool non è più accessibile, il solo modo per ripristinare le funzionalità complete per gli utenti del pool è eseguire il failover del pool utilizzando il parametro DisasterMode.</p>
<p>Se questo parametro non è presente, il pool è ancora attivo e funzionante e il failover è stato eseguito per scelta dell'amministratore. Ad esempio, è possibile eseguire temporaneamente il failover del pool per effettuare aggiornamenti hardware o software nel server.</p></td>
</tr>
<tr class="even">
<td><p><em>FlushStorageService</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se questo parametro viene specificato, il cmdlet <strong>Invoke-CsPoolFailOver</strong> eseguirà il failover di tutti gli utenti del pool e chiamerà il cmdlet <a href="invoke-csstorageserviceflush.md">Invoke-CsStorageServiceFlush</a> per scaricare il database del servizio di archiviazione in ogni Front End Server del pool. Lo scaricamento di un database comporta la scrittura su disco di tutti i dati accodati e quindi la cancellazione del contenuto della cache del database.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Impedisce la visualizzazione di eventuali messaggi di errore non irreversibili che potrebbero verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>WaitTime</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Specifica l'intervallo di tempo, in secondi, che il cmdlet attenderà prima di presupporre che i dati siano stati sincronizzati dal pool in failover al pool di riserva.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Invoke-CsPoolFailOver** non accetta input inviato tramite pipe.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Invoke-CsPoolFailBack](invoke-cspoolfailback.md)

