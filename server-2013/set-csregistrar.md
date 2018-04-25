---
title: Set-CsRegistrar
TOCTitle: Set-CsRegistrar
ms:assetid: e0c31acc-179c-4423-910e-8bd7807e6489
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398993(v=OCS.15)
ms:contentKeyID: 49302238
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsRegistrar

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di modificare le proprietà di uno o più servizi di registrazione. I servizi di registrazione vengono utilizzati per autenticare richieste di accesso e per conservare informazioni sulla disponibilità e sullo stato degli utenti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsRegistrar [-Identity <XdsGlobalRelativeIdentity>] [-ArchivingDatabase <String>] [-ArchivingServer <String>] [-BackupRegistrar <String>] [-Confirm [<SwitchParameter>]] [-EdgeServer <String>] [-EnableAutomaticFailover <$true | $false>] [-FailbackDetectionInterval <TimeSpan>] [-FailureDetectionInterval <TimeSpan>] [-Force <SwitchParameter>] [-LyssWcfMtlsPort <UInt16>] [-MirrorArchivingDatabase <String>] [-MirrorMonitoringDatabase <String>] [-MonitoringDatabase <String>] [-MonitoringServer <String>] [-Registrar <String>] [-SipHealthPort <UInt16>] [-SipPort <UInt16>] [-SipServerTcpPort <UInt16>] [-UserServer <String>] [-WebPort <UInt16>] [-WebServer <String>] [-WhatIf [<SwitchParameter>]] [-WinFabClientConnectionPort <UInt16>] [-WinFabFederationPort <UInt16>] [-WinFabIPCPort <UInt16>] [-WinFabLeaseAgentPort <UInt16>] [-WinFabReplicationPort <UInt16>] [-XmppGatewaySipPort <UInt16>]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 imposta la porta SIP per il servizio di registrazione Registrar:atl-cs-001.litwareinc.com su 5072.

    Set-CsRegistrar -Identity "Registrar:atl-cs-001.litwareinc.com" -SipPort 5072

## ESEMPIO 2

Nell'esempio 2 viene impostata la porta SIP su 5072 per tutti i servizi di registrazione presenti nell'organizzazione. A tale scopo, nel comando vengono innanzitutto utilizzati il cmdlet **Get-CsService** e il parametro Registrar per restituire una raccolta di tutti i servizi di registrazione attualmente in uso. La raccolta viene quindi inviata al cmdlet **ForEach-Object**, che individua i singoli servizi di registrazione presenti nella raccolta ed esegue il cmdlet **Set-CsRegistrar** per impostare su 5072 la porta SIP.

    Get-CsService -Registrar | ForEach-Object {Set-CsRegistrar -Identity $_.Identity -SipPort 5072}

## ESEMPIO 3

Nell'esempio 3 vengono configurati sia un servizio di registrazione di backup (BackupRegistrar) sia il failover automatico (EnableAutomaticFailover) per il servizio di registrazione Registrar:atl-cs-001.litwareinc.com.

    Set-CsRegistrar -Identity "Registrar:atl-cs-001.litwareinc.com" -BackupRegistrar "Registrar:dublin-cs-001.litwareinc.com" -EnableAutomaticFailover $True

## Descrizione dettagliata

Il servizio di registrazione è forse il componente più importante di Lync Server. Senza tale servizio, gli utenti non potrebbero infatti accedere al sistema e Lync Server non potrebbe tenere traccia degli utenti e del relativo stato corrente. Quando un utente accede a Lync Server, l'endpoint da cui viene eseguito l'accesso (sia che si tratti di un computer, di un telefono cellulare o di qualsiasi altro dispositivo) invia una richiesta REGISTER al server di registrazione che, a sua volta, risponde inviando al dispositivo client una richiesta di autenticazione delle credenziali dell'utente. Se il client supera la richiesta di autenticazione (presentando un set di credenziali valido), l'utente viene autenticato e le informazioni sull'endpoint (quali indirizzo IP, porta e nome utente) vengono registrate nel database di registrazione. Quando un utente si disconnette, queste informazioni vengono rimosse dal database. Tra l'accesso e la disconnessione, il servizio di registrazione mantiene aggiornate le informazioni sullo stato e agevola l'instradamento dei messaggi da e verso l'utente.

