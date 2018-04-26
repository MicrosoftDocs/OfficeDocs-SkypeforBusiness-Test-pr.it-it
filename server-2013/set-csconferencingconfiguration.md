---
title: Set-CsConferencingConfiguration
TOCTitle: Set-CsConferencingConfiguration
ms:assetid: c468d7fd-fb2c-469c-85fb-58e0834aac36
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412969(v=OCS.15)
ms:contentKeyID: 49301885
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsConferencingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta esistente di impostazioni di configurazione delle conferenze. Tali impostazioni determinano aspetti quali la dimensione massima consentita per il contenuto e gli stampati delle riunioni, il periodo di tolleranza del contenuto (ovvero il periodo di tempo in cui il contenuto rimarrà archiviato prima di essere eliminato) e gli URL per i download interni ed esterni del client supportato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsConferencingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsConferencingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ClientAppSharingPort <UInt16>] [-ClientAppSharingPortRange <UInt32>] [-ClientAudioPort <UInt16>] [-ClientAudioPortRange <UInt32>] [-ClientFileTransferPort <UInt16>] [-ClientFileTransferPortRange <UInt32>] [-ClientMediaPort <UInt16>] [-ClientMediaPortRange <UInt32>] [-ClientMediaPortRangeEnabled <$true | $false>] [-ClientSipDynamicPort <UInt16>] [-ClientSipDynamicPortRange <UInt32>] [-ClientVideoPort <UInt16>] [-ClientVideoPortRange <UInt32>] [-Confirm [<SwitchParameter>]] [-ConsoleDownloadExternalUrl <String>] [-ConsoleDownloadInternalUrl <String>] [-ContentGracePeriod <TimeSpan>] [-Force <SwitchParameter>] [-HelpdeskExternalUrl <String>] [-HelpdeskInternalUrl <String>] [-MaxBandwidthPerAppSharingServiceMb <UInt64>] [-MaxContentStorageMb <UInt16>] [-MaxUploadFileSizeMb <UInt16>] [-Organization <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 il cmdlet **Set-CsConferencingConfiguration** modifica l'istanza globale delle impostazioni di configurazione delle conferenze. In questo caso il comando imposta il valore della proprietà Organization su Litwareinc. Questa operazione viene effettuata includendo il parametro Organization seguito dal nome dell'organizzazione: Litwareinc.

    Set-CsConferencingConfiguration -Identity global -Organization Litwareinc

## ESEMPIO 2

L'esempio 2 è un'estensione del primo esempio. In questo caso il comando modifica il valore della proprietà Organization per ciascuna raccolta di impostazioni di configurazione delle conferenze attualmente in uso. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsConferencingConfiguration** per recuperare una raccolta di tutte le impostazioni di configurazione delle conferenze. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsConferencingConfiguration**, che seleziona ogni elemento della raccolta e cambia il valore della proprietà Organization in Litwareinc.

    Get-CsConferencingConfiguration | Set-CsConferencingConfiguration -Organization Litwareinc

## ESEMPIO 3

Il comando riportato nell'esempio 3 cambia il valore della proprietà MaxContentStorageMb per tutte le impostazioni di configurazione delle conferenze applicate nell'ambito del sito. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsConferencingConfiguration** con il parametro Filter. Il valore di filtro "site:\*" assicura che vengano restituite solo le impostazioni con valore Identity che inizia con i caratteri "site:". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsConferencingConfiguration**, che cambia in 50 il valore della proprietà MaxContentStorageMb di ogni elemento nella raccolta.

    Get-CsConferencingConfiguration -Filter site:* | Set-CsConferencingConfiguration -MaxContentStorageMb 50 

## ESEMPIO 4

Nell'esempio 4, vengono modificate tutte le impostazioni di configurazione della conferenza che consentono l'archiviazione di oltre 100 megabyte di contenuto per impostare l'archiviazione di contenuto massima consentita su 100 megabyte. Per eseguire questa attività, il comando chiama innanzitutto il cmdlet **Get-CsConferencingConfiguration** senza alcun parametro per restituire una raccolta di tutte le impostazioni di configurazione delle conferenze attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona le impostazioni con proprietà MaxContentStorageMB maggiore di 100. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsConferencingConfiguration**, che seleziona ogni elemento della raccolta e imposta il valore della proprietà MaxContentStorageMB su 100.

    Get-CsConferencingConfiguration | Where-Object {$_.MaxContentStorageMb -gt 100} | Set-CsConferencingConfiguration -MaxContentStorageMB 100

## ESEMPIO 5

Nell'esempio 5 vengono recuperate le impostazioni di configurazione della conferenza per il sito Redmond (-Identity site:Redmond) e si modifica il valore della proprietà ContentGracePeriod, mediante l'impostazione del periodo di tolleranza su 22 ore (22 ore: 00 minuti: 00 secondi).

    Set-CsConferencingConfiguration -Identity site:Redmond -ContentGracePeriod "22:00:00"

## ESEMPIO 6

Nell'esempio 6, vengono modificate tutte le impostazioni di configurazione della conferenza nel cui elenco non compare Fabrikam come proprietà Organization. In particolare, a tutte le impostazioni viene assegnato Litwareinc come nuova organizzazione. Per eseguire questa attività, il comando chiama innanzitutto il cmdlet **Get-CsConferencingConfiguration** senza alcun parametro. Viene restituita una raccolta di tutte le impostazioni delle conferenze attualmente in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona tutte le impostazioni con proprietà Organization non uguale a (-ne) Fabrikam. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsConferencingConfiguration**. A sua volta, il cmdlet **Set-CsConferencingConfiguration** seleziona ogni elemento nella raccolta e cambia il valore della proprietà Organization in Litwareinc.

    Get-CsConferencingConfiguration | Where-Object {$_.Organization -ne "Fabrikam"} | Set-CsConferencingConfiguration -Organization Litwareinc

## Descrizione dettagliata

Per le conferenze, la gestione e l'amministrazione vengono controllate da due insiemi di cmdlet distinti. Se si desidera stabilire le operazioni che gli utenti possono o non possono eseguire (ad esempio se possono invitare partecipanti anonimi a una conferenza, offrire la condivisione di applicazioni o trasferire file durante una conferenza), sarà necessario utilizzare i cmdlet **CsConferencingPolicy**.

Oltre alle attività degli utenti, gli amministratori devono gestire il servizio Web Conferencing. Devono ad esempio poter eseguire operazioni quali specificare la quantità massima di spazio di archiviazione contenuti assegnata a una singola conferenza e specificare il periodo di tolleranza consentito prima dell'eliminazione automatica del contenuto della conferenza. Devono inoltre poter specificare le porte utilizzate per attività quali la condivisione di applicazioni e il trasferimento di file.

Tali attività possono essere gestite tramite i cmdlet **CsConferencingConfiguration**. Questi cmdlet consentono di gestire i server veri e propri. I cmdlet **CsConferencingConfiguration** (che possono essere applicati all'ambito globale, del sito e del servizio) non vengono infatti utilizzati per specificare se un utente può condividere applicazioni durante una conferenza. Se la condivisione delle applicazioni è abilitata, tali cmdlet consentono tuttavia di indicare quali porte utilizzare per questa attività. Analogamente, i cmdlet consentono di specificare aspetti quali i limiti di archiviazione e i periodi di scadenza, nonché i puntatori agli URL interni ed esterni da cui gli utenti possono ottenere assistenza e risorse per le conferenze.

Quando si installa Lync Server, viene fornita un singola raccolta di impostazioni di configurazione delle conferenze, ovvero la raccolta globale. Se è necessario creare impostazioni personalizzate per un sito o un servizio, è possibile utilizzare il cmdlet **New-CsConferencingConfiguration** per tale scopo. Una volta create queste impostazioni personalizzate, è possibile modificarle oppure modificare la raccolta globale utilizzando il cmdlet **Set-CsConferencingConfiguration**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsConferencingConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsConferencingConfiguration"}

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
<td><p><em>ClientAppSharingPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Rappresenta il numero di porta iniziale utilizzato per la condivisione di applicazioni. ClientAppSharingPort deve corrispondere a un numero di porta compreso tra 1024 e 65535, inclusi. Il valore predefinito è 5350.</p></td>
</tr>
<tr class="even">
<td><p><em>ClientAppSharingPortRange</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il numero totale di porte disponibili per la condivisione di applicazioni. Il valore predefinito è 40. Per determinare quali porte vengono effettivamente utilizzate per la condivisione di applicazioni, utilizzare questo valore e quello di ClientAppSharingPort. Ad esempio, se ClientAppSharingPort è impostato su 5350 e ClientAppSharingPortRange è impostato su 3, sono disponibili le seguenti 3 porte per la condivisione di applicazioni: 5350, 5351, 5352.</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientAudioPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Rappresenta il numero di porta iniziale utilizzato per l'audio del client. ClientAudioPort deve corrispondere a un numero di porta compreso tra 1024 e 65535, inclusi. Il valore predefinito è 5350.</p></td>
</tr>
<tr class="even">
<td><p><em>ClientAudioPortRange</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il numero totale di porte disponibili per l'audio del client. Il valore predefinito è 40. Per determinare quali porte vengono effettivamente utilizzate per l'audio del client, utilizzare questo valore e quello di ClientAudioPort. Se ad esempio ClientAudioPort è impostato su 5350 e ClientAudioPortRange è impostato su 3, saranno disponibili le seguenti tre porte per l'audio del client: 5350, 5351, 5352.</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientFileTransferPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Rappresenta il numero di porta iniziale utilizzato per i trasferimenti di file. ClientFileTransferPort deve corrispondere a un numero di porta compreso tra 1024 e 65535, inclusi. Il valore predefinito è 5350.</p></td>
</tr>
<tr class="even">
<td><p><em>ClientFileTransferPortRange</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il numero totale di porte disponibili per i trasferimenti di file. Il valore predefinito è 40. Per determinare quali porte vengono effettivamente utilizzate per i trasferimenti di file, utilizzare questo valore e quello di ClientFileTransferPort. Se ad esempio ClientFileTransferPort è impostato su 5350 e ClientFileTransferPortRange è impostato su 3, saranno disponibili le seguenti tre porte per i trasferimenti di file: 5350, 5351, 5352.</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientMediaPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Rappresenta il numero di porta iniziale utilizzato per gli elementi multimediali client. Utilizzare questo parametro per i client di Microsoft Office Communicator 2007 R2. ClientMediaPort deve corrispondere a un numero di porta compreso tra 1024 e 65535, inclusi. Il valore predefinito è 5350.</p></td>
</tr>
<tr class="even">
<td><p><em>ClientMediaPortRange</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il numero totale delle porte disponibili per gli elementi multimediali client. Il valore predefinito è 40. Utilizzare questo parametro per i client di Office Communicator 2007 R2. Per determinare quali porte vengono effettivamente utilizzate per gli elementi multimediali client, utilizzare questo valore e quello di ClientMediaPort. Se ad esempio ClientMediaPort è impostato su 5350 e ClientMediaPortRange è impostato su 3, per gli elementi multimediali client saranno disponibili le tre porte seguenti: 5350, 5351, 5352.</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientMediaPortRangeEnabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, i client utilizzeranno l'intervallo di porte specificato per il traffico degli elementi multimediali. Se è impostato su False, ovvero il valore predefinito, qualsiasi porta disponibile (dalla porta 1024 alla porta 65535) verrà utilizzata per gestire il traffico degli elementi multimediali.</p></td>
</tr>
<tr class="even">
<td><p><em>ClientSipDynamicPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Rappresenta il numero di porta iniziale utilizzato per il traffico SIP. ClientSipDynamicPort deve corrispondere a un numero di porta compreso tra 1024 e 65535, inclusi. Il valore predefinito è 7100.</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientSipDynamicPortRange</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il numero totale di porte disponibili per il traffico SIP. Il valore predefinito è 3. Per determinare quali porte vengono effettivamente utilizzate per il traffico SIP, utilizzare questo valore e quello di ClientSipDynamicPort. Ad esempio, se ClientSipDynamicPort è impostato su 7100 e ClientSipDynamicPortRange è impostato su 3, sono disponibili le seguenti 3 per gli elementi multimediali client: 7100, 7101, 7102.</p></td>
</tr>
<tr class="even">
<td><p><em>ClientVideoPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Rappresenta il numero di porta iniziale utilizzato per il video del client. ClientVideoPort deve corrispondere a un numero di porta compreso tra 1024 e 65535, inclusi. Il valore predefinito è 5350.</p></td>
</tr>
<tr class="odd">
<td><p><em>ClientVideoPortRange</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il numero totale di porte disponibili per il video del client. Il valore predefinito è 40. Per determinare quali porte vengono effettivamente utilizzate per il video del client, utilizzare questo valore e quello di ClientVideoPort. Se ad esempio ClientVideoPort è impostato su 5350 e ClientVideoPortRange è impostato su 3, saranno disponibili le seguenti tre porte per il video del client: 5350, 5351, 5352.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>ConsoleDownloadExternalUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL da cui gli utenti esterni possono scaricare un client supportato, ad esempio Lync 2013. Si noti che questa impostazione si applica solo ai client legacy (ad esempio Microsoft Office Communicator 2007 R2) che eseguono l'accesso a un pool di Lync Server.</p></td>
</tr>
<tr class="even">
<td><p><em>ConsoleDownloadInternalUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL da cui gli utenti interni possono scaricare un client supportato, ad esempio Lync 2013. Si noti che questa impostazione si applica solo ai client legacy (ad esempio Microsoft Office Communicator 2007 R2) che eseguono l'accesso a un pool di Lync Server.</p></td>
</tr>
<tr class="odd">
<td><p><em>ContentGracePeriod</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Indica per quanto tempo il contenuto della conferenza resterà sul server dopo la fine della conferenza. Il valore di ContentGracePeriod deve essere specificato utilizzando il formato giorni.ore:minuti:secondi. Per impostare ad esempio il periodo di tolleranza del contenuto su 30 giorni, utilizzare la seguente sintassi: -ContentGracePeriod 30.00:00:00.</p>
<p>Il periodo di tolleranza del contenuto può essere impostato su qualsiasi valore compreso tra 30 minuti (00:30:00) e 180 giorni (180.00:00:00). Il valore predefinito è 15 giorni (15.00:00:00).</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>HelpdeskExternalUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL a cui verranno indirizzati gli utenti esterni che fanno clic su ? durante una conferenza.</p></td>
</tr>
<tr class="even">
<td><p><em>HelpdeskInternalUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL a cui verranno indirizzati gli utenti interni che fanno clic su ? durante una conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per la raccolta di impostazioni di configurazione delle conferenze da modificare. Per fare riferimento alla raccolta globale, utilizzare questa sintassi: -Identity global. Per far riferimento a una raccolta configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity &quot;site:Redmond&quot;. Per fare riferimento a una raccolta nell'ambito del servizio, utilizzare una sintassi simile alla seguente: -Identity &quot;service:ConferencingServer:atl-cs-001.litwareinc.com&quot;. Il servizio Web Conferencing è l'unico servizio che può ospitare queste impostazioni di configurazione.</p>
<p>Se questo parametro non è specificato, il cmdlet <strong>Set-CsConferencingConfiguration</strong> modifica automaticamente le impostazioni globali.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto ConfSettings</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
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
<td><p>Quantità massima di spazio dei file (in megabyte) consentita per l'archiviazione del contenuto della riunione. MaxContentStorageMb può essere impostato su qualsiasi valore intero compreso tra 50 e 1024 (1 gigabyte), inclusi. Il valore predefinito è 500 megabyte.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConfSettings. Il cmdlet **Set-CsConferencingConfiguration** accetta le istanze da pipeline dell'oggetto di configurazione delle conferenze.

## Tipi restituiti

Il cmdlet **Set-CsConferencingConfiguration** non restituisce alcun oggetto o valore. Configura invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConfSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsConferencingConfiguration](get-csconferencingconfiguration.md)  
[New-CsConferencingConfiguration](new-csconferencingconfiguration.md)  
[Remove-CsConferencingConfiguration](remove-csconferencingconfiguration.md)

