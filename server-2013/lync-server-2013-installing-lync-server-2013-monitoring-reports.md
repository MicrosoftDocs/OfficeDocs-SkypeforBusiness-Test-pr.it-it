---
title: Installazione dei rapporti di monitoraggio di Lync Server 2013
TOCTitle: Installazione dei rapporti di monitoraggio di Lync Server 2013
ms:assetid: 6f417569-b100-442c-ad48-fdd794626cf7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204989(v=OCS.15)
ms:contentKeyID: 49300919
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Installazione dei rapporti di monitoraggio di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

I rapporti di monitoraggio di Microsoft Lync Server 2013 offrono moltissime informazioni sulla qualità e quantità delle sessioni di comunicazione che hanno luogo presso l'organizzazione. Tuttavia, i rapporti di monitoraggio non sono installati automaticamente con l'installazione di Lync Server 2013; è necessario installare i rapporti di monitoraggio separatamente, e soltanto al termine dell'installazione di Lync Server.


> [!NOTE]
> È consigliabile installare i rapporti di monitoraggio sullo stesso computer sul quale è installato il database di monitoraggio, al fine di semplificare il processo di assegnazione delle autorizzazioni di accesso ai rapporti. Se si installano i rapporti di monitoraggio sul computer che ospita l'archivio di monitoraggio, non si avrà bisogno di configurare le autorizzazioni che permettono a un database sul computer di interagire con i servizi di reporting eseguiti su un secondo computer.



I rapporti di monitoraggio di Lync Server includono più di 30 rapporti concepiti per offrire informazioni dettagliate su conferenze, sessioni di messaggistica istantanea peer-to-peer, registrazioni utente, applicazione dei Response Group e molto altro. Nella versione 2013, i rapporti di monitoraggio di Lync Server includono diversi miglioramenti:

  - **Nuovo rapporti di qualità delle chiamate**. Questi nuovi rapporti includono il [Rapporto di confronto qualità multimediale in Lync Server 2013](lync-server-2013-media-quality-comparison-report.md), che mette a confronto la qualità di diversi tipi di chiamate (ad esempio, chiamate cablate rispetto a chiamate wireless), e [Rapporto Tempo di partecipazione alla conferenza](lync-server-2013-conference-join-time-report.md), che fornisce informazioni sulla quantità di tempo necessaria affinché un utente possa partecipare a una conferenza.

  - **Rapporti migliorati per l'analisi e la risoluzione dei problemi delle sessioni video e di condivisione applicazioni.** il [Rapporto riepilogativo qualità multimediale in Lync Server 2013](lync-server-2013-media-quality-summary-report.md) consente di analizzare le chiamate video e di condivisione delle applicazioni, mentre il [Rapporto prestazioni dei server in Lync Server 2013](lync-server-2013-server-performance-report.md) fornisce dettagli sulle prestazioni dei server che generano queste chiamate. Le metriche relative a video e condivisione applicazioni sono fornite inoltre dal [Rapporto Dettagli sessione peer-to-peer in Lync Server 2013](lync-server-2013-peer-to-peer-session-detail-report.md) e dal [Rapporto Dettagli conferenza](lync-server-2013-conference-detail-report.md).

  - **Prestazioni dei rapporti migliorate**. Il miglioramento include tempi di risposta e recupero dei dati più veloci, nonché uno spostamento più semplice e veloce all'interno dei rapporti.

Nella documentazione relativa ai rapporti di monitoraggio è possibile trovare maggiori informazioni sui singoli rapporti.


> [!NOTE]
> In Lync Server 2013 è incluso un nuovo rapporto, ovvero il sottorapporto dei dettagli di qualità della chiamata (QoE Call Detail Subreport). Questo rapporto è inteso per un uso interno, e non per un accesso diretto.



Esistono due modalità di installazione dei rapporti di monitoraggio di Lync Server: è possibile utilizzare la Distribuzione guidata di Lync Server o uno script di Windows PowerShell incluso nei file di installazione di Lync Server 2013. Indipendentemente dal metodo di installazione selezionato, è necessario assicurarsi di:

  - Possedere i diritti necessari per l'aggiunta di un ruolo del database a un account utente del database di monitoraggio.

  - Detenere il ruolo di gestione del contenuto per SQL Server Reporting Services, che consente di distribuire rapporti a SQL Server Reporting Services.

Per installare i rapporti di monitoraggio attraverso la Distribuzione guidata, eseguire le operazioni seguenti:

1.  Fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Distribuzione guidata di Lync Server**.

2.  Nella Distribuzione guidata fare clic su **Distribuisci rapporti di monitoraggio** per avviare la Distribuzione guidata dei rapporti di monitoraggio.

