---
title: Configurazione dei criteri di avvio dei client in Lync Server 2013
TOCTitle: Configurazione dei criteri di avvio dei client in Lync Server 2013
ms:assetid: 45042eca-b845-4207-b12f-b8b7f5d44bdf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425941(v=OCS.15)
ms:contentKeyID: 49300373
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione dei criteri di avvio dei client in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per la gestione dei Criteri di gruppo è possibile utilizzare gli strumenti Console Gestione criteri di gruppo e l'Editor oggetti Criteri di gruppo. Con il modello amministrativo Criteri di gruppo di Office sono inclusi i modelli amministrativi Lync 2013.admx (ADMX) e .adml (ADML), che contengono le impostazioni dei criteri basate sul Registro di sistema configurate per gli oggetti Criteri di gruppo del dominio. I file ADML sono specifici della lingua e sono complementari ai file ADMX. Ogni file ADMX e ADML contiene le impostazioni dei criteri per una singola applicazione Office.

Per Lync 2013 sono disponibili diversi criteri di avvio client che è consigliabile configurare prima che gli utenti accedano al server per la prima volta, come ad esempio la modalità di sicurezza e i server predefiniti che il client deve usare fino a quando non viene effettuato l'accesso. È possibile utilizzare i Criteri di gruppo per stabilire tali impostazioni nei Registri di sistema dei computer degli utenti prima che effettuino l'accesso e inizino a ricevere le impostazioni di provisioning di tipo in-band dal server. Nella tabella seguente sono elencate le impostazioni dei Criteri di gruppo disponibili per Lync 2013.

### Impostazioni dei Criteri di gruppo per Lync 2013

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Impostazione dei Criteri di gruppo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Specifica server<br />
(ConfigurationMode)</p></td>
<td><p>Specifica in che modo Lync 2013 identifica il trasporto e il server da utilizzare durante l'accesso. All'interno di questa impostazione è possibile specificare:</p>
<ul>
<li><p>ServerAddressExternal: specifica il nome del server o l'indirizzo IP utilizzato dai client e dai contatti federati durante la connessione dall'esterno del firewall.</p></li>
<li><p>ServerAddressInternal: specifica il nome del server o l'indirizzo IP utilizzato quando i client si connettono dall'interno del firewall dell'organizzazione.</p></li>
<li><p>Transport: specifica il protocollo TCP (Transmission Control Protocol) o TLS (Transport Layer Security).</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Versioni server aggiuntive supportate<br />
(ConfiguredServerCheckValues)</p></td>
<td><p>Specifica un elenco di nomi di versioni server delimitati da punto e virgola ai quali accederà Lync Server 2013, oltre alle versioni server supportate per impostazione predefinita.</p></td>
</tr>
<tr class="odd">
<td><p>Disabilita caricamento automatico log errori di accesso (DisableAutomaticSendTracing)</p></td>
<td><p>Carica automaticamente i log degli errori di accesso in Lync Server per l'analisi. Se l'accesso riesce, non viene caricato alcun log automaticamente. Se questo criterio non è configurato, si verifica quanto segue.</p>
<dl>
<dt><span></span></dt>
<dd><p>Per gli utenti di Lync Online: i log degli errori di accesso vengono caricati automaticamente.</p>
</dd>
<dt><span></span></dt>
<dd><p>Per gli utenti locali di Lync: prima del caricamento viene visualizzata una finestra di dialogo di conferma all'utente.</p>
</dd>
</dl>
<p>Quando questa impostazione è disabilitata, i log di accesso vengono automaticamente caricati in Lync Server sia per gli utenti locali di Lync che per quelli di Lync Online. Quando questa impostazione è abilitata, i log di accesso non vengono mai caricati automaticamente.</p></td>
</tr>
<tr class="even">
<td><p>Disabilita fallback HTTP per connessione SIP<br />
(DisableHttpConnect)</p></td>
<td><p>Impedisce a Lync Server di tentare di connettersi al server mediante HTTP, se TLS o TCP non è disponibile. Per impostazione predefinita, Lync tenta prima di connettersi al server mediante TLS o TCP e quindi, se nessuno di questi metodi di trasporto riesce, Lync tenta di connettersi mediante HTTP. Utilizzare questo criterio per disabilitare il tentativo di connessione HTTP di fallback.</p></td>
</tr>
<tr class="odd">
<td><p>Richiedi credenziali di accesso<br />
(DisableNTCredentials)</p></td>
<td><p>Richiede all'utente di fornire le credenziali di accesso per Lync anziché eseguire automaticamente questa operazione tramite le credenziali di Windows durante l'accesso a un server SIP.</p></td>
</tr>
<tr class="even">
<td><p>Disabilita controllo versione server<br />
(DisableServerCheck)</p></td>
<td><p>Se impostato su 1, questo criterio impedisce a Lync di controllare il nome e la versione del server prima dell'accesso. Per impostazione predefinita, Lync esegue queste verifiche prima del'accesso.</p></td>
</tr>
<tr class="odd">
<td><p>Abilita con BITS per il download dei file del servizio Rubrica<br />
(EnableBitsForGalDownload)</p></td>
<td><p>Consente a Lync di utilizzare BITS (Background Intelligent Transfer Service) per scaricare i file del servizio Rubrica.</p></td>
</tr>
<tr class="even">
<td><p>Configura modalità di sicurezza SIP<br />
(EnableSIPHighSecurityMode)</p></td>
<td><p>Consente a Lync di inviare e ricevere messaggi istantanei in modo più sicuro. Questo criterio non ha effetto sui servizi di Windows .NET o Microsoft Exchange Server.</p>
<p>Se non si configura l'impostazione di questo criterio, Lync può utilizzare qualsiasi trasporto. Ma se non utilizza TLS e se il server autentica gli utenti, Lync deve utilizzare l'autenticazione NTLM o Kerberos.</p></td>
</tr>
<tr class="odd">
<td><p>Ritardo iniziale download elenco indirizzi globale<br />
(GalDownloadInitialDelay)</p></td>
<td><p>Specifica il periodo di tempo che deve trascorrere prima che si verifichi un download dell'elenco indirizzi globale (GAL). Il valore predefinito è 60 minuti, il che significa che il server ritarda il download del file GAL per un periodo casuale compreso tra 0 e 60 minuti.</p></td>
</tr>
<tr class="even">
<td><p>Impedisci esecuzione di Microsoft Lync<br />
(PreventRun)</p></td>
<td><p>Impedisce l'esecuzione di Lync. È possibile configurare questa impostazione di criterio sia in Configurazione computer che in Configurazione utente, ma l'impostazione in Configurazione computer ha la precedenza.</p></td>
</tr>
<tr class="odd">
<td><p>Consenti memorizzazione password utente<br />
(SavePassword)</p></td>
<td><p>Consente a Lync di memorizzare password.</p></td>
</tr>
<tr class="even">
<td><p>Configura modalità di compressione SIP<br />
(SipCompression)</p></td>
<td><p>Specifica quando attivare la compressione SIP. Per impostazione predefinita, la compressione SIP è abilitata in base alla velocità della scheda. Tenere presente che l'impostazione di questo criterio potrebbe comportare un aumento del tempo di accesso.</p></td>
</tr>
<tr class="odd">
<td><p>Elenco domini attendibili<br />
(TrustModelData)</p></td>
<td><p>Elenca i domini attendibili che non corrispondono al prefisso del dominio SIP del cliente.</p></td>
</tr>
</tbody>
</table>


