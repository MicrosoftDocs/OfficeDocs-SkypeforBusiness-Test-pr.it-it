---
title: Attributi e descrizioni di schema in Lync Server 2013
TOCTitle: Attributi e descrizioni di schema in Lync Server 2013
ms:assetid: b009df76-9c22-471d-b57a-bda009a98261
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412841(v=OCS.15)
ms:contentKeyID: 49301668
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Attributi e descrizioni di schema in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questa sezione vengono descritti tutti gli attributi di schema utilizzati da Lync Server 2013. Per le classi associate agli attributi, vedere [Attributi dello schema in base alla classe in Lync Server 2013](lync-server-2013-schema-attributes-by-class.md). Per un elenco delle classi e degli attributi introdotti per la prima volta in Lync Server 2013, vedere [Modifiche dello schema in Lync Server 2013](lync-server-2013-schema-changes-in-lync-server-2013.md).

Gli attributi che costituiscono coppie collegate sono specificati come collegamenti successivi o collegamenti a ritroso. Un attributo che fa riferimento a un altro oggetto è un collegamento successivo. L'attributo dell'altro oggetto che restituisce il riferimento al primo oggetto è un collegamento a ritroso. I collegamenti successivi sono aggiornabili, mentre i collegamenti a ritroso sono di sola lettura.

Alcuni attributi dispongono di un valore maschera di bit. Per questi attributi, ogni impostazione è rappresentata da un bit e il valore decimale visualizzato rappresenta la posizione del bit. Le posizioni del bit iniziano con bit 0. Ad esempio, 1 (binario) è bit 0 impostato e 10000 (binario) è bit 4 impostato. Ogni bit rappresenta una proprietà. Di seguito sono riportati alcuni esempi:

  - 10000 (binario) ha un valore decimale di 16 (bit 4 impostato).

  - 100000000 (binario) ha un valore decimale di 256 (bit 8 impostato).

  - 1100 (binario) ha un valore decimale di 12 (bit 2 e 3 impostati, le proprietà rappresentate da entrambi i bit sono abilitate).

  - 1111000001 (binario) ha un valore decimale di 961 (bit 0, 6, 7, 8, e 9 impostati, le proprietà per ognuno di questi bit sono abilitate).