3.  Nella pagina **Specifica database di monitoraggio** della Distribuzione guidata dei rapporti di monitoraggio, assicurarsi che il nome di dominio completo del computer che ospita l'archivio di monitoraggio compaia nell'elenco a discesa **Database di monitoraggio**. (Se si hanno più archivi di monitoraggio, è necessario selezionare il server appropriato dall'elenco a discesa.) Verificare che nella casella **Istanza di SQL Server Reporting Services (SSRS)** compaia l'istanza di SQL Server Reporting Services (SSRS) appropriata, ad esempio **atl-sql-001.litwareinc.com/archinst**, quindi fare clic su **Avanti**.

4.  Nella casella **Nome utente** della pagina **Specifica credenziali**, digitare il nome di dominio e il nome utente dell'account che si desidera utilizzare per l'accesso ai rapporti di monitoraggio (ad esempio, **litwareinc\\davidegarghentini**). Se non si utilizza questo formato (dominio\\nome utente) verrà restituito un errore.
    
    Digitare la password dell'account utente nella casella **Password** e fare clic su **Avanti**. Si noti che non sono necessari diritti speciali per questo account. L'account otterrà automaticamente l'accesso richiesto e le autorizzazioni per il database al termine della configurazione.

5.  Nella casella Gruppo utenti della pagina **Specifica gruppo di sola lettura**, inserire il nome di un gruppo di sicurezza al quale sarà garantito l'accesso di sola lettura a SQL Server Reporting Services. Ad esempio, per fornisce un tipo di accesso amministratore di sola lettura ai rapporti, inserire **RTCUniversalReadOnlyAdmins** e fare clic su **Avanti**.

6.  Nella pagina **Esecuzione comandi in corso** fare clic su **Fine**.

I rapporti di monitoraggio possono anche essere installati da Lync Server Management Shell eseguendo lo script DeployReports.ps1; questo script di Windows PowerShell si trova nella cartella \\Setup\\ReportingSetup del supporto di installazione di Lync Server. Per installare i rapporti di monitoraggio utilizzando DeployReports.ps1, digitare un comando simile al seguente nel prompt di Management Shell:

    D:\Setup\AMD64\Setp\ReportingSetup\DeployReports.ps1 -storedUserName "litwareinc\kenmyer" -storedPassword "p@ssw0rd" -readOnlyGroupName "RTCUniversalReadOnlyAdmins" -reportServerSqlInstance "atl-sql-001.litwareinc.com" -monitoringDatabaseId "MonitoringDatabase:atl-sql-001.litwareinc.com"

Nella seguente tabella sono illustrati i parametri utilizzati nel comando precedente:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome del parametro</th>
<th>Obbligatorio</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>storedUserName</p></td>
<td><p>Sì</p></td>
<td><p>Account utente (nel formato dominio\nome utente) utilizzato per l'accesso all'archivio di monitoraggio; ad esempio:</p>
<pre><code>-storedUserName &quot;litwareinc\kenmyer&quot;</code></pre>
<p>Affinché lo script venga eseguito correttamente, l'account deve avere le autorizzazioni per SQL Server e SQL Server Reporting Services specificate in precedenza.</p></td>
</tr>
<tr class="even">
<td><p>storedPassword</p></td>
<td><p>Sì</p></td>
<td><p>Password dell'account utente utilizzato per l'accesso all'archivio di monitoraggio.</p></td>
</tr>
<tr class="odd">
<td><p>readOnlyGroupName</p></td>
<td><p>No</p></td>
<td><p>Dominio o gruppo di sicurezza locale ai cui membri è fornito l'accesso di sola lettura ai rapporti di monitoraggio. Lo script avrà esito negativo se il gruppo specificato non esiste. Se in seguito si decide di annullare queste autorizzazioni, o di concederle ad altri utenti o gruppi, è possibile farlo attraverso SQL Service Reporting Services Report Manager.</p></td>
</tr>
<tr class="even">
<td><p>reportSqlServerInstance</p></td>
<td><p>No</p></td>
<td><p>Istanza di SQL Server che ospita il Reporting Service. L'istanza di Reporting deve essere specificata attraverso il nome di dominio completo del Report Server, ad esempio:</p>
<pre><code>-reportServerSqlInstance atl-sql-001.litwareinc.com</code></pre>
<p>Se il parametro non è incluso nello script, assumerà che il Reporting service è ospitato dalla medesima istanza SQL Server che ospita il database di monitoraggio.</p></td>
</tr>
<tr class="odd">
<td><p>monitoringDatabaseId</p></td>
<td><p>No</p></td>
<td><p>Identità del servizio per i database di monitoraggio. Attraverso il seguente comando è possibile restituire le identità dei database di monitoraggio:</p>
<pre><code>Get-CsService -MonitoringDatabase</code></pre></td>
</tr>
</tbody>
</table>


Dopo l'installazione dei rapporti di monitoraggio, è necessario utilizzare il cmdlet Set-CsReportingConfiguration per configurare l'URL utilizzato per accedere ai rapporti. Questa attività può essere eseguita da Lync Server Management Shell attraverso il seguente comando di Windows PowerShell. È consigliabile, ma non obbligatorio, utilizzare il protocollo HTTPS quando si configura l'URL dei rapporti:

    Set-CsReportingConfiguration -Identity "MonitoringDatabase:atl-sql-001.litwareinc.com" -ReportingURL "https://atl-sql-001.litwareinc.com:443/Reports_ARCHINST"

Nel comando precedente, la proprietà ReportingUrl deve essere impostata sull'URL Report Manager utilizzato da SQL Server 2008 R2 Reporting Services. L'URL può essere determinato eseguendo la seguente procedura sul computer in cui è installato SQL Server Reporting Services:

1.  Fare clic sul pulsante Start, scegliere Tutti i programmi, fare clic su Microsoft SQL Server 2008 R2, quindi su Strumenti di configurazione e su Gestione configurazione Reporting Services.

2.  Nella finestra di dialogo Connessione configurazione Reporting Services, assicurarsi che il nome del computer per i Reporting Services compaia nella casella Nome server. Selezionare l'istanza SQL Server dall'elenco a discesa Istanza Server Report, quindi fare clic su Connetti.

3.  In Gestione configurazione Reporting Services, fare clic su URL Report Manager. Nel riquadro dovrebbero comparire uno o più URL, che possono essere utilizzati come URL di Reporting URL, sebbene è consigliabile ancora una volta di utilizzare il protocollo HTTPS per la proprietà ReportingUrl.

Se è stato impostato un database mirror come database di monitoraggio, sarà anche necessario associare i rapporti di monitoraggio con il database mirror. Per informazioni dettagliate, vedere l'articolo [Associazione delle relazioni di monitoraggio a un database mirror](lync-server-2013-associating-monitoring-reports-with-a-mirror-database.md).

