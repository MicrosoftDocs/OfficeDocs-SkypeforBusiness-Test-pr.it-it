---
title: Move-CsManagementServer
TOCTitle: Move-CsManagementServer
ms:assetid: bcead113-fbd2-4fcf-ae01-6a312511ceef
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412921(v=OCS.15)
ms:contentKeyID: 49301803
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsManagementServer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Sposta il server di gestione centrale da un pool a un altro. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Move-CsManagementServer [-ConfigurationFileName <String>] [-LisConfigurationFileName <String>] [-TargetFqdn <Fqdn>] <COMMON PARAMETERS>

    Move-CsManagementServer [-TargetFqdn <Fqdn>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 sposta il server di gestione centrale dal pool esistente in un nuovo pool. Per eseguire questa migrazione in tempo reale, ovvero per spostare un server di gestione centrale online e accessibile, è necessario eseguire il comando da un computer situato nel pool in cui deve essere spostato il server.

    Move-CsManagementServer

## ESEMPIO 2

Nell'esempio 2 viene spostato il server di gestione centrale in una situazione di ripristino di emergenza, ovvero in uno scenario in cui il server di gestione esistente risulta offline o comunque non accessibile. Per eseguire questo tipo di migrazione, è necessario eseguire il comando precedente da un computer situato nel pool in cui deve essere spostato il server. È necessario inoltre includere i parametri ConfigurationFileName per importare il file di backup della configurazione precedentemente salvato, LisConfigurationFileName per importare il file di backup salvato in precedenza per il servizio di emergenza eventualmente in uso e infine Force per forzare il trasferimento del server di gestione centrale, anche se non è possibile contattare il server esistente.

    Move-CsManagementServer -ConfigurationFileName "C:\CsConfiguration.zip" -LisConfigurationFileName "C:\CsLisConfiguration.zip" -Force

## Descrizione dettagliata

Il cmdlet **Move-CsManagementServer** consente agli amministratori di spostare il server di gestione centrale e il relativo archivio di gestione centrale da un pool a un altro. Poiché esiste sempre un potenziale rischio di perdita dei dati (per non citare le interruzioni di servizio), ogni volta che si sposta il server di gestione centrale è consigliabile non eseguire il trasferimento a meno che non si verifichino le seguenti condizioni:

1\. È necessario rimuovere il pool di gestione esistente e trasferire il server di gestione centrale prima di eseguire l'operazione.

2\. Si è verificata una situazione di ripristino di emergenza in cui il server di gestione centrale esistente non è più accessibile.

Prima di spostare il server di gestione centrale, è necessario effettuare le seguenti operazioni:

1\. Verificare di aver creato il nuovo archivio di gestione centrale. A tale scopo, eseguire il cmdlet **Install-CsDatabase** e utilizzare il parametro CentralManagementDatabase.

2\. In caso di spostamento del server di gestione centrale in un server Standard Edition, verificare di aver utilizzato il programma di installazione locale per eseguire l'opzione di preparazione di server Standard Edition. Questa preparazione avanzata è necessaria per aggiungere regole del firewall con cui consentire a Windows PowerShell di accedere in remoto al nuovo archivio di gestione centrale.

3\. Verificare di disporre di spazio libero sufficiente nel computer in cui viene eseguito il cmdlet **Move-CsManagementServer** per gestire il server di gestione centrale.

4\. Verificare che il servizio Front End Server sia stato installato nel computer in cui viene eseguito il cmdlet **Move-CsManagementServer**. Se questo servizio non è installato e in esecuzione, lo spostamento avrà esito negativo.

5\. Verificare di poter eseguire il cmdlet **Enable-CsTopology** nel computer in cui verrà eseguito il cmdlet **Move-CsManagementServer**. Se in tale computer non è possibile eseguire il cmdlet **Enable-CsTopology**, lo spostamento avrà esito negativo e non si disporrà più di un archivio di gestione centrale funzionante.

Dopo aver eseguito queste operazioni, per spostare il server di gestione centrale dal Pool A al Pool B è sufficiente accedere a un computer del Pool B e quindi chiamare il cmdlet **Move-CsManagementServer** senza parametri aggiuntivi:

Move-CsManagementServer

Al termine dell'operazione, il cmdlet **Move-CsManagementServer** consulterà la topologia per determinare la posizione precedente del server di gestione centrale (Pool A) e quindi trasferire il server di gestione centrale e l' archivio di gestione centrale nel pool corrente (Pool B).

Se lo spostamento ha esito positivo, il cmdlet **Move-CsManagementServer** visualizzerà un elenco di computer. Per completare lo spostamento, è necessario eseguire il programma di installazione locale in ognuno di questi computer. I computer del Pool A continueranno a eseguire una versione inattiva del servizio di gestione centrale. L'esecuzione del programma di installazione locale eliminerà tale servizio. Il computer del Pool B in cui è stato spostato il server di gestione centrale eseguirà il servizio di gestione centrale. Gli altri computer del pool tuttavia non eseguiranno tale servizio. Con l'esecuzione del programma di installazione locale in questi computer verrà installato il servizio di gestione centrale.

Per trasferire il server di gestione centrale in uno scenario di ripristino di emergenza, in teoria sarebbe stato necessario utilizzare i cmdlet **Export-CsConfiguration** e **Export-CsLisConfiguration** per creare i file di backup della configurazione rispettivamente di Lync Server e del servizio per chiamate di emergenza (Enhanced 9-1-1 o E9-1-1). Poiché le situazioni di emergenza si verificano generalmente senza alcun preavviso, è consigliabile eseguire periodicamente questi cmdlet e creare file di backup delle impostazioni di configurazione in uso. Quando viene chiamato il cmdlet **Move-CsManagementServer**, è consigliabile includere entrambi i parametri ConfigurationFileName e LisConfigurationFileName per leggere i file di backup.

Includere inoltre il parametro Force ogni volta che si tenta di spostare un server di gestione centrale offline o comunque non accessibile. Quando si chiama il cmdlet **Move-CsManagementServer**, l' archivio di gestione centrale viene impostato temporaneamente sulla modalità di sola lettura prima di effettuare lo spostamento. Questa procedura garantisce una protezione dalla perdita di dati. In una situazione di ripristino di emergenza tuttavia non è possibile contrassegnare l' archivio di gestione centrale come di sola lettura. Il parametro Force indica al cmdlet di spostare l' archivio di gestione centrale anche se non è stato configurato come di sola lettura.

Se il cmdlet **Move-CsManagementServer** ha esito negativo, è possibile che si verifichi una situazione in cui non si dispone più di un server di gestione centrale funzionante. Per ripristinare il server di gestione centrale, sarà necessario risolvere il problema per cui il cmdlet **Move-CsManagementServer** ha avuto esito negativo e quindi eseguire di nuovo il cmdlet. Per rieseguire il cmdlet è possibile utilizzare un nuovo pool o quello precedente. Se si esegue il cmdlet **Move-CsManagementServer** nel pool precedente, lo spostamento verrà annullato e sarà attiva la configurazione originale.

Il cmdlet **Move-CsManagementServer** deve essere eseguito localmente. Non è possibile chiamarlo da una sessione di gestione remota.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Move-CsManagementServer** i membri dei seguenti gruppi: RTCUniversalServerAdmins. È inoltre necessario svolgere il ruolo di amministratore locale del computer in cui viene eseguito il cmdlet.

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
<td><p><em>ConfigurationFileName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Percorso completo del file di backup della configurazione di Lync Server creato mediante l'esecuzione del cmdlet <strong>Export-CsConfiguration</strong>. Questo parametro deve essere eseguito solo in uno scenario di ripristino di emergenza.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Forza lo spostamento del server di gestione centrale anche se l'archivio esistente è offline. Questo parametro è obbligatorio in una situazione di ripristino di emergenza. Esiste tuttavia la possibilità che si verifichi la perdita di alcuni dati ogni volta che si forza lo spostamento del server di gestione centrale.</p>
<p>È inoltre possibile utilizzare il parametro Force in caso di esito negativo di tentativi precedenti di chiamate al cmdlet <strong>Move-CsManagementServer</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>LisConfigurationFileName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Percorso completo del file di backup del servizio di chiamate di emergenza creato mediante l'esecuzione del cmdlet <strong>Export-CsLisConfiguration</strong>. Questo parametro deve essere utilizzato solo in una situazione di ripristino di emergenza.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\MoveManagementServer.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del pool in cui deve essere spostato il server di gestione.</p></td>
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

Nessuno. Il cmdlet **Move-CsManagementServer** non accetta input inviato tramite pipe.

## Tipi restituiti

Nessuno. Il cmdlet **Move-CsManagementServer** non restituisce alcun oggetto.

## Vedere anche

#### Ulteriori risorse

[Set-CsManagementServer](set-csmanagementserver.md)