### Attributi di schema per Lync Server 2013

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributo</th>
<th>Descrizione</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>dnsHostName</p></td>
<td><p>Attributo esistente in Servizi di dominio Active Directory ora associato alle classi <strong>msRTCSIP-Pool</strong> e <strong>msRTCSIP-MonitoringServer</strong>. Questo attributo specifica il nome di dominio completo di un pool o di Monitoring Server.</p>
<p>È possibile utilizzare 63 caratteri per ciascun segmento e 255 caratteri per l'intero nome di dominio completo.</p></td>
<td><p>Nuovo in Microsoft Office Live Communications Server 2005.</p></td>
</tr>
<tr class="even">
<td><p>msDS-SourceObjectDN</p></td>
<td><p>Questo attributo contiene la rappresentazione di stringa del nome distinto (DN) dell'oggetto in un'altra foresta corrispondente a questo oggetto. Viene utilizzato per l'espansione dei gruppi di distribuzione e la partecipazione automatica. L'attributo viene definito nello schema predefinito di Active Directory per Windows Server 2003 R2.</p>
<p>Per evitare di richiedere un aggiornamento di AD DS a Windows Server 2003 R2, nella preparazione dello schema di Active Directory lo schema di Windows Server 2003 viene esteso utilizzando questa definizione di attributo.</p></td>
<td><p>Nuovo in Microsoft Office Communications Server 2007.</p></td>
</tr>
<tr class="odd">
<td><p>msExchUCVoiceMailSettings</p></td>
<td><p>Questo attributo multivalore contiene le impostazioni della segreteria telefonica ed è condiviso con Messaggistica unificata di Exchange.</p></td>
<td><p>Nuovo in Microsoft Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msExchUserHoldPolicies</p></td>
<td><p>Questo attributo multivalore contiene gli identificatori per i criteri di esenzione che si applicano all'utente. I criteri di esenzione mantengono gli elementi della casetta postale dell'utente per la durata dell'esenzione. Questo attributo è condiviso con Exchange 2013.</p></td>
<td><p>Nuovo in Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-AcpInfo</p></td>
<td><p>Questo attributo archivia le informazioni sui provider di servizi di audioconferenza per un utente.</p></td>
<td><p>Nuovo in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ApplicationDestination</p></td>
<td><p>Questo attributo punta alla voce del servizio trusted per il contatto applicazione.</p></td>
<td><p>Nuovo in Microsoft Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ApplicationList</p></td>
<td><p>Questo attributo contiene un elenco delle applicazioni ospitate nel server applicazioni.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ApplicationOptions</p></td>
<td><p>Questo attributo specifica le opzioni per il contatto applicazione.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ApplicationPrimaryLanguage</p></td>
<td><p>Questo attributo contiene la lingua principale per il contatto applicazione.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ApplicationSecondaryLanguages</p></td>
<td><p>Questo attributo multivalore contiene le lingue secondarie per il contatto applicazione.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ApplicationServerBL</p></td>
<td><p>Questo attributo contiene un elenco di server applicazioni appartenenti al pool. Il collegamento successivo corrispondente a questo attributo di collegamento a ritroso è <strong>msRTCSIP-ApplicationServerPoolLink</strong>.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ApplicationServerPoolLink</p></td>
<td><p>Questo attributo punta al pool cui appartiene il server applicazioni. Si tratta di un collegamento successivo. Il collegamento a ritroso corrispondente è <strong>msRTCSIP-ApplicationServerBL</strong>.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ArchiveDefault (obsoleto)</p></td>
<td><p>-</p></td>
<td><p>Nuovo in Live Communications Server 2005.</p>
<p>Obsoleto in Office Communications Server 2007.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ArchiveDefaultFlags (obsoleto)</p></td>
<td><p>Questo attributo specifica l'impostazione predefinita globale all'interno della foresta per l'archiviazione delle comunicazioni di tutti gli utenti. Viene applicato dal livello agente di archiviazione. I valori validi per questo attributo sono:</p>
<ul>
<li><p><strong>TRUE</strong>: vengono archiviate le comunicazioni di tutti gli utenti</p></li>
<li><p><strong>FALSE</strong>: le comunicazioni degli utenti non vengono archiviate</p></li>
</ul>
<p>Questo attributo controlla a livello globale, all'interno della foresta, la modalità di archiviazione delle comunicazioni degli utenti in una rete interna.</p>
<p><strong>Comportamento di Live Communications Server 2005 (ritirato)</strong></p>
<p>I valori validi per questo attributo sono:</p>
<ul>
<li><p>0: le comunicazioni vengono archiviate con il corpo dei messaggi [bit 0]</p></li>
<li><p>1: le comunicazioni non vengono archiviate con il corpo dei messaggi [bit 0]</p></li>
</ul>
<p><strong>Comportamento di Office Communications Server 2007</strong></p>
<p>I valori validi per questo attributo sono:</p>
<ul>
<li><p>0: ArchiveFederationDefaultWithoutBody (ritirato)</p></li>
<li><p>1-2: ArchiveInternalCommunications</p></li>
<li><p>3-4: ArchiveFederatedCommunications</p></li>
<li><p>5: RecordPresenceRegistrations</p></li>
<li><p>6: RecordIMCallDetails</p></li>
<li><p>7: RecordGroupIMCallDetails</p></li>
<li><p>8: RecordFileTransferInstances</p></li>
<li><p>9: RecordAudioCallDetails</p></li>
<li><p>10: RecordVideoCallDetails</p></li>
<li><p>11: RecordRemoteAssistanceCallDetails</p></li>
<li><p>12: RecordApplicationSharingDetails</p></li>
<li><p>13: RecordMeetingInstantiations</p></li>
<li><p>14: RecordMeetingJoins</p></li>
<li><p>15: RecordDataJoins</p></li>
<li><p>16: RecordAVJoins</p></li>
</ul></td>
<td><p>Nuovo in Live Communications Server 2005.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ArchiveFederationDefault (obsoleto)</p></td>
<td><p>-</p></td>
<td><p>Nuovo in Live Communications Server 2005.</p>
<p>Obsoleto in Office Communications Server 2007.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ArchiveFederationDefaultFlags (obsoleto)</p></td>
<td><p>-</p></td>
<td><p>Nuovo in Live Communications Server 2005.</p>
<p>Obsoleto in Office Communications Server 2007.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ArchivingEnabled</p></td>
<td><p>Questo attributo è un integer utilizzato come campo di bit per determinare se le comunicazioni di un singolo utente verranno archiviate. Questo controllo viene applicato dal livello agente di archiviazione. L'attributo è contrassegnato per la replica nel catalogo globale.</p>
<p>L'ambito di questo attributo è specifico di un singolo utente o contatto. I valori validi e le posizioni di bit associate in Lync Server sono:</p>
<ul>
<li><p>0: Non archiviare (nessun bit impostato)</p></li>
<li><p>1: Ritirato (posizione bit 0)</p></li>
<li><p>2: Ritirato (posizione bit 1)</p></li>
<li><p>4: Archivia comunicazioni interne (posizione bit 2)</p></li>
<li><p>8: Archivia comunicazioni federate (posizione bit 3)</p></li>
</ul>
<p>I valori validi in precedenza in Live Communications Server 2005 sono:</p>
<ul>
<li><p>0: viene utilizzato il valore predefinito specificato da <strong>msRTCSIP-ArchiveDefault</strong> e <strong>msRTCSIP-ArchiveFederation</strong> (in quest'ordine di precedenza):</p>
<ul>
<li><p>1: le comunicazioni vengono archiviate</p></li>
<li><p>2: le comunicazioni non vengono archiviate</p></li>
<li><p>3: le comunicazioni vengono archiviate senza il corpo dei messaggi</p></li>
</ul></li>
</ul></td>
<td><p>Nuovo in Live Communications Server 2005.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ArchivingServerData (obsoleto)</p></td>
<td><p>Questo attributo è riservato per un utilizzo futuro.</p></td>
<td><p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ArchivingServerVersion (obsoleto)</p></td>
<td><p>Questo attributo definisce la versione del Servizio archiviazione. È un tipo di integer crescente in modo monotono che viene incrementato a ogni versione ufficiale del prodotto. I valori validi possibili sono:</p>
<ul>
<li><p>Indefinito: Live Communications Server 2003</p>
<p>                 Live Communications Server 2005</p>
<p>                 Live Communications Server 2005 con SP1</p></li>
<li><p>3: Office Communications Server 2007</p></li>
<li><p>4: Office Communications Server 2007 R2</p></li>
</ul></td>
<td><p>Nuovo in Office Communications Server 2007.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-BackEndServer</p></td>
<td><p>Questo attributo specifica il nome di dominio completo del server back-end del pool. Si tratta di un attributo a valore singolo, poiché può esistere un unico server back-end per ciascun pool.</p>
<p>È possibile utilizzare 63 caratteri per ciascun segmento e 255 caratteri per l'intero nome di dominio completo.</p></td>
<td><p>Nuovo in Live Communications Server 2005.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ConferenceDirectoryHomePool</p></td>
<td><p>Questo attributo contiene l'identificatore del pool in cui si trova la directory conferenze.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ConferenceDirectoryId</p></td>
<td><p>Questo attributo contiene l'identificatore di una directory conferenze.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ConferenceDirectoryTargetPool</p></td>
<td><p>Questo attributo contiene l'identificatore del pool in cui verrà spostata la directory conferenze.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-Default</p></td>
<td><p>Questo attributo booleano definisce se l'utilizzo telefono è predefinito. Se l'attributo è impostato su <strong>TRUE</strong>, l'utilizzo telefono è predefinito e non può essere eliminato dall'amministratore. Se l'attributo è impostato su <strong>FALSE</strong>, l'utilizzo può essere eliminato.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-DefaultCWAExternalURL</p></td>
<td><p>Questo attributo identifica l'URL di Communicator Web Access per gli utenti che si trovano all'esterno dell'organizzazione.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-DefaultCWAInternalURL</p></td>
<td><p>Questo attributo identifica l'URL di Communicator Web Access per gli utenti che si trovano all'interno dell'organizzazione.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-DefaultLocationProfileLink (obsoleto)</p></td>
<td><p>Questo attributo a valore singolo contiene il nome distinto (DN) di un oggetto classe profilo località a esso assegnato.</p>
<p>Collegamento in avanti: <strong>Link ID 11036</strong></p>
<p>Il collegamento a ritroso corrispondente è <strong>msRTCSIP-ServerReferenceBL</strong>.</p></td>
<td><p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-DefaultPolicy (obsoleto)</p></td>
<td><p>Questo attributo booleano specifica se il criterio è predefinito. Il criterio è predefinito se impostato su <strong>TRUE</strong>.</p></td>
<td><p>Nuovo in Office Communications Server 2007</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-DefaultRouteToEdgeProxy (obsoleto)</p></td>
<td><p>Questo attributo specifica il nome di dominio completo dell'server perimetrale che esegue il servizio Access Edge, se è possibile accedervi direttamente, o del bilanciamento del carico hardware per un pool di server che eseguono il servizio Access Edge. Se i server che eseguono servizio Access Edge sono accessibili soltanto tramite uno o più server Director, questo attributo specifica il nome FQDN ed eventualmente il numero di porta del Director o del servizio di bilanciamento del carico hardware per un pool di server Director.</p>
<p>È possibile utilizzare 63 caratteri per ciascun segmento e 255 caratteri per l'intero nome di dominio completo.</p></td>
<td><p>Nuovo in Live Communications Server 2005.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-DefaultRouteToEdgeProxyPort (obsoleto)</p></td>
<td><p>Questo attributo rappresenta il numero di porta da utilizzare per la connessione al server che esegue servizio Access Edge.</p>
<p>Il valore valido è un valore integer che specifica la porta da utilizzare. Il valore predefinito è 5061.</p></td>
<td><p>Nuovo in Live Communications Server 2005.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-DefPresenceSubscriptionTimeout (obsoleto)</p></td>
<td><p>Questo attributo rappresenta il periodo di timeout predefinito per la sottoscrizione relativa alla presenza.</p></td>
<td><p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-DefRegistrationTimeout (obsoleto)</p></td>
<td><p>Questo attributo rappresenta la finestra di timeout predefinita per la registrazione.</p></td>
<td><p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-DefRoamingDataSubscriptionTimeout (obsoleto)</p></td>
<td><p>Questo attributo rappresenta la finestra di timeout predefinita per la sottoscrizione dei dati di roaming.</p></td>
<td><p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-DeploymentLocator</p></td>
<td><p>Questo attributo viene utilizzato in una topologia di domini divisi e contiene un nome di dominio completo (FQDN).</p></td>
<td><p>Nuovo in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-Description (obsoleto)</p></td>
<td><p>Questo attributo di stringa UNICODE a valore singolo contiene una descrizione della route telefonica o della regola di normalizzazione.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-DomainData</p></td>
<td><p>Questo attributo è riservato per un utilizzo futuro.</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-DomainName</p></td>
<td><p>Questo attributo rappresenta un dominio configurato per la funzione di registrazione.</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-EdgeProxyData</p></td>
<td><p>Questo attributo è riservato per un utilizzo futuro.</p></td>
<td><p>Nuovo in Live Communications Server 2005.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-EdgeProxyFQDN</p></td>
<td><p>Questo attributo specifica il nome di dominio completo del server che esegue il servizio Access Edge.</p>
<p>È possibile utilizzare 63 caratteri per ciascun segmento e 255 caratteri per l'intero nome di dominio completo.</p></td>
<td><p>Nuovo in Live Communications Server 2005.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-EnableBestEffortNotify (obsoleto)</p></td>
<td><p>Questo attributo determina se un server genera una richiesta Best Effort NOTIFY (BENOTIFY), anziché una richiesta NOTIFY, in risposta a una richiesta SUBSCRIBE inviata da un client. BENOTIFY è un'estensione ottimizzata del metodo di handshake per la notifica della sottoscrizione, in base alla quale un server genera richieste BENOTIFY anziché richieste NOTIFY standard. A differenza di NOTIFY, BENOTIFY non richiede una risposta 200 OK dal client con conseguenti vantaggi in termini di prestazioni.</p>
<p>I valori validi sono <strong>TRUE</strong> o <strong>FALSE</strong>.</p>

> [!NOTE]
> Live Communications Server 2003 non supporta richieste BENOTIFY. Per garantire l'interoperabilità con applicazioni server basate su API server di Live Communications Server 2003 in esecuzione su server Live Communications Server 2005 server di terze parti, è possibile disattivare le richieste BENOTIFY impostando il relativo valore su <STRONG>FALSE</STRONG>. La funzionalità BENOTIFY non è attualmente inclusa nel processo di standardizzazione SIP sviluppato dalla IETF (Internet Engineering Task Force).


</td>
<td><p>Nuovo in Live Communications Server 2005.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-EnableFederation (obsoleto)</p></td>
<td><p>Questo attributo è un'opzione globale utilizzata dagli amministratori IT per specificare se gli utenti possono comunicare o meno con utenti di altre organizzazioni. Consente agli amministratori di sovrascrivere l'attributo <strong>FederationEnabled</strong> di un singolo utente. Questo attributo risulta inoltre utile per proteggere la rete interna da attacchi via Internet causati da worm, virus o da attacchi diretti contro l'organizzazione.</p>
<p>I valori validi e le posizioni di bit associate sono:</p>
<ul>
<li><p>1: abilitato per la connettività per messaggistica istantanea pubblica (posizione bit 0)</p></li>
<li><p>2: riservato (posizione bit 1)</p></li>
<li><p>4: riservato (posizione bit 2)</p></li>
<li><p>8: riservato (posizione bit 3)</p></li>
<li><p>16: abilitato per il controllo delle chiamate remote [Telefonia] (posizione bit 4)</p></li>
<li><p>64: AllowOrganizeMeetingWithAnonymousParticipants (consente agli utenti di invitare utenti anonimi alle riunioni) (posizione bit 6)</p></li>
<li><p>128: UCEnabled (abilita gli utenti per le comunicazioni unificate) (posizione bit 7)</p></li>
<li><p>256: EnabledForEnhancedPresence (abilita l'utente per la connettività per messaggistica istantanea pubblica) (posizione bit 8)</p></li>
<li><p>512: RemoteCallControlDualMode (modalità doppia di controllo delle chiamate remote) (posizione bit 9)</p></li>
</ul></td>
<td><p>Nuovo in Live Communications Server 2005.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-EnterpriseServices</p></td>
<td><p>Questo attributo indica se Enterprise Services è caricato nel server specificato.</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ExtensionData</p></td>
<td><p>Questo attributo è riservato per un utilizzo futuro.</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ExternalAccessCode</p></td>
<td><p>Questo attributo contiene il prefisso per l'accesso esterno.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-FederationEnabled</p></td>
<td><p>Questo attributo determina se un singolo utente è abilitato per la federazione. Viene applicato dal livello Enterprise Services. L'attributo è contrassegnato per la replica nel catalogo globale.</p>
<p>I valori validi sono <strong>TRUE</strong> o <strong>FALSE</strong>.</p></td>
<td><p>Nuovo in Live Communications Server 2005.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-FrontEndServers</p></td>
<td><p>Questo attributo è un elenco multivalore dei nomi di dominio di tutti i server Enterprise Edition associati a un pool.</p>
<p>Collegamento a ritroso: <strong>Link ID 11023</strong></p>
<p>Il collegamento in avanti corrispondente a questo collegamento a ritroso è <strong>msRTCSIP-PoolAddress</strong>.</p></td>
<td><p>Nuovo in Live Communications Server 2005.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-Gateways (obsoleto)</p></td>
<td><p>Questo attributo di stringa multivalore contiene un elenco di gateway e porte (per gateway).</p></td>
<td><p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-GlobalSettingsData (obsoleto)</p></td>
<td><p>Questo attributo archivia le coppie nome:valore. La coppia nome:valore già definita viene utilizzata per abilitare il polling sulla presenza.</p></td>
<td><p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-GroupingID</p></td>
<td><p>Questo attributo è un identificatore univoco di un gruppo utilizzato per raggruppare le voci della Rubrica.</p></td>
<td><p>Nuovo in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-HomeServer (obsoleto)</p></td>
<td><p>-</p></td>
<td><p>Nuovo in Live Communications Server 2003 (non utilizzato).</p>
<p>Obsoleto in Live Communications Server 2005.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-HomeServerString (obsoleto)</p></td>
<td><p>-</p></td>
<td><p>Nuovo in Live Communications Server 2003.</p>
<p>Obsoleto in Live Communications Server 2005.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-HomeUsers (obsoleto)</p></td>
<td><p>-</p></td>
<td><p>Nuovo in Live Communications Server 2003 (non utilizzato).</p>
<p>Obsoleto in Live Communications Server 2005.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-InternetAccessEnabled</p></td>
<td><p>Questo attributo determina se un singolo utente è abilitato per l'accesso utente esterno. Viene applicato dal livello Enterprise Services. L'attributo è contrassegnato per la replica nel catalogo globale.</p>
<p>I valori validi sono <strong>TRUE</strong> o <strong>FALSE</strong>.</p></td>
<td><p>Nuovo in Live Communications Server 2005.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-IsMaster (obsoleto)</p></td>
<td><p>-</p></td>
<td><p>Nuovo in Live Communications Server 2003</p>
<p>Obsoleto in Live Communications Server 2005.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-Line</p></td>
<td><p>Questo attributo a valore singolo contiene l'ID dispositivo, ovvero l'URI SIP o l'URI TEL del telefono controllato dall'utente, utilizzato in Lync per la telefonia. L'attributo è contrassegnato per la replica nel catalogo globale ed è indicizzato. Se un utente è abilitato per VoIP aziendale, questo attributo archivia la versione normalizzata in formato E.164 del numero di telefono dell'utente.</p></td>
<td><p>Nuovo in Microsoft Office Live Communications Server 2005 con SP1</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-LineServer</p></td>
<td><p>Questo attributo a valore singolo contiene l'URI SIP del server gateway CSTA-SIP. L'attributo è contrassegnato per la replica nel catalogo globale ma non è indicizzato.</p></td>
<td><p>Nuovo in Microsoft Office Live Communications Server 2005 con SP1</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-LocalNormalizationData (obsoleto)</p></td>
<td><p>Questo attributo è riservato per un utilizzo futuro.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-LocalNormalizationLinks (obsoleto)</p></td>
<td><p>Questo attributo multivalore contiene un elenco dei nomi distinti (DN) di normalizzazione locali associati a questo profilo località. Il tipo di questo attributo corrisponde al valore binario del nome distinto. È presente una relazione uno a molti tra il profilo località e le regole di normalizzazione locali. È necessario mantenere l'ordinamento dell'elenco dei nomi distinti di normalizzazione locali specificato dall'amministratore. Il mantenimento dell'ordine viene garantito dalla parte binaria del valore binario del nome distinto, che specifica l'indice per l'ordinamento.</p>
<p>Collegamento in avanti: <strong>Link ID 11034</strong></p>
<p>Il collegamento a ritroso corrispondente a questo attributo di collegamento in avanti è <strong>msRTCSIP-LocationProfileBL</strong>.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-LocalNormalizationOptions</p></td>
<td><p>Questo attributo contiene un elenco di opzioni per la regola di normalizzazione.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-LocationName (obsoleto)</p></td>
<td><p>Questo attributo a valore singolo contiene un nome descrittivo del profilo località che indica la località rappresentata dal profilo. Poiché possono essere disponibili più profili località, l'amministratore deve poter distinguere tra profili diversi.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-locationProfileBL (obsoleto)</p></td>
<td><p>Questo attributo multivalore contiene un elenco dei nomi distinti dei profili località. Specifica il collegamento a ritroso a uno o più profili località.</p>
<p>Collegamento a ritroso: <strong>Link ID 11035</strong></p>
<p>L'attributo corrisponde al collegamento in avanti <strong>msRTCSIP-LocalNormalizationLinks</strong>.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-LocationProfileData (obsoleto)</p></td>
<td><p>Questo attributo è riservato per un utilizzo futuro.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-LocationProfileOptions</p></td>
<td><p>Questo attributo contiene le opzioni per il profilo località.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MappingContact</p></td>
<td><p>Questo attributo multivalore contiene un elenco di contatti applicazione.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MappingLocation</p></td>
<td><p>Questo attributo multivalore contiene un elenco di profili località.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MaxNumOutstandingSearchPerServer (obsoleto)</p></td>
<td><p>Questo attributo rappresenta il numero massimo di richieste di ricerca in attesa per server.</p></td>
<td><p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MaxNumSubscriptionsPerUser (obsoleto)</p></td>
<td><p>Questo attributo rappresenta il numero massimo di sottoscrizioni per utente.</p></td>
<td><p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MaxPresenceSubscriptionTimeout (obsoleto)</p></td>
<td><p>Questo attributo rappresenta la finestra di timeout massima per la sottoscrizione.</p></td>
<td><p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MaxRegistrationsTimeout (obsoleto)</p></td>
<td><p>Questo attributo rappresenta la finestra di timeout massima per le registrazioni.</p></td>
<td><p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MaxRoamingDataSubscriptionTimeout (obsoleto)</p></td>
<td><p>Questo attributo rappresenta la finestra di timeout massima per le sottoscrizioni dei dati di roaming.</p></td>
<td><p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MCUData</p></td>
<td><p>Questo attributo è riservato per un utilizzo futuro.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MCUFactoryAddress</p></td>
<td><p>Questo attributo è un attributo del punto di controllo del servizio della classe computer che specifica un collegamento a ritroso alla factory MCU (Multipoint Control Unit) a cui appartiene. Il punto di controllo del servizio e l'attributo vengono creati per ogni MCU Microsoft. Ogni MCU Microsoft deve individuare il server back-end del pool a cui appartiene per poter recuperare da esso le impostazioni a livello di pool.</p>
<p>Il valore di questo attributo corrisponde al nome distinto (DN) della factory MCU. Si tratta di un attributo a valore singolo contrassegnato per la replica nel catalogo globale.</p>
<p>Collegamento in avanti: <strong>Link ID 11026</strong></p>
<p>Il collegamento a ritroso corrispondente a questo attributo di collegamento in avanti è <strong>msRTCSIP-MCUServers</strong>.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MCUFactoryData</p></td>
<td><p>Attributo multistringa riservato. Le impostazioni archiviate in questo attributo sono rappresentate come coppie nome=valore. Le coppie nome=valore attualmente definite sono:</p>
<ul>
<li><p>FactoryURL = &lt;URL&gt;</p></li>
</ul></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MCUFactoryPath</p></td>
<td><p>Attributo a valore singolo che contiene il nome distinto (DN) di una singola factory MCU associata a un pool.</p>
<p>Collegamento in avanti: <strong>Link ID 11024</strong></p>
<p>Il collegamento a ritroso corrispondente a questo attributo di collegamento in avanti è <strong>msRTCSIP-PoolAddresses</strong>.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MCUFactoryProviderID</p></td>
<td><p>Questo attributo corrisponde a una stringa a valore singolo che specifica il GUID del provider della factory MCU. In base al valore del GUID, il processo della factory MCU determina se elaborare le richieste di questo tipo di MCU. Se il valore GUID è <strong>{F0810510-424F-46ef-84FE-6CC720DF1791}</strong>, verrà elaborato dal processo della factory MCU (disponibile in Lync Server per impostazione predefinita). Con tutti gli altri valori di GUID, il processo della factory MCU non elaborerà le richieste del tipo di MCU.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MCUServers</p></td>
<td><p>Questo attributo corrisponde a un elenco multivalore di nomi distinti (DN). Contiene un elenco di tutti i server MCU dello stesso tipo e fornitore associati a questa factory MCU. È possibile utilizzare 63 caratteri per ciascun segmento e 255 caratteri per l'intero nome di dominio completo.</p>
<p>Collegamento a ritroso: Link ID 11027</p>
<p>Il collegamento in avanti corrispondente a questo collegamento a ritroso è <strong>msRTCSIP-MCUFactoryAddress</strong>.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MCUType</p></td>
<td><p>Questo attributo corrisponde a una stringa a valore singolo che specifica il supporto che la MCU è in grado di gestire.</p>
<p>I tipi validi supportati sono:</p>
<ul>
<li><p>meeting</p></li>
<li><p>audio-video</p></li>
<li><p>chat</p></li>
<li><p>phone-conf</p></li>
</ul></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MCUVendor</p></td>
<td><p>Questo attributo corrisponde a una stringa a valore singolo che specifica il nome di un fornitore di MCU. L'attributo specificato per tutte le MCU Microsoft sarà <strong>Microsoft Corporation</strong>.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MeetingFlags (obsoleto)</p></td>
<td><p>Questo attributo definisce le diverse opzioni relative alle riunioni abilitate a livello globale per tutti gli oggetti utente o contatto. Corrisponde a un valore di maschera di bit di tipo integer.</p>
<p>I valori validi e le posizioni di bit associate sono:</p>
<ul>
<li><p>0: AllowOrganizeMeetingWithAnonymousParticipants è None (non consente agli utenti di invitare utenti anonimi alle riunioni) (nessun bit impostato)</p></li>
<li><p>4: AllowOrganizeMeetingWithAnonymousParticipants è Everyone (consente a tutti gli utenti di invitare utenti anonimi alle riunioni) (posizione bit 2)</p></li>
<li><p>8: AllowOrganizeMeetingWithAnonymousParticipants è UsePerUserSetting (consente agli utenti di invitare utenti anonimi alle riunioni sulla base dell'impostazione per ciascun utente) (posizione bit 3)</p></li>
<li><p>16: UserPerUserMeetingPolicy (criteri riunione definiti per utente) (posizione bit 4)</p></li>
</ul></td>
<td><p>Nuovo in Office Communications Server 2007.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MeetingPolicy (obsoleto)</p></td>
<td><p>Questo attributo specifica il nome distinto (DN) del criterio che l'amministratore ha assegnato per l'utente come attributo a valore singolo.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MinPresenceSubscriptionTimeout (obsoleto)</p></td>
<td><p>Questo attributo rappresenta la finestra di timeout minima per la sottoscrizione relativa alla presenza.</p></td>
<td><p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MinRegistrationTimeout (obsoleto)</p></td>
<td><p>Questo attributo rappresenta l'intervallo di tempo di timeout minimo per la registrazione.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MinRoamingDataSubscriptionTimeout (obsoleto)</p></td>
<td><p>Questo attributo rappresenta la finestra di timeout minima per la sottoscrizione dei dati di roaming.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MirrorBackEndServer</p></td>
<td><p>Questo attributo viene utilizzato per archiviare il back-end SQL Server con mirroring utilizzato dal pool Front End.</p></td>
<td><p>Nuovo in Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-MobilityFlags</p></td>
<td><p>Questo attributo contiene le opzioni e i flag che definiscono le impostazioni di mobilità.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-MobilityPolicy</p></td>
<td><p>Questo attributo contiene il nome distinto per un oggetto criterio di mobilità.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-NumDevicesPerUser (obsoleto)</p></td>
<td><p>Questo attributo rappresenta il numero consentito di dispositivi in cui un utente può effettuare la registrazione di comunicazioni SIP e la sottoscrizione della presenza.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-OptionFlags</p></td>
<td><p>Questo attributo specifica le opzioni abilitate per l'oggetto utente o contatto. Corrisponde a un valore di maschera di bit di tipo integer. Ogni opzione è rappresentata da un bit. L'attributo è contrassegnato per la replica nel catalogo globale.</p>
<p>I valori validi e le posizioni di bit associate sono:</p>
<ul>
<li><p>1: abilitato per la connettività per messaggistica istantanea pubblica (posizione bit 0)</p></li>
<li><p>2: riservato (posizione bit 1)</p></li>
<li><p>4: riservato (posizione bit 2)</p></li>
<li><p>8: riservato (posizione bit 3)</p></li>
<li><p>16: abilitato per il controllo delle chiamate remote [Telefonia] (posizione bit 4)</p></li>
<li><p>64: AllowOrganizeMeetingWithAnonymousParticipants (consente agli utenti di invitare utenti anonimi alle riunioni) (posizione bit 6)</p></li>
<li><p>128: UCEnabled (abilita gli utenti alle comunicazioni unificate) (posizione bit 7)</p></li>
<li><p>256: EnabledForEnhancedPresence (abilita l'utente per la connettività per messaggistica istantanea pubblica) (posizione bit 8)</p></li>
<li><p>512: RemoteCallControlDualMode (modalità doppia di controllo delle chiamate remote) (posizione bit 9)</p></li>
</ul></td>
<td><p>Nuovo in Live Communications Server 2005 con SP1.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-OriginatorSID</p></td>
<td><p>Questo attributo viene utilizzato in topologie a foresta risorsa e topologie a foresta centralizzata per abilitare Single Sign-On quando l'ObjectSID di un utente dell'account principale di Windows NT viene copiato in questo attributo dell'oggetto utente o contatto corrispondente nella foresta risorsa o centralizzata. Communicator Web Access esegue la ricerca di un utente in Servizi di dominio Active Directory utilizzando questo attributo o l'ObjectSID dell'utente. L'attributo è contrassegnato per la replica nel catalogo globale.</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-OwnerUrn</p></td>
<td><p>Questo attributo corrisponde all'URN (Uniform Resource Name) del proprietario per il contatto applicazione.</p></td>
<td><p>Nuovo in Lync Server 2010.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-Pattern (obsoleto)</p></td>
<td><p>Questo attributo di stringa a valore singolo contiene un criterio utilizzato per la corrispondenza dei numeri composti in formato E.164. Se il numero composto corrisponde a questo criterio, la conversione viene applicata al numero composto.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-PhoneRouteBL (obsoleto)</p></td>
<td><p>Questo attributo multivalore contiene un elenco dei nomi distinti (DN) delle route telefoniche. Specifica il collegamento a ritroso a una o più route telefoniche.</p>
<p>Collegamento a ritroso: <strong>Link ID 11033</strong></p>
<p>Corrisponde al collegamento in avanti <strong>msRTCSIP-RouteUsageLinks</strong>.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-PhoneRouteData (obsoleto)</p></td>
<td><p>Questo attributo è riservato per un utilizzo futuro.</p></td>
<td><p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-PhoneRouteName (obsoleto)</p></td>
<td><p>Questo attributo di stringa UNICODE a valore singolo specifica il nome descrittivo della route telefonica in modo che l'amministratore possa farvi riferimento più facilmente.</p></td>
<td><p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-PhoneUsageData (obsoleto)</p></td>
<td><p>Questo attributo è riservato per un utilizzo futuro.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-PolicyContent (obsoleto)</p></td>
<td><p>Questo attributo corrisponde a una stringa Unicode a valore singolo. L'attributo di stringa contiene la definizione del criterio in formato XML. La definizione dello schema XML è comune in diversi tipi di criteri. Per ciascun tipo di criterio cambiano solo le impostazioni.</p>
<p>Di seguito viene indicata la definizione dello schema XML (XSD):</p>
<pre><code>&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;
&lt;xs:schema id=&quot;instance&quot;  xmlns:xs=&quot;http://www.w3.org/2001/XMLSchema&quot; xmlns:msdata=&quot;urn:schemas-microsoft-com:xml-msdata&quot;&gt;
  &lt;xs:element name=&quot;instance&quot; msdata:IsDataSet=&quot;true&quot;&gt;
    &lt;xs:complexType&gt;
      &lt;xs:choice maxOccurs=&quot;unbounded&quot;&gt;
        &lt;xs:element name=&quot;property&quot; nillable=&quot;true&quot;&gt;
          &lt;xs:complexType&gt;
            &lt;xs:simpleContent msdata:ColumnName=&quot;property_Text&quot; msdata:Ordinal=&quot;1&quot;&gt;
              &lt;xs:extension base=&quot;xs:string&quot;&gt;
                &lt;xs:attribute name=&quot;name&quot; type=&quot;xs:string&quot; /&gt;
              &lt;/xs:extension&gt;
            &lt;/xs:simpleContent&gt;
          &lt;/xs:complexType&gt;
        &lt;/xs:element&gt;
      &lt;/xs:choice&gt;
    &lt;/xs:complexType&gt;
  &lt;/xs:element&gt;
&lt;/xs:schema&gt;</code></pre></td>
<td><p>Nuovo in Office Communications Server 2007.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-PolicyData (obsoleto)</p></td>
<td><p>Questo attributo è riservato per un utilizzo futuro.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-PolicyType (obsoleto)</p></td>
<td><p>Questo attributo di stringa Unicode a valore singolo contiene il tipo di criterio. I tipi di criteri validi sono:</p>
<ul>
<li><p>meeting</p></li>
<li><p>telephony</p></li>
</ul></td>
<td><p>Nuovo in Office Communications Server 2007.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-PoolAddress</p></td>
<td><p>Questo attributo specifica un collegamento al pool cui appartiene un computer. Viene impostato indipendentemente dalla versione di Lync Server in esecuzione nel computer (Standard Edition o Enterprise Edition). L'attributo è contrassegnato per la replica nel catalogo globale.</p>
<p>Il valore valido corrisponde al nome di dominio del pool.</p>
<p>Collegamento in avanti: <strong>Link ID 11022</strong></p>
<p>Il collegamento a ritroso corrispondente a questo attributo di collegamento in avanti è <strong>msRTCSIP-FrontEndServers</strong>.</p></td>
<td><p>Nuovo in Live Communications Server 2005.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-PoolAddresses</p></td>
<td><p>Attributo multivalore che contiene un elenco dei nomi distinti (DN) dei pool cui è associata la factory MCU.</p>
<p>Collegamento a ritroso: <strong>Link ID 11025</strong></p>
<p>Il collegamento in avanti corrispondente a questo collegamento a ritroso è <strong>msRTCSIP-MCUFactoryPath</strong>.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-PoolData</p></td>
<td><p>Questo attributo è riservato per un utilizzo futuro.</p></td>
<td><p>Nuovo in Live Communications Server 2005 con SP1.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-PoolDisplayName</p></td>
<td><p>Questo attributo specifica un nome arbitrario per un pool visualizzato nella console di gestione. Questo nome può essere modificato dall'amministratore.</p>
<p>Il valore valido è una stringa che rappresenta il nome di un pool.</p></td>
<td><p>Nuovo in Live Communications Server 2005.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-PoolDomainFQDN</p></td>
<td><p>Questo attributo corrisponde a una stringa a valore singolo. Il valore di questo attributo, se presente, rappresenta il nome di dominio completo del pool, se l'amministratore desidera creare un pool Front End con un nome di dominio completo non conforme alla struttura del dominio di Active Directory in cui tale pool viene creato, ad esempio uno spazio dei nomi SIP distinto dallo spazio dei nomi DNS (Domain Name System).</p>
<p>È consigliabile eseguire il mapping dell'FQDN di dominio del pool Front End alla parte del nome del dominio di Active Directory in cui risiede il pool. Quando, pertanto, tale attributo non include alcun valore, il nome di dominio completo del pool Front End corrisponderà, per impostazione predefinita, alla struttura del nome del dominio Active Directory, come indicato dall'attributo <strong>dnsHostName</strong>.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-PoolFunctionality</p></td>
<td><p>Elenco multivalore dei nomi di dominio di tutti i server Lync Server, Enterprise Edition associati a un pool. Questo attributo di tipo integer definisce se il pool supporta messaggistica istantanea, presenza e riunioni.</p>
<p>I tipi di valori validi possibili sono:</p>
<ul>
<li><p>Indefinito: servizio di messaggistica istantanea e presenza (Live Communications Server 2005 e 2003)</p></li>
<li><p>1: servizio di messaggistica istantanea e presenza (Lync Server)</p></li>
<li><p>2: servizio di messaggistica istantanea e presenza, servizio riunioni (Lync Server)</p></li>
</ul></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-PoolType</p></td>
<td><p>Questo attributo specifica se un pool di server esegue un server Standard Edition o un server Enterprise Edition. Corrisponde a un valore di maschera di bit di tipo integer. Ogni opzione è rappresentata da un bit.</p>
<p>I valori validi e le posizioni di bit associate sono:</p>
<ul>
<li><p>1: Server Standard Edition, utenti host (posizione bit 0)</p></li>
<li><p>2: Server Enterprise Edition, utenti host (posizione bit 1)</p></li>
<li><p>4: Server Standard Edition, applicazioni host (posizione bit 2)</p></li>
<li><p>8: Server Enterprise Edition, applicazioni host (posizione bit 3)</p></li>
</ul>
<p>Poiché Lync Server non supporta i pool che ospitano solo applicazioni, gli unici valori validi sono:</p>
<ul>
<li><p>5: Server Standard Edition, applicazioni e utenti host (posizioni bit 0 e 2)</p></li>
<li><p>10: Server Enterprise Edition, applicazioni e utenti host (posizioni bit 1 e 3)</p></li>
</ul></td>
<td><p>Nuovo in Live Communications Server 2005.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-PoolVersion</p></td>
<td><p>Questo attributo definisce la versione del pool. È un tipo di numero integer che viene incrementato a ogni versione principale del prodotto.</p>
<p>I tipi di valori validi possibili sono:</p>
<ul>
<li><p>0: Live Communications Server 2003</p></li>
<li><p>1: Live Communications Server 2005</p></li>
<li><p>2: Live Communications Server 2005 con SP1</p></li>
<li><p>3: Office Communications Server 2007</p></li>
<li><p>4: Office Communications Server 2007 R2</p></li>
<li><p>5: Lync Server 2010</p></li>
</ul></td>
<td><p>Live Communications Server 2005 con SP1.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-PresenceFlags</p></td>
<td><p>Questo attributo contiene le opzioni e i flag che definiscono le impostazioni della presenza.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-PresencePolicy</p></td>
<td><p>Questo attributo contiene il nome distinto per un oggetto criterio di presenza.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-PrimaryHomeServer</p></td>
<td><p>Questo attributo abilita la messaggistica SIP per un utente o un contatto. È stato aggiunto alla classe Contact in quanto in una topologia a foresta centralizzata sono abilitati per SIP gli oggetti contatto ma non gli oggetti utente.</p>
<p>Il valore valido corrisponde al nome distinto del server Standard Edition o del pool Enterprise Edition Front End cui è assegnato un utente.</p></td>
<td><p>Nuovo in Live Communications Server 2005.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-PrimaryUserAddress</p></td>
<td><p>Questo attributo contiene l'indirizzo SIP di un utente specificato.</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-PrivateLine</p></td>
<td><p>Questo attributo contiene l'ID del dispositivo della linea privata.</p></td>
<td><p>Nuovo in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-Routable</p></td>
<td><p>Questo attributo booleano viene utilizzato per determinare se Lync Server è autorizzato a eseguire il routing a questo servizio utilizzando l'indirizzo GRUU. Se questo valore è impostato su <strong>TRUE</strong>, Lync Server è autorizzato a eseguire il routing a questo servizio. Se il valore è impostato su <strong>FALSE</strong>, Lync Server non è autorizzato a eseguire il routing a questo servizio.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-RouteUsageAttribute (obsoleto)</p></td>
<td><p>Questo attributo di stringa UNICODE a valore singolo definisce un attributo che qualifica l'utilizzo per una route telefonica. La selezione di una route telefonica dipende da due elementi: l'attributo di utilizzo assegnato alla route telefonica e gli attributi di utilizzo dei criteri consentiti del chiamante. Viene selezionata la prima route telefonica con un attributo di utilizzo corrispondente all'utilizzo consentito del chiamante.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-RouteUsageLinks (obsoleto)</p></td>
<td><p>Questo attributo multivalore di nome distinto (DN) contiene un elenco dei nomi distinti degli utilizzi di route.</p>
<p>Collegamento in avanti: <strong>Link ID 11032</strong></p>
<p>Questo attributo è un collegamento in avanti corrispondente al collegamento a ritroso <strong>msRTCSIP-PhoneRouteBL</strong>.</p></td>
<td><p>Obsoleto in Lync Server 2010.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-RoutingPoolDN</p></td>
<td><p>Questo attributo contiene il nome distinto che punta al pool attraverso cui deve passare tutto il traffico SIP indirizzato alla MCU o al servizio trusted.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-RuleName (obsoleto)</p></td>
<td><p>Questo attributo di stringa UNICODE a valore singolo specifica il nome descrittivo della regola di normalizzazione in modo che un amministratore possa farvi riferimento più facilmente.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-SchemaVersion</p></td>
<td><p>Questo attributo rappresenta la versione dello schema attualmente distribuita nell'organizzazione.</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-SearchMaxRequests (obsoleto)</p></td>
<td><p>Questo attributo limita il numero di risultati restituiti da una ricerca di directory quando un utente cerca un contatto utilizzando Communicator. Questo attributo sostituisce il valore fornito dal client.</p></td>
<td><p>Obsoleto in Lync Server 2010.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-SearchMaxResults (obsoleto)</p></td>
<td><p>Questo attributo limita il numero di richieste di ricerca restituite.</p></td>
<td><p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ServerBL</p></td>
<td><p>Questo attributo multivalore corrisponde a un collegamento a ritroso che contiene un elenco di nomi distinti (DN). Tali nomi distinti puntano a un oggetto pool o <strong>TrustedService</strong>.</p>
<p>Corrisponde al collegamento successivo <strong>msRTCSIP-TrustedServiceLinks</strong>.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ServerData</p></td>
<td><p>Questo attributo è riservato per un utilizzo futuro.</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-ServerReferenceBL (obsoleto)</p></td>
<td><p>Questo attributo multivalore contiene un elenco di nomi distinti. Tali nomi distinti sono collegamenti a ritroso che fanno riferimento ad altri oggetti server a cui è possibile assegnare un profilo località predefinito.</p>
<p>Collegamento a ritroso: <strong>Link ID 11037</strong></p>
<p>Il collegamento in avanti corrispondente a questo collegamento a ritroso è <strong>msRTCSIP-DefaultLocationProfileLink</strong>.</p>
<p>Questo collegamento a ritroso fa riferimento solo a pool e Mediation Server.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-ServerVersion</p></td>
<td><p>Questo attributo definisce le informazioni sulla versione del server. Il numero di versione si applica a tutti i ruoli del server. È un valore integer che viene incrementato regolarmente a ogni versione ufficiale del prodotto.</p>
<p>I valori validi possibili sono:</p>
<ul>
<li><p>Indefinito: Live Communications Server 2003</p>
<p>                 Live Communications Server 2005</p>
<p>                 Live Communications Server 2005 con SP1</p></li>
<li><p>3: Office Communications Server 2007</p></li>
<li><p>4: Office Communications Server 2007 R2</p></li>
<li><p>5: Lync Server 2010</p></li>
<li><p>6: Lync Server 2013</p></li>
</ul></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-SourceObjectType</p></td>
<td><p>Questo attributo a valore singolo di tipo integer specifica il tipo di oggetto cui punta <strong>msDS-SourceObjectDN</strong>, come specificato di seguito:</p>
<ul>
<li><p>null | 0x00000001: rappresenta un oggetto utente principale di Windows NT Server appartenente a una foresta diversa</p></li>
<li><p>I seguenti attributi rappresentano un tipo di gruppo appartenente a una foresta diversa per l'espansione del gruppo di distribuzione:</p>
<ul>
<li><p>0x00000002: ADS_GROUP_TYPE_GLOBAL_GROUP</p></li>
<li><p>0x00000004: ADS_GROUP_TYPE_DOMAIN_LOCAL_GROUP</p></li>
<li><p>0x00000004: ADS_GROUP_TYPE_LOCAL_GROUP</p></li>
<li><p>0x00000008: ADS_GROUP_TYPE_UNIVERSAL_GROUP</p></li>
<li><p>0x80000000: ADS_GROUP_TYPE_SECURITY_ENABLED</p></li>
<li><p>0x90000000: rappresenta un oggetto accesso sottoscrittore o operatore automatico appartenente alla stessa foresta o a una foresta diversa</p></li>
</ul></li>
</ul></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-SubscriptionAuthRequired (obsoleto)</p></td>
<td><p>-</p></td>
<td><p>Nuovo in Live Communications Server 2003.</p>
<p>Obsoleto in Live Communications Server 2005.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-TargetHomeServer</p></td>
<td><p>Questo attributo consente di spostare un oggetto contatto o utente da un pool di Lync Server a un altro. È stato aggiunto alla classe Contact, in quanto in una topologia a foresta centralizzata sono abilitati per SIP gli oggetti contatto e non gli oggetti utente.</p>
<p>Il valore valido corrisponde al nome distinto del server Standard Edition o del pool Front End di destinazione in cui verrà spostato l'utente.</p></td>
<td><p>Nuovo in Live Communications Server 2005.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TargetPhoneNumber (obsoleto)</p></td>
<td><p>Questo attributo di stringa a valore singolo contiene un formato o un intervallo di numeri di telefono per il routing ai gateway specificati definiti in <strong>msRTCSIP-Gateways</strong>.</p></td>
<td><p>Obsoleto in Lync Server 2010.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-TargetUserPolicies</p></td>
<td><p>Questo attributo archivia le coppie nome-valore dei criteri di destinazione per gli utenti di Lync Server.</p></td>
<td><p>Nuovo in Lync Server 2010.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TenantId</p></td>
<td><p>Questo attributo archivia l'identificatore univoco per un tenant.</p></td>
<td><p>Nuovo in Lync Server 2010.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-Translation (obsoleto)</p></td>
<td><p>Questo attributo viene utilizzato dalla funzionalità vocale di Lync Server e contiene la stringa di conversione da applicare al numero composto se viene trovata una corrispondenza.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TrustedMCUData</p></td>
<td><p>Questo attributo è riservato per un utilizzo futuro.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-TrustedMCUFQDN</p></td>
<td><p>Questo attributo corrisponde a un valore stringa che contiene il nome di dominio completo della MCU. Si tratta di un attributo a valore singolo. È possibile utilizzare 63 caratteri per ciascun segmento e 255 caratteri per l'intero nome di dominio completo.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TrustedProxyData</p></td>
<td><p>Questo attributo è riservato per un utilizzo futuro.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-TrustedProxyFQDN</p></td>
<td><p>Questo attributo corrisponde a un valore stringa che contiene il nome di dominio completo del server che esegue il server proxy. Si tratta di un attributo a valore singolo. È possibile utilizzare 63 caratteri per ciascun segmento e 255 caratteri per l'intero nome di dominio completo.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TrustedServerData</p></td>
<td><p>Questo attributo è riservato per un utilizzo futuro.</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-TrustedServerFQDN</p></td>
<td><p>Questo attributo a valore singolo rappresenta il nome di dominio completo di un server trusted.</p></td>
<td><p>Nuovo in Live Communications Server 2005.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TrustedServerVersion</p></td>
<td><p>Questo attributo specifica il numero di versione di un server incluso nell'elenco di server trusted.</p>
<p>I valori validi possibili sono:</p>
<ul>
<li><p>NULL: Live Communications Server 2003</p></li>
<li><p>2: Live Communications Server 2005</p></li>
<li><p>3: Office Communications Server 2007</p></li>
<li><p>4: Office Communications Server 2007 R2</p></li>
<li><p>5: Lync Server 2010</p></li>
<li><p>6: Lync Server 2013</p></li>
</ul></td>
<td><p>Nuovo in Live Communications Server 2005.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-TrustedServiceFlags</p></td>
<td><p>Questo attributo definisce le opzioni abilitate per il servizio trusted.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TrustedServiceLinks</p></td>
<td><p>Questo attributo multivalore contiene un elenco di nomi distinti (DN) che fanno riferimento a un oggetto servizio trusted, ad esempio MRAS (Media Relay Authentication Service). Per poter supportare scenari audio per utenti remoti, un oggetto MRAS, fisicamente inserito nell'server perimetrale che esegue il servizio A/V Conferencing, deve essere associato a un pool.</p>
<p>Il collegamento a ritroso corrispondente a questo attributo di collegamento successivo è <strong>msRTCSIP-ServerBL</strong>.</p></td>
<td><p>UC</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-TrustedServicePort</p></td>
<td><p>Questo attributo è un valore integer che definisce il numero di porta utilizzato per la connessione al servizio GRUU.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TrustedServiceType</p></td>
<td><p>Questo attributo corrisponde a un valore stringa che definisce il tipo di servizio GRUU rappresentato.</p>
<p>I tipi di servizio GRUU validi sono:</p>
<ul>
<li><p>MediationServer</p></li>
<li><p>Gateway</p></li>
<li><p>MRAS (Media Relay Authentication Service)</p></li>
<li><p>QoSM</p></li>
<li><p>msRTCSIP-UserExtension CWA</p></li>
</ul></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-TrustedWebComponentsServerData</p></td>
<td><p>Questo attributo è riservato per un utilizzo futuro.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-TrustedWebComponentsServerFQDN</p></td>
<td><p>Questo attributo corrisponde a un valore stringa che contiene il nome di dominio completo del server IIS che esegue i servizi Web di Lync Server. Si tratta di un attributo a valore singolo. È possibile utilizzare 63 caratteri per ciascun segmento e 255 caratteri per l'intero nome di dominio completo.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-UCFlags (obsoleto)</p></td>
<td><p>Questo attributo definisce le diverse opzioni relative alle comunicazioni unificate abilitate a livello globale per tutti gli oggetti utente o contatto. Corrisponde a un valore di maschera di bit di tipo integer. Ogni opzione è rappresentata dalla presenza di un bit.</p>
<p>Il valore valido e la posizione di bit associata è:</p>
<ul>
<li><p>4: UsePerUserUCPolicy (posizione bit 2)</p></li>
</ul>
<p>Quando questo bit è impostato, il criterio di comunicazione unificata viene definito per singolo utente.</p></td>
<td><p>Obsoleto in Lync Server 2010.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-UCPolicy (obsoleto)</p></td>
<td><p>Questo attributo a valore singolo contiene il nome distinto (DN) del criterio di comunicazione unificata che l'amministratore ha assegnato per l'utente.</p></td>
<td><p>Obsoleto in Lync Server 2010.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-UserDomainList (obsoleto)</p></td>
<td><p>Questo attributo fornisce l'elenco di tutti i domini in una foresta che ospitano utenti abilitati per SIP. Per impostazione predefinita, questo elenco è vuoto a indicare che tutti i domini nella foresta sono abilitati per SIP.</p>
<p>I valori validi sono più stringhe che rappresentano i nomi di dominio dei singoli domini.</p></td>
<td><p>Nuovo in Live Communications Server 2005.</p>
<p>Obsoleto in Lync Server 2010.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-UserEnabled</p></td>
<td><p>Questo attributo determina se l'utente è attualmente abilitato per Lync Server.</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-UserExtension</p></td>
<td><p>Questo attributo multivalore contiene un elenco di coppie nome-valore in formato &quot;nome=valore&quot;. L'attributo è contrassegnato per la replica nel catalogo globale.</p></td>
<td><p>Nuovo in Live Communications Server 2005 con SP1.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-UserLocationProfile</p></td>
<td><p>Questo attributo contiene il nome distinto che punta a un oggetto profilo località.</p></td>
<td><p>Nuovo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-UserPolicies</p></td>
<td><p>Questo attributo archivia le coppie nome valore per i criteri utente.</p></td>
<td><p>Nuovo in Lync Server 2010.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-UserPolicy</p></td>
<td><p>Questo attributo multivalore contiene un elenco di nomi distinti con valori binari (DN_WITH_BINARY) che puntano a criteri utente globali di tipi diversi. La parte binaria indica il tipo di criterio a cui punta la parte del nome distinto.</p>
<p>I valori binari validi sono:</p>
<ul>
<li><p>0x00000001: criterio per riunioni</p></li>
<li><p>0x00000002: criterio per comunicazioni unificate</p></li>
<li><p>0x00000005: criterio di presenza</p></li>
</ul></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-UserRoutingGroupId</p></td>
<td><p>Questo è l'ID del gruppo di routing SIP. Gli utenti dello stesso gruppo eseguiranno la registrazione nello stesso Front End Server.</p></td>
<td><p>Nuovo in Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-WebComponentsData</p></td>
<td><p>Attributo a valore singolo. Questo attributo è riservato per un utilizzo futuro.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-WebComponentsPoolAddress</p></td>
<td><p>Questo attributo a valore singolo punta al pool o al server Standard Edition cui appartengono i componenti Web.</p>
<p>Collegamento in avanti: <strong>Link ID 11028</strong></p>
<p>Il collegamento a ritroso corrispondente a questo attributo di collegamento in avanti è <strong>msRTCSIP-WebComponentsServers</strong>.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="odd">
<td><p>msRTCSIP-WebComponentsServers</p></td>
<td><p>Questo attributo corrisponde a un elenco multivalore di nomi distinti. Questo attributo contiene un elenco di tutti i server Web associati al pool.</p>
<p>Collegamento a ritroso: <strong>Link ID 11029</strong></p>
<p>Il collegamento in avanti corrispondente a questo collegamento a ritroso è <strong>msRTCSIP-WebComponentsPoolAddress</strong>.</p></td>
<td><p>Nuovo in Office Communications Server 2007.</p></td>
</tr>
<tr class="even">
<td><p>msRTCSIP-WMIInstanceId (obsoleto)</p></td>
<td><p>-</p></td>
<td><p>Nuovo in Live Communications Server 2003.</p>
<p>Obsoleto in Live Communications Server 2005.</p></td>
</tr>
<tr class="odd">
<td><p>OtherIPPhone</p></td>
<td><p>Questo attributo esistente di Active Directory viene utilizzato dalla telefonia per specificare l'elenco di indirizzi TCP/IP alternativi per un telefono.</p></td>
<td><p>Nuovo nel sistema operativo Windows Server 2008.</p></td>
</tr>
<tr class="even">
<td><p>PhoneOfficeOther</p></td>
<td><p>Questo attributo esistente di Active Directory viene utilizzato dai componenti della funzionalità vocale di Lync Server solo per oggetti contatto per eseguire il routing di chiamate a numeri di accesso di operatori automatici e sottoscrittori di messaggistica unificata. L'indirizzo utilizzato per l'inoltro di chiamata incondizionato viene archiviato in questo attributo multivalore. Questo account viene creato specificamente per consentire l'accesso a operatori automatici e sottoscrittori. Gli attributi di questo account non devono essere modificati dagli amministratori.</p></td>
<td><p>Nuovo nel sistema operativo Windows 2000.</p></td>
</tr>
<tr class="odd">
<td><p>ProxyAddresses</p></td>
<td><p>Questo attributo multivalore esistente di Active Directory fa parte dello schema di base di Active Directory introdotto in Windows 2000 e contiene i diversi indirizzi X400, X500 e SMTP della posta elettronica dell'utente. In Live Communications Server 2003 e versioni successive a questo elenco viene aggiunto l'URI SIP dell'utente utilizzando il tag &quot;sip:&quot;.</p>
<p>Le applicazioni seguenti eseguono la ricerca dell'URI SIP dell'utente tramite questo attributo:</p>
<ul>
<li><p>Client di messaggistica e collaborazione Microsoft Office Outlook 2003</p></li>
<li><p>Microsoft Office SharePoint Server 2007</p></li>
</ul></td>
<td><p>Nuovo nel sistema operativo Windows 2000.</p></td>
</tr>
<tr class="even">
<td><p>TelephoneNumber</p></td>
<td><p>Questo attributo esistente di Active Directory contiene il numero di telefono dell'utente.</p></td>
<td><p>Nuovo nel sistema operativo Windows 2000.</p></td>
</tr>
</tbody>
</table>

