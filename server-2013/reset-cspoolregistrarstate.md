---
title: Reset-CsPoolRegistrarState
TOCTitle: Reset-CsPoolRegistrarState
ms:assetid: 1bdbd5d7-cc72-46c5-ac20-ddc0d5723fe0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619172(v=OCS.15)
ms:contentKeyID: 49299850
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Reset-CsPoolRegistrarState

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Reimposta i servizi Windows Fabric e di registrazione per il pool di registrazione specificato. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Reset-CsPoolRegistrarState -PoolFqdn <Fqdn> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-MachineFqdn <Fqdn>] [-NoReStart <SwitchParameter>] [-ResetLocalDatabases <SwitchParameter>] [-ResetType <ServiceReset | QuorumLossRecovery | FullReset | MachineStateRemoved>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 esegue una reimpostazione del servizio per il pool di registrazione atl-cs-001.litwareinc.com. Si noti che, dopo l'esecuzione del comando, verrà richiesto se si desidera o meno procedere alla reimpostazione del servizio.

    Reset-CsPoolRegistrarState -PoolFqdn "atl-cs-001.litwareinc.com" -ResetType ServiceReset

## Esempio 2

Anche nell'esempio 2 viene eseguita una reimpostazione dei servizi per il pool di registrazione atl-cs-001.litwareinc.com. In questo caso, è stato però incluso il parametro Confirm con il valore $False (-Confirm:$False). Ciò determina l'eliminazione del messaggio di conferma che viene in genere visualizzato quando si chiama il cmdlet **Reset-CsPoolRegistrarState**. Non verrà quindi richiesto se si desidera o meno procedere alla reimpostazione del servizio e il comando verrà eseguito non appena si preme INVIO.

    Reset-CsPoolRegistrarState -PoolFqdn "atl-cs-001.litwareinc.com" -ResetType ServiceReset -Confirm:$False

## Esempio 3

Nell'esempio 3, viene eseguita una reimpostazione del recupero della perdita di quorum sul pool atl-cs-001.litwareinc.com. Una reimpostazione del recupero della perdita di quorum viene in genere utilizzata quando il numero di Front End Server attivi in un pool scende sotto lo stato del quorum (ovvero, quando in un pool è attualmente attivo meno dell'85% dei Front End Server). Si noti che solo i servizi che si trovano in una perdita di quorum dovranno ricaricare i dati utente dall'archivio di backup. Gli altri servizi non saranno interessati da questo comando.

    Reset-CsPoolRegistrarState -PoolFqdn "atl-cs-001.litwareinc.com" -ResetType QuorumLossRecovery

## Esempio 4

Nell'esempio 4 viene eseguita una reimpostazione completa per il pool atl-cs-001.litwareinc.com. In una reimpostazione completa, i servizi Front End e Windows Fabric vengono arrestati e viene rimosso un set di elementi (inclusi i file LyncServer-MachineSet.xml e Settings.xml). Dopo la rimozione di questi elementi, i servizi Front End e Windows Fabric vengono riavviati.

Quando si tenta di riavviare un pool, è possibile che l'utilizzo dell'opzione FullReset generi un errore e che il pool non venga riavviato. È pertanto consigliabile provare a riavviare il pool utilizzando prima una delle altre opzioni ResetType. In caso di esito negativo, consultare il personale di supporto Microsoft prima di ricorrere all'opzione FullReset.

    Reset-CsPoolRegistrarState -PoolFqdn "atl-cs-001.litwareinc.com" -ResetType FullReset

## Esempio 5

L'esempio 5 è una variante del comando riportato nell'esempio 4. In questo caso, è tuttavia incluso il parametro NoReStart, che impedisce al cmdlet **Reset-CsPoolRegistrarState** di riavviare i servizi (ad esempio, il servizio Windows Fabric) che vengono arrestati durante la reimpostazione del pool. Il riavvio manuale di questi servizi dovrà essere eseguito dagli amministratori.

Come illustrato nell'esempio 4, quando si tenta di riavviare un pool, è possibile che l'utilizzo dell'opzione FullReset generi un errore e che il pool non venga riavviato. È pertanto consigliabile provare a riavviare il pool utilizzando prima una delle altre opzioni ResetType. In caso di esito negativo, consultare il personale di supporto Microsoft prima di ricorrere all'opzione FullReset.

    Reset-CsPoolRegistrarState -PoolFqdn "atl-cs-001.litwareinc.com" -ResetType FullReset -NoReStart

## Descrizione dettagliata