I criteri configurati nel server hanno la priorità sulle impostazioni di Criteri di gruppo e sulle opzioni client configurate dall'utente. Nella tabella riportata di seguito viene riepilogato l'ordine di priorità delle impostazioni in caso di conflitto.

### Priorità di Criteri di gruppo

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Priorità</th>
<th>Percorso o metodo di impostazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>Provisioning di tipo in-band di Lync Server 2013</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Office\15.0\Lync</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p>HKEY_CURRENT_USER\SOFTWARE\Policies\Microsoft\Office\15.0\Lync</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>Finestra di dialogo Lync - Opzioni in Lync 2013</p></td>
</tr>
</tbody>
</table>


## Per definire le impostazioni dei Criteri di gruppo utilizzando i file di modello amministrativo di Lync 2013

1.  Creare una cartella a livello radice in cui inserire tutti i file ADMX indipendenti dalla lingua. Creare ad esempio la cartella radice per l'archivio centrale nel controller di dominio nella posizione seguente:
    
    `%systemroot%\sysvol\domain\policies\PolicyDefinitions`
    

    > [!NOTE]
    > Questa procedura parte dal presupposto che si desideri gestire più computer del dominio. In questo caso si memorizzano i modelli in un archivio centrale nella cartella Sysvol sul controller di dominio principale. Si fornisce in tal modo un percorso di archiviazione centrale per i modelli amministrativi del dominio.



2.  Creare una sottocartella per ogni lingua che si intende usare. Le sottocartelle conterranno i file di risorse ADML specifici della lingua. Creare ad esempio una sottocartella per l'inglese degli Stati Uniti (EN-US) nella posizione seguente:
    
    `%systemroot%\sysvol\domain\policies\PolicyDefinitions\EN-US`

Per informazioni dettagliate sui file ADMX, vedere la guida dettagliata alla gestione dei file ADMX dei Criteri di gruppo all'indirizzo [http://go.microsoft.com/fwlink/?linkid=75124\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=75124%26clcid=0x410).

