---
title: New-CsConferencingConfiguration
TOCTitle: New-CsConferencingConfiguration
ms:assetid: c4295f94-f525-46ce-93b8-ae9338c9bc4e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412967(v=OCS.15)
ms:contentKeyID: 49301917
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsConferencingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni di configurazione delle conferenze. Tali impostazioni determinano aspetti quali la dimensione massima consentita per il contenuto e gli stampati delle conferenze, il periodo di tolleranza (ovvero per quanto tempo il contenuto resterà archiviato prima di essere eliminato) e gli URL per i download interni ed esterni del client supportato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsConferencingConfiguration -Identity <XdsIdentity> [-ClientAppSharingPort <UInt16>] [-ClientAppSharingPortRange <UInt32>] [-ClientAudioPort <UInt16>] [-ClientAudioPortRange <UInt32>] [-ClientFileTransferPort <UInt16>] [-ClientFileTransferPortRange <UInt32>] [-ClientMediaPort <UInt16>] [-ClientMediaPortRange <UInt32>] [-ClientMediaPortRangeEnabled <$true | $false>] [-ClientSipDynamicPort <UInt16>] [-ClientSipDynamicPortRange <UInt32>] [-ClientVideoPort <UInt16>] [-ClientVideoPortRange <UInt32>] [-Confirm [<SwitchParameter>]] [-ConsoleDownloadExternalUrl <String>] [-ConsoleDownloadInternalUrl <String>] [-ContentGracePeriod <TimeSpan>] [-Force <SwitchParameter>] [-HelpdeskExternalUrl <String>] [-HelpdeskInternalUrl <String>] [-InMemory <SwitchParameter>] [-MaxBandwidthPerAppSharingServiceMb <UInt64>] [-MaxContentStorageMb <UInt16>] [-MaxUploadFileSizeMb <UInt16>] [-Organization <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Tramite il comando illustrato nell'esempio 1 è possibile creare una nuova raccolta di impostazioni di configurazione delle conferenze per il sito di Redmond (site:Redmond). In questo esempio è incluso un parametro aggiuntivo (Organization), che viene utilizzato per impostare il valore della proprietà Organization su Litwareinc. Se il sito di Redmond dispone già di una raccolta di impostazioni di configurazione delle conferenze, il comando avrà esito negativo poiché è ammessa una sola raccolta per sito.

    New-CsConferencingConfiguration -Identity site:Redmond -Organization Litwareinc

## ESEMPIO 2

Nell'esempio 2 viene creata una nuova raccolta di impostazioni di configurazione delle conferenze inizialmente solo in memoria. Tali impostazioni virtuali vengono successivamente applicate al sito di Redmond. A tale scopo, nel primo comando riportato nell'esempio viene utilizzato il cmdlet **New-CsConferencingConfiguration** per creare una nuova raccolta in memoria di impostazioni archiviate nella variabile $x. Il parametro InMemory specifica che la raccolta deve essere creata in memoria anziché essere applicata immediatamente al sito Redmond.

Dopo aver creato la raccolta, il secondo comando imposta il valore della proprietà Organization su Litwareinc. Nel terzo comando, infine, viene utilizzato il cmdlet **Set-CsConferencingConfiguration** per applicare effettivamente le nuove impostazioni al sito Redmond. Se al sito sono già state applicate impostazioni di configurazione delle conferenze, questo comando avrà esito negativo. Se non si chiama il cmdlet **Set-CsConferencingConfiguration**, le nuove impostazioni non verranno mai applicate e verranno rimosse non appena viene terminata la sessione di Windows PowerShell o viene eliminata la variabile $x.

    $x = New-CsConferencingConfiguration -Identity site:Redmond -InMemory
    $x.Organization = "Litwareinc"
    Set-CsConferencingConfiguration -Instance $x

## Descrizione dettagliata

Per le conferenze, la gestione e l'amministrazione vengono controllate da due insiemi di cmdlet distinti. Se si desidera stabilire le operazioni che gli utenti possono o non possono eseguire (ad esempio se possono invitare partecipanti anonimi a una conferenza, offrire la condivisione di applicazioni o trasferire file durante una conferenza), sarà necessario utilizzare i cmdlet **CsConferencingPolicy**.

Gli amministratori devono inoltre poter gestire il servizio Web Conferencing. Devono ad esempio poter eseguire operazioni quali specificare la quantità massima di spazio di archiviazione contenuti assegnata a una singola conferenza e specificare il periodo di tolleranza consentito prima dell'eliminazione automatica del contenuto della conferenza. Devono inoltre poter specificare le porte utilizzate per attività quali la condivisione di applicazioni e il trasferimento di file.

Tali attività possono essere gestite tramite i cmdlet **CsConferencingConfiguration**. Questi cmdlet consentono di gestire i server veri e propri. I cmdlet **CsConferencingConfiguration** (che possono essere applicati all'ambito globale, del sito e del servizio) non vengono infatti utilizzati per specificare se un utente può condividere applicazioni durante una conferenza. Se la condivisione delle applicazioni è abilitata, tali cmdlet consentono tuttavia di indicare quali porte utilizzare per questa attività. Analogamente, i cmdlet consentono di specificare aspetti quali i limiti di archiviazione e i periodi di scadenza, nonché i puntatori agli URL interni ed esterni da cui gli utenti possono ottenere assistenza e risorse per le conferenze.

Quando si installa Lync Server, viene fornita un singola raccolta di impostazioni di configurazione delle conferenze, ovvero la raccolta globale. Se è necessario creare impostazioni personalizzate per un sito o un servizio, è possibile utilizzare il cmdlet **New-CsConferencingConfiguration** per tale scopo. Tali nuove impostazioni potranno tuttavia essere applicate solo all'ambito del sito o del servizio. Non è infatti possibile creare una nuova raccolta globale di impostazioni di configurazione delle conferenze. Inoltre, un singolo sito o servizio non può ospitare più di una raccolta di impostazioni. Se si tenta di creare nuove impostazioni per il sito Redmond che però ospita già una raccolta di impostazioni di configurazione delle conferenze, il comando avrà esito negativo.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsConferencingConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsConferencingConfiguration"}

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
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per la raccolta di impostazioni di configurazione delle conferenze da modificare. Per far riferimento a una raccolta configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity &quot;site:Redmond&quot;. Per fare riferimento a una raccolta nell'ambito del servizio, utilizzare una sintassi simile alla seguente: -Identity &quot;service:ConferencingServer:atl-cs-001.litwareinc.com&quot;. Il servizio Web Conferencing è l'unico servizio che può ospitare queste impostazioni di configurazione.</p></td>
</tr>
<tr class="even">
<td><p><em>ClientAppSharingPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Rappresenta il numero di porta iniziale utilizzato per la condivisione di applicazioni. ClientAppSharingPort deve corrispondere a un numero di porta compreso tra 1024 e 65535, inclusi. Il valore predefinito è 5350.</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientAppSharingPortRange</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il numero totale di porte disponibili per la condivisione di applicazioni. Il valore predefinito è 40. Per determinare quali porte vengono effettivamente utilizzate per la condivisione di applicazioni, utilizzare questo valore e quello di ClientAppSharingPort. Ad esempio, se ClientAppSharingPort è impostato su 5350 e ClientAppSharingPortRange è impostato su 3, sono disponibili le seguenti 3 porte per la condivisione di applicazioni: 5350, 5351, 5352.</p></td>
</tr>
<tr class="even">
<td><p><em>ClientAudioPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Rappresenta il numero di porta iniziale utilizzato per l'audio del client. ClientAudioPort deve corrispondere a un numero di porta compreso tra 1024 e 65535, inclusi. Il valore predefinito è 5350.</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientAudioPortRange</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il numero totale di porta disponibili per l'audio del client. Il valore predefinito è 40. Per determinare quali porte vengono effettivamente utilizzate per l'audio del client, utilizzare questo valore e quello di ClientAudioPort. Ad esempio, se ClientAudioPort è impostato su 5350 e ClientAudioPortRange è impostato su 3, sono disponibili le seguenti 3 porte per l'audio del client: 5350, 5351, 5352.</p></td>
</tr>
<tr class="even">
<td><p><em>ClientFileTransferPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Rappresenta il numero di porta iniziale utilizzato per i trasferimenti di file. ClientFileTransferPort deve corrispondere a un numero di porta compreso tra 1024 e 65535, inclusi. Il valore predefinito è 5350.</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientFileTransferPortRange</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il numero totale di porte disponibili per i trasferimenti di file. Il valore predefinito è 40. Per determinare quali porte vengono effettivamente utilizzate per i trasferimenti di file, utilizzare questo valore e quello di ClientFileTransferPort. Se ad esempio ClientFileTransferPort è impostato su 5350 e ClientFileTransferPortRange è impostato su 3, saranno disponibili le seguenti tre porte per i trasferimenti di file: 5350, 5351, 5352.</p></td>
</tr>
<tr class="even">
<td><p><em>ClientMediaPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Rappresenta il numero di porta iniziale utilizzato per gli elementi multimediali client. Utilizzare questo parametro per i client di Microsoft Office Communicator 2007 R2. ClientMediaPort deve corrispondere a un numero di porta compreso tra 1024 e 65535, inclusi. Il valore predefinito è 5350.</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientMediaPortRange</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il numero totale delle porte disponibili per gli elementi multimediali client. Il valore predefinito è 40. Utilizzare questo parametro per i client di Office Communicator 2007 R2. Per determinare quali porte vengono effettivamente utilizzate per gli elementi multimediali client, utilizzare questo valore e quello di ClientMediaPort. Se ad esempio ClientMediaPort è impostato su 5350 e ClientMediaPortRange è impostato su 3, per gli elementi multimediali client saranno disponibili le tre porte seguenti: 5350, 5351, 5352.</p></td>
</tr>
<tr class="even">
<td><p><em>ClientMediaPortRangeEnabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, i client utilizzeranno l'intervallo di porte specificato per il traffico degli elementi multimediali. Se è impostato su False, ovvero il valore predefinito, qualsiasi porta disponibile (dalla porta 1024 alla porta 65535) verrà utilizzata per gestire il traffico degli elementi multimediali.</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientSipDynamicPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Rappresenta il numero di porta iniziale utilizzato per il traffico SIP. ClientSipDynamicPort deve corrispondere a un numero di porta compreso tra 1024 e 65535, inclusi. Il valore predefinito è 7100.</p></td>
</tr>
<tr class="even">
<td><p><em>ClientSipDynamicPortRange</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il numero totale di porte disponibili per il traffico SIP. Il valore predefinito è 3. Per determinare quali porte vengono effettivamente utilizzate per il traffico SIP, utilizzare questo valore e quello di ClientSipDynamicPort. Se ad esempio ClientSipDynamicPort è impostato su 7100 e ClientSipDynamicPortRange è impostato su 3, saranno disponibili le seguenti tre porte per gli elementi multimediali client: 7100, 7101, 7102.</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientVideoPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Rappresenta il numero di porta iniziale utilizzato per il video del client. ClientVideoPort deve corrispondere a un numero di porta compreso tra 1024 e 65535, inclusi. Il valore predefinito è 5350.</p></td>
</tr>
<tr class="even">
<td><p><em>ClientVideoPortRange</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il numero totale di porte disponibili per il video del client. Il valore predefinito è 40. Per determinare quali porte vengono effettivamente utilizzate per il video del client, utilizzare questo valore e quello di ClientVideoPort. Se ad esempio ClientVideoPort è impostato su 5350 e ClientVideoPortRange è impostato su 3, saranno disponibili le seguenti tre porte per il video del client: 5350, 5351, 5352.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>ConsoleDownloadExternalUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL da cui gli utenti esterni possono scaricare un client supportato, ad esempio Lync Server 2013. Si noti che questa impostazione si applica solo ai client legacy (ad esempio Microsoft Office Communicator 2007 R2) che eseguono l'accesso a un pool di Lync Server.</p></td>
</tr>
<tr class="odd">
<td><p><em>ConsoleDownloadInternalUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL da cui gli utenti interni possono scaricare un client supportato, ad esempio Lync 2013. Si noti che questa impostazione si applica solo ai client legacy (ad esempio Microsoft Office Communicator 2007 R2) che eseguono l'accesso a un pool di Lync Server.</p></td>
</tr>
<tr class="even">
<td><p><em>ContentGracePeriod</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Indica per quanto tempo il contenuto della conferenza resterà sul server dopo la fine di una riunione. Il valore di ContentGracePeriod deve essere specificato utilizzando il formato giorni.ore:minuti:secondi. Ad esempio, per impostare il periodo di tolleranza del contenuto su 30 giorni utilizzare la sintassi seguente: -ContentGracePeriod 30.00:00:00.</p>
<p>Il periodo di tolleranza del contenuto può essere impostato su qualsiasi valore compreso tra 30 minuti (00:30:00) e 180 giorni (180.00:00:00). Il valore predefinito è 15 giorni (15.00:00:00).</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>HelpdeskExternalUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL a cui verranno indirizzati gli utenti esterni che fanno clic su ? durante una conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><em>HelpdeskInternalUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL a cui verranno indirizzati gli utenti interni che fanno clic su ? durante una conferenza.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxBandwidthPerAppSharingServiceMb</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt64</p></td>
<td><p>Indica la larghezza di banda massima (in megabyte) riservata per il servizio conferenze di Condivisione applicazioni. MaxBandwidthPerAppSharingServiceMb può essere impostato su qualsiasi valore intero compreso tra 50 e 100000 inclusi. Il valore predefinito è 375 megabyte.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxContentStorageMb</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Quantità massima di spazio dei file (in megabyte) consentita per l'archiviazione del contenuto delle conferenze. MaxContentStorageMb può essere impostato su qualsiasi valore intero compreso tra 50 e 1024 (1 gigabyte), inclusi. Il valore predefinito è 500.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxUploadFileSizeMb</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Dimensioni totali massime dei file, inclusi stampati e diapositive di PowerPoint, che è possibile utilizzare in una determinata conferenza. Questa impostazione viene in genere utilizzata quando il contenuto della conferenza viene archiviato in Microsoft Exchange Server: impostando una dimensione di caricamento file massima si garantisce che il contenuto utilizzato nella conferenza, e quindi il contenuto che deve essere archiviato, non superi le dimensioni file minime configurate per Microsoft Exchange. Il valore predefinito è 500 megabyte.</p></td>
</tr>
<tr class="even">
<td><p><em>Organization</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome dell'organizzazione che ospita la conferenza.</p></td>
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

Nessuno. Il cmdlet **New-CsConferencingConfiguration** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **New-CsConferencingConfiguration** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConfSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsConferencingConfiguration](get-csconferencingconfiguration.md)  
[Remove-CsConferencingConfiguration](remove-csconferencingconfiguration.md)  
[Set-CsConferencingConfiguration](set-csconferencingconfiguration.md)