Il cmdlet **Reset-CsPoolRegistrarState** consente di reimpostare il servizio Windows Fabric (FabricHostSvc) e il servizio di registrazione di Lync Server (RtcSrv) per un pool di registrazione. Tale operazione potrebbe essere necessaria se il pool non risponde più o non può essere avviato, una condizione che determina in genere il blocco del servizio di registrazione nello stato Avvio in sospeso. L'esecuzione del cmdlet consente, per impostazione predefinita, di arrestare e quindi riavviare tutti i servizi pertinenti nel pool. È però possibile utilizzare il parametro NoReStart per fare in modo che il cmdlet **Reset-CsPooRegistrarState** arresti i servizi senza riavviarli. Sarà quindi possibile scegliere di riavviarli tutti (o alcuni) manualmente.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Reset-CsPoolRegistrarState"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Reset-CsPoolRegistrarState** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Nome di dominio completo del pool di registrazione in fase di reimpostazione. Ad esempio:</p>
<p>-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di visualizzare una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>MachineFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del computer da rimuovere dal pool. Questo parametro viene utilizzato solo quando si esegue una reimpostazione MachineStateRemoved.</p></td>
</tr>
<tr class="odd">
<td><p><em>NoReStart</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, i servizi, come RtcSrv and FabricHostSvc, interrotti con l'esecuzione del cmdlet non vengono riavviati.</p></td>
</tr>
<tr class="even">
<td><p><em>ResetLocalDatabases</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, vengono interrotti e riavviati i database Lync Server locali oltre ai servizi Lync Server locali.</p></td>
</tr>
<tr class="odd">
<td><p><em>ResetType</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Hadr.ResetPoolFabricStateCmdlet+PoolResetType</p></td>
<td><p>Tipo di reimpostazione da eseguire. I valori consentiti sono:</p>
<p>* <strong>ServiceReset</strong> – i servizi RtcSrv e fabricHostSvc vengono interrotti e riavviati. Se non viene specificato il parametro <code>ResetType</code> viene eseguita una reimpostazione del servizio.</p>
<p>* <strong>QuorumLossRecovery</strong> – consente di ricaricare i dati utente dall'archivio di backup per tutti i gruppi di routing attualmente in uno stato di perdita del quorum. Si verifica una perdita del quorum quando non sono disponibili né il database né le relative repliche. Quando si esegue questo tipo reimpostazione è possibile che i dati non ancora scritti nel database vadano persi.</p>
<p>L'opzione <code>QuorumLossRecovery</code> consente al pool di eseguire il recupero dalla perdita del quorum a livello di replica. Per il funzionamento del pool, tuttavia, è necessario che la perdita del quorum a livello di pool non raggiunga un livello di gravità superiore. Per ulteriori informazioni, vedere <a href="lync-server-2013-topologies-and-components-for-front-end-servers-instant-messaging-and-presence.md">Topologie e componenti per Front End Server, messaggistica istantanea e presenza in Lync Server 2013</a>.</p>
<p>* <strong>FullReset</strong> – esegue lo stesso tipo di reimpostazione di <code>QuorumLossRecovery</code>. In aggiunta, però, consente di ricreare i database di Lync Server locali. Questo tipo di reimpostazione può potenzialmente richiedere un'ampia quantità di tempo e risorse. Utilizzare questa opzione solo in caso di variazione del numero di Front End Server in un pool, ad esempio da 2 a qualsiasi numero, da 1 a qualsiasi numero, da qualsiasi numero a 2 o da qualsiasi numero a 1. <strong>Non utilizzare questa opzione per risolvere problemi relativi all'avvio del servizio.</strong></p>
<p>L'utilizzo di questo cmdlet con le opzioni ServiceReset o FullReset influirà sugli utenti che hanno eseguito l'accesso, mentre l'opzione QuorumLossRecovery non determinerà conseguenze per gli utenti.</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Quando si tenta di riavviare un pool, è possibile che l'utilizzo dell'opzione FullReset generi un errore e che il pool non venga riavviato. È pertanto consigliabile provare a riavviare il pool utilizzando prima una delle altre opzioni ResetType. In caso di esito negativo, consultare il personale di supporto Microsoft prima di ricorrere all'opzione FullReset. FullReset viene generalmente usata solo quando una topologia cambia da un pool con un unico server front-end a un pool con più server front-end.</td>
</tr>
</tbody>
</table>

</div>
<p><code>* MachineStateRemoved</code> – consente di rimuovere il server specificato dal pool. È consigliabile utilizzare questo tipo di reimpostazione solo se il server in questione o i relativi database sono stati definitivamente persi.</p></td>
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

Nessuno. Il cmdlet **Reset-CsPoolRegistrarState** non accetta input da pipeline.

## Tipi restituiti

Valori stringa. Il cmdlet **Reset-CsPoolRegistrarState** non restituisce oggetti.

## Vedere anche

#### Ulteriori risorse

[Get-CsPoolFabricState](get-cspoolfabricstate.md)