Il cmdlet **Set-CsRegistrar** consente di modificare le proprietà di uno o più servizi di registrazione presenti nell'organizzazione. Consente ad esempio di modificare le impostazioni delle porte e di specificare l'azione da eseguire nel caso in cui un servizio di registrazione non sia più disponibile.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsRegistrar** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsRegistrar\\b"}

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
<td><p><em>ArchivingDatabase</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Identità servizio del database utilizzato dal servizio di archiviazione.</p></td>
</tr>
<tr class="even">
<td><p><em>ArchivingServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Posizione del servizio del server di archiviazione da associare al servizio di registrazione. Ad esempio: -ArchivingServer &quot;ArchivingServer:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>BackupRegistrar</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Posizione del servizio di registrazione da utilizzare se questo servizio di registrazione non è disponibile. Ad esempio: -BackupRegistrar &quot;Registrar:dublin-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>EdgeServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Posizione del servizio del server perimetrale da associare al servizio di registrazione. Ad esempio: -EdgeServer &quot;EdgeServer:atl-edge-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableAutomaticFailover</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se True, ogni volta che il servizio di registrazione primario non risulterà disponibile, verrà utilizzato quello di backup. Se False, il servizio di registrazione di backup non verrà utilizzato quando il servizio di registrazione primario non risulterà disponibile.</p>
<p>Questo parametro influisce anche sugli utenti che si sono registrati con un servizio di registrazione di backup. Se questo parametro è impostato su True, questi utenti verranno cancellati dal servizio di registrazione di backup e registrati nuovamente sul servizio di registrazione primario se e quando questo servizio di registrazione diventerà disponibile.</p></td>
</tr>
<tr class="odd">
<td><p><em>FailbackDetectionInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Specifica per quanto tempo il sistema deve attendere prima di verificare se un servizio di registrazione non più disponibile è tornato di nuovo disponibile. Se EnableAutomaticFailover è stato impostato su True, il sistema eseguirà il &quot;failover&quot; sul servizio di registrazione di backup ogni volta che un servizio di registrazione non risulterà più disponibile. In altri termini, il sistema tenterà semplicemente di connettere al servizio di registrazione di backup gli utenti connessi al servizio di registrazione non funzionante.</p>
<p>La proprietà FailbackDetectionInterval specifica quanto tempo il sistema deve attendere prima di verificare se il servizio di registrazione originale è tornato disponibile. In caso affermativo, Lync Server tenterà di eseguire il &quot;failback&quot; su tale servizio di registrazione. A seguito del failback, si tornerà al servizio di registrazione inizialmente in uso. In altri termini, gli utenti verranno di nuovo connessi al rispettivo servizio di registrazione originale.</p>
<p>Il failback è esclusivamente un processo automatico. Non è pertanto possibile eseguire manualmente il failback da un servizio di registrazione all'altro.</p>
<p>l'intervallo di rilevamento può essere impostato su un valore qualsiasi compreso fra 30 e 84.400 secondi (24 ore). Specificare tale intervallo nel formato ore:minuti:secondi. Nel seguente esempio l'intervallo viene impostato su 1 ora e 15 minuti: - FailbackDetectionInterval 01:15:00.</p>
<p>Questo parametro può essere utilizzato solo se è stato specificato un servizio di registrazione di backup.</p></td>
</tr>
<tr class="even">
<td><p><em>FailureDetectionInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Specifica l'intervallo di tempo che il sistema deve attendere prima di stabilire che un servizio di registrazione non è disponibile. Se EnableAutomaticFailover è stato impostato su True, il sistema tenterà di connettere gli utenti al servizio di registrazione di backup.</p>
<p>l'intervallo di rilevamento può essere impostato su un valore qualsiasi compreso fra 30 e 84.400 secondi (24 ore). Specificare tale intervallo nel formato ore:minuti:secondi. Nel seguente esempio l'intervallo viene impostato su 1 ora e 15 minuti: - FailureDetectionInterval 01:15:00.</p>
<p>Questo parametro può essere utilizzato solo se è stato specificato un servizio di registrazione di backup.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Posizione del servizio di registrazione da modificare. Ad esempio: -Identity &quot;Registrar:atl-cs-001.litwareinc.com&quot;.</p>
<p>È possibile omettere il prefisso &quot;Registrar:&quot; quando si specifica un servizio di registrazione. Ad esempio: -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>LyssWcfMtlsPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata da Lync Storage Service (LYSS). Il valore predefinito è 5077.</p></td>
</tr>
<tr class="even">
<td><p><em>MirrorArchivingDatabase</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Identità servizio del database mirror utilizzato dal servizio di archiviazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>MirrorMonitoringDatabase</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Identità servizio del database mirror utilizzato dal servizio di monitoraggio.</p></td>
</tr>
<tr class="even">
<td><p><em>MonitoringDatabase</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Identità servizio del database di monitoraggio associato al servizio di registrazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>MonitoringServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Posizione del servizio del Monitoring Server da associare al servizio di registrazione. Ad esempio: -MonitoringServer &quot;MonitoringServer:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Registrar</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Posizione del servizio di registrazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipHealthPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per il monitoraggio dell'integrità del server.</p></td>
</tr>
<tr class="even">
<td><p><em>SipPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per il traffico SIP (Session Initiation Protocol).</p></td>
</tr>
<tr class="odd">
<td><p><em>SipServerTcpPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta di attesa SIP. Il valore predefinito è 5060.</p></td>
</tr>
<tr class="even">
<td><p><em>UserServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Posizione del servizio del Servizi utente da associare al servizio di registrazione. Ad esempio: -UserServer &quot;UserServer:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>WebPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per comunicare con i server Web.</p></td>
</tr>
<tr class="even">
<td><p><em>WebServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Posizione del servizio del server Web da associare al servizio di registrazione. Ad esempio: -WebServer &quot;WebServer:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
<tr class="even">
<td><p><em>WinFabClientConnectionPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per le connessioni client a Windows Fabric. Il valore predefinito è 5092.</p></td>
</tr>
<tr class="odd">
<td><p><em>WinFabFederationPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per la federazione di Windows Fabric. La federazione si riferisce al processo mediante cui Windows Fabric instrada i messaggi. Il valore predefinito è 5090.</p></td>
</tr>
<tr class="even">
<td><p><em>WinFabIPCPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata da Windows Fabric per la comunicazione interprocesso (IPC, inter-process communication). IPC è una tecnologia che consente lo scambio di dati tra più thread di un processo. Il valore predefinito è 5093.</p></td>
</tr>
<tr class="odd">
<td><p><em>WinFabLeaseAgentPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata dall'agente di lease di Windows Fabric. Gli agenti di lease vengono utilizzati per interagire con il driver di lease a livello di kernel. Il valore predefinito è 5091.</p></td>
</tr>
<tr class="even">
<td><p><em>WinFabReplicationPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per la replica di Windows Fabric. Lync Server 2013 utilizza Windows Fabric per replicare le directory di conferenze in tutti i Front End Server all'interno di un pool di registrazione. Il valore predefinito è 5094.</p></td>
</tr>
<tr class="odd">
<td><p><em>XmppGatewaySipPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata dal gateway XMPP associato al servizio di registrazione. Il protocollo XMPP (Extensible Messaging and Presence Protocol) è un protocollo di comunicazione a standard aperto per lo scambio di messaggi mediante XML. Un partner consentito è un provider di messaggistica istantanea e presenza ai cui utenti è consentito lo scambio di messaggi istantanei e di informazioni sulla presenza con li utenti di Lync Server. Il valore predefinito è 5098.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Set-CsRegistrar** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Set-CsRegistrar** non restituisce alcun oggetto o valore. Modifica invece le istanze esistenti dell'oggetto Microsoft.Rtc.Management.Xds.DisplayRegistrar.

## Vedere anche

#### Ulteriori risorse

[Get-CsService](get-csservice.md)

