---
title: Get-CsService
TOCTitle: Get-CsService
ms:assetid: f687d41b-2cb3-4c32-ae28-90e25cdd0d6a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413038(v=OCS.15)
ms:contentKeyID: 49302503
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsService

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui servizi e sui ruoli del server utilizzati nell'infrastruttura di Lync Server. Un servizio è un'istanza di un ruolo che è stata distribuita in un pool di Lync Server. Ad esempio, può essere presente un pool di computer che eseguono il servizio di monitoraggio. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsService [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsService [-ApplicationServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-ApplicationDatabase <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-ArchivingServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-ArchivingDatabase <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-BackupServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-CentralManagement <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-CentralManagementDatabase <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-ConferencingServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-Director <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-EdgeServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-TrustedApplicationPool <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-FileStore <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-PersistentChatServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-PersistentChatComplianceDatabase <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-PersistentChatDatabase <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-LegalInterceptServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-ManagementServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-MediationServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-MonitoringServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-MonitoringDatabase <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-PstnGateway <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-Registrar <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-UserServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-UserDatabase <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-WacServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-WebServer <SwitchParameter>] <COMMON PARAMETERS>

    Get-CsService [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-PoolFqdn <String>]

## Esempi

## ESEMPIO 1

Il comando indicato nell'esempio 1 restituisce informazioni su tutti i servizi e i ruoli del server di Lync Server attualmente in esecuzione nell'organizzazione.

    Get-CsService

## ESEMPIO 2

Nell'esempio 2 vengono restituite informazioni su Servizio applicazione. È possibile restituire le informazioni per altri servizi/ruoli del server semplicemente utilizzando il parametro appropriato. Ad esempio, questo comando restituisce le informazioni sull'archivio file:

    Get-CsService -ApplicationServer

## ESEMPIO 3

Nell'esempio 3 viene restituito il parametro Identity per ciascun servizio presente nel pool atl-cs-001.litwareinc.com. Per eseguire questa attività, il comando innanzitutto chiama il cmdlet **Get-CsService** e il parametro PoolFqdn per restituire solo i servizi e i ruoli del server presenti nel pool atl-cs-001.litwareinc.com. La raccolta viene quindi inviata tramite pipe al cmdlet **Select-Object**, che restituisce il parametro Identity di ogni elemento nella raccolta.

    Get-CsService -PoolFqdn "atl-cs-001.litwareinc.com" | Select-Object Identity

## ESEMPIO 4

Nell'esempio 4 le informazioni vengono restituite per tutti i servizi/ruoli del server trovati nel sito di Redmond. Questa operazione viene eseguita chiamando il cmdlet **Get-CsService** senza alcun parametro, per restituire la raccolta di tutti i servizi e ruoli del server attualmente in uso nell'organizzazione. I dati vengono quindi inviati tramite pipe al cmdlet **Where-Object**, che estrae solo gli elementi in cui la proprietà SiteID è uguale a site:Redmond.

    Get-CsService | Where-Object {$_.SiteID -eq "site:Redmond"}

## ESEMPIO 5

Il comando indicato nell'esempio 5 restituisce le informazioni su tutti i servizi che definiscono Registrar come un servizio dipendente. A tale scopo, il cmdlet **Get-CsService** viene chiamato per restituire la raccolta di tutti i servizi e ruoli del server attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona ogni elemento in cui la proprietà DependentServiceList include il valore stringa "Registrar". I criteri del cmdlet **Where-Object** vengono specificati utilizzando l'operatore -like e il valore con carattere jolly "\*Registrar\*".

    Get-CsService | Where-Object {$_.DependentServiceList -like "*Registrar*"}

## Descrizione dettagliata

Le funzionalità disponibili in Lync Server vengono definite in genere come servizi o ruoli del server. Ad esempio, è possibile configurare Lync Server in modo da salvare automaticamente la trascrizione di ciascuna sessione di messaggistica istantanea che avviene nell'organizzazione. A tale scopo, è necessario installare il ruolo del server server di archiviazione. I servizi e i ruoli del server possono essere configurati contemporaneamente all'installazione di Lync Server o possono essere configurati con il software in esecuzione.

Il cmdlet **Get-CsService** consente di restituire informazioni sui ruoli del server e sui servizi in esecuzione nell'organizzazione. Il cmdlet **Get-CsService**, chiamato senza parametri aggiuntivi, restituisce informazioni dettagliate su tutti i servizi e i ruoli del server in uso. In alternativa, è possibile limitare i dati restituiti a un pool specifico utilizzando il parametro PoolFqdn. È possibile inoltre utilizzare un numero qualsiasi di parametri opzionali per limitare i dati restituiti a un tipo specifico di servizio. Un parametro opzionale è un parametro che non richiede un valore del parametro. Ad esempio, questo comando restituisce informazioni su tutti i server di archiviazione in uso:

Get-CsService –ArchivingServer

È possibile utilizzare solamente un parametro opzionale di questo tipo per ciascun comando. Il comando seguente, che tenta di restituire le informazioni sia sui server di archiviazione sia sui server di monitoraggio, non funzionerà:

Get-CsService –ArchivingServer –MonitoringServer

Per restituire le informazioni per più ruoli del server, è possibile utilizzare il cmdlet **Get-CsService** in modo da restituire la raccolta completa dei dati del servizio e inviare tali dati tramite pipe al cmdlet **Where-Object**:

Get-CsService | Where-Object {$\_.Role –eq "ArchivingServer" –or $\_.Role –eq "MonitoringServer"}

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Get-CsService** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsService"}

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
<td><p><em>ApplicationDatabase</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sui database dell'applicazione utilizzati nell'organizzazione. I database dell'applicazione vengono utilizzati da Servizio applicazione.</p></td>
</tr>
<tr class="even">
<td><p><em>ApplicationServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni su Servizio applicazione. Servizio applicazione consente di eseguire le applicazioni create utilizzando Microsoft Unified Communications Managed API (UCMA).</p></td>
</tr>
<tr class="odd">
<td><p><em>ArchivingDatabase</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sui database di archiviazione utilizzati nell'organizzazione. I database di archiviazione archiviano le trascrizioni delle sessioni di messaggistica istantanea.</p></td>
</tr>
<tr class="even">
<td><p><em>ArchivingServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sui server di archiviazione utilizzati nell'organizzazione. I server di archiviazione consentono di salvare le trascrizioni delle sessioni di messaggistica istantanea.</p></td>
</tr>
<tr class="odd">
<td><p><em>BackupServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sui server di backup utilizzati nell'organizzazione.</p></td>
</tr>
<tr class="even">
<td><p><em>CentralManagement</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sul servizio di gestione centrale utilizzato nell'organizzazione. Il servizio servizio di gestione centrale viene utilizzato per inviare dati di configurazione ai computer che eseguono servizi di Lync Server.</p></td>
</tr>
<tr class="odd">
<td><p><em>CentralManagementDatabase</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sul archivio di gestione centrale utilizzato nell'organizzazione. Il archivio di gestione centrale mantiene le informazioni di configurazione per Lync Server.</p></td>
</tr>
<tr class="even">
<td><p><em>ConferencingServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sul servizio servizio A/V Conferencing utilizzato nell'organizzazione. servizio A/V Conferencing è utilizzato per gestire le riunioni e le conferenze online.</p></td>
</tr>
<tr class="odd">
<td><p><em>Director</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sui Director utilizzati nell'organizzazione. I Director sono configurati per gestire le richieste degli utenti e l'autenticazione utente, ma non per ospitare gli account utente. In genere i Director vengono utilizzati per gestire le richieste degli utenti esterni.</p></td>
</tr>
<tr class="even">
<td><p><em>EdgeServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sui server perimetrali utilizzati nell'organizzazione. I server perimetrali forniscono connettività tra la rete interna ed Internet.</p></td>
</tr>
<tr class="odd">
<td><p><em>FileStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sugli archivi file utilizzati nell'organizzazione. L'archivio file viene utilizzato per conservare i file di Lync Server, quali i file audio utilizzati dal servizio Annuncio.</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare i caratteri jolly per specificare il servizio (o i servizi) da restituire. Non è possibile utilizzare i parametri Filter e Identity nello stesso comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>L'identificatore univoco del servizio o del ruolo del server specifico da restituire. Ad esempio: -Identity &quot;Registrar:atl-cs-001.litwareinc.com&quot;.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>LegalInterceptServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sui server di intercettazione legale utilizzati nell'organizzazione. I server di intercettazione legale consentono l'intercettazione in tempo reale delle comunicazioni di messaggistica istantanea in Office 365.</p></td>
</tr>
<tr class="odd">
<td><p><em>ManagementServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sul server di gestione centrale utilizzato nell'organizzazione. server di gestione centrale in genere è collocato nei Front End Server ed è responsabile dell'accesso alle informazioni nel archivio di gestione centrale.</p></td>
</tr>
<tr class="even">
<td><p><em>MediationServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sui Mediation Server utilizzati nell'organizzazione. I Mediation Server consentono di costituire un ponte tra la rete VoIP aziendale e la rete PSTN (Public Switched Telephone Network).</p></td>
</tr>
<tr class="odd">
<td><p><em>MonitoringDatabase</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sui database di monitoraggio utilizzati nell'organizzazione. I database di monitoraggio archiviano le informazioni relative all'utilizzo del telefono e alla qualità delle chiamate di VoIP aziendale.</p></td>
</tr>
<tr class="even">
<td><p><em>MonitoringServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sui server di monitoraggio utilizzati nell'organizzazione. I server di monitoraggio vengono utilizzati per tenere traccia dell'utilizzo del telefono e della qualità delle chiamate di VoIP aziendale.</p></td>
</tr>
<tr class="odd">
<td><p><em>PersistentChatComplianceDatabase</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sui database utilizzati per mantenere le informazioni di conformità di Chat persistente.</p></td>
</tr>
<tr class="even">
<td><p><em>PersistentChatDatabase</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sui database utilizzati per mantenere le informazioni di conformità di Chat persistente.</p></td>
</tr>
<tr class="odd">
<td><p><em>PersistentChatServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sui server di Chat persistente utilizzati nell'organizzazione.</p></td>
</tr>
<tr class="even">
<td><p><em>PoolFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome di dominio completo del pool che ospita il servizio o il ruolo del server. Se si utilizza il parametro PoolFqdn senza specificare un parametro specifico del servizio, verranno restituiti tutti i servizi e i ruoli del server trovati sul pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>PstnGateway</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sui gateway PSTN (Public Switched Telephone Network) utilizzati nell'organizzazione. I gateway PSTN convertono i segnali inviati dai dispositivi VoIP aziendale in segnali che possono essere compresi dai dispositivi PSTN e viceversa.</p></td>
</tr>
<tr class="even">
<td><p><em>Registrar</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sui Registrar utilizzati nell'organizzazione. I Registrar vengono utilizzati per autenticare gli utenti e tenere traccia dello stato corrente di un utente.</p></td>
</tr>
<tr class="odd">
<td><p><em>TrustedApplicationPool</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sui pool di applicazioni attendibili utilizzati nell'organizzazione. In tali pool sono ospitati i computer che eseguono applicazioni attendibili.</p></td>
</tr>
<tr class="even">
<td><p><em>UserDatabase</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sul database degli utenti utilizzato nell'organizzazione. I database utente archiviano i dati necessari al servizio Server utente.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sul Servizi utente utilizzato nell'organizzazione. Il servizio Servizi utente consente di eseguire la replica degli utenti, il provisioning di tipo in-band, la pubblicazione e le notifiche di presenza e lo scambio delle schede contatto.</p></td>
</tr>
<tr class="even">
<td><p><em>WacServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sui server di Office Web Apps utilizzati con Microsoft Lync Server. Il server di Office Web Apps era precedentemente denominato &quot;WacServer&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>WebServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sul servizi Web utilizzato nell'organizzazione. Il servizio servizi Web ospita applicazioni basate su Web quali il Servizio Rubrica.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsService** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Get-CsService** restituisce oggetti diversi sulla base dei parametri utilizzati durante la chiamata del cmdlet. Ad esempio, se si include il parametro MonitoringDatabase, il cmdlet **Get-CsService** restituisce le istanze dell'oggetto Microsoft.Rtc.Management.Xds.DisplayMonitoringDatabase. Per determinare gli oggetti restituiti utilizzando altri parametri, effettuare la chiamata del cmdlet **Get-CsService** utilizzando uno di questi parametri e inviare quindi tramite pipe l'oggetto restituito al cmdlet **Get-Member**. Ad esempio: Get-CsService -Registrar | Get-Member.

## Vedere anche

#### Ulteriori risorse

[Set-CsApplicationServer](set-csapplicationserver.md)  
[Set-CsArchivingServer](set-csarchivingserver.md)  
[Set-CsConferenceServer](set-csconferenceserver.md)  
[Set-CsDirector](set-csdirector.md)  
[Set-CsEdgeServer](set-csedgeserver.md)  
[Set-CsManagementServer](set-csmanagementserver.md)  
[Set-CsMediationServer](set-csmediationserver.md)  
[Set-CsMonitoringServer](set-csmonitoringserver.md)  
[Set-CsRegistrar](set-csregistrar.md)  
[Set-CsUserServer](set-csuserserver.md)  
[Set-CsWebServer](set-cswebserver.md)

