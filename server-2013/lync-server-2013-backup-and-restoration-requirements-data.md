---
title: 'Requisiti di backup e ripristino: dati'
TOCTitle: 'Requisiti di backup e ripristino: dati'
ms:assetid: ecfb8e4d-cb4f-476d-9772-4486bd683c04
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh202194(v=OCS.15)
ms:contentKeyID: 52062464
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti di backup e ripristino: dati

 

_**Ultima modifica dell'argomento:** 2013-03-26_

In Lync Server vengono utilizzate impostazioni e informazioni di configurazione archiviate in database, nonché dati archiviati in database e in archivi file. In questa sezione vengono descritti i dati di cui è necessario eseguire il backup per avere la possibilità di ripristinare il servizio in caso di errori o guasti. Vengono inoltre identificati i dati e i componenti utilizzati in Lync Server da sottoporre a backup separatamente.

## Requisiti di impostazioni e dati di configurazione

In questo argomento sono riportate le procedure di backup e ripristino delle impostazioni e delle informazioni di configurazione necessarie per il ripristino del servizio Lync Server. Le informazioni di configurazione sono memorizzate nell'archivio di gestione centrale oppure in un altro database di back-end o server Standard Edition.

Nella tabella seguente sono identificate le impostazioni e le informazioni di configurazione di cui è necessario eseguire il backup e il ripristino.

### Impostazioni e dati di configurazione

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di dati</th>
<th>Dove sono archiviati</th>
<th>Descrizione/Quando eseguire il backup</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Informazioni di configurazione della topologia</p></td>
<td><p>archivio di gestione centrale (database: Xds.mdf)</p></td>
<td><p>Impostazioni relative a topologia, criteri e configurazione.</p>
<p>Eseguire il backup in occasione dei backup regolari e dopo aver utilizzato Pannello di controllo di Lync Server o i cmdlet per modificare la configurazione o i criteri.</p></td>
</tr>
<tr class="even">
<td><p>Informazioni sulle posizioni</p></td>
<td><p>archivio di gestione centrale (database: Lis.mdf)</p></td>
<td><p>Informazioni sulla configurazione del servizio Enhanced 9-1-1 (E9-1-1) di VoIP aziendale. Queste informazioni sono in genere statiche.</p>
<p>Eseguire il backup in occasione dei backup regolari.</p></td>
</tr>
<tr class="odd">
<td><p>Informazioni di configurazione di Response Group</p></td>
<td><p>Server back-end o server Standard Edition (database: RgsConfig.mdf)</p></td>
<td><p>Gruppi di agenti, code e flussi di lavoro di Response Group.</p>
<p>Eseguire il backup in occasione dei backup regolari e dopo aver aggiunto o modificato gruppi di agenti, code o flussi di lavoro.</p></td>
</tr>
</tbody>
</table>


## Requisiti dei dati

Di seguito è disponibile un elenco dei dati di Lync Server di cui è necessario eseguire il backup, per consentire il ripristino del servizio Lync Server in caso di errore.

Si noti che alcuni tipi di dati non sono necessari per il recupero. Questo argomento non include procedure per il backup di questi tipi di dati, inclusi i seguenti:

  - Dati utente temporanei, ad esempio endpoint e sottoscrizioni, server per conferenze attivi e stati di conferenza transitori (database: RtcDyn.mdf)

  - Dati della Rubrica (database: Rtcab.mdf e Rtcab1.mdf). Il database della Rubrica viene rigenerato automaticamente da Servizi di dominio Active Directory.

  - Informazioni dinamiche per l'applicazione Parcheggio di chiamata (database: CpsDyn.mdf)

  - Dati di Response Group temporanei, ad esempio lo stato di accesso degli agenti e le informazioni sulle chiamate in attesa (database: RgsDyn.mdf)

  - Il database di conformità per Chat persistente (database: MgcComp.mdf). Se la conformità di Chat persistente è abilitata, le informazioni nel database di conformità di Chat persistente saranno temporanee, purché sia disponibile un adattatore configurato per la lettura di informazioni dal database e la conversione in un formato alternativo. Il database di conformità di Chat persistente viene quindi considerato temporaneo.
    
    Lync Server 2013 server Chat persistente include un adattatore XML. È anche possibile installare adattatori personalizzati, che acquisiscono questi dati e li spostano in altre origini, ad esempio archivi ospitati da Exchange.

Nella tabella seguente sono identificati i dati di cui è necessario eseguire il backup e il ripristino.

### Dati archiviati in database

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di dati</th>
<th>Dove sono archiviati</th>
<th>Descrizione/Quando eseguire il backup</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dati utente permanenti</p></td>
<td><p>Server back-end o server Standard Edition (database: RTCXDS.mdf)</p></td>
<td><p>Diritti utente, elenchi Contatti, dati di server o pool, conferenze pianificate e così via. Questi dati utente non includono contenuti caricati in una conferenza.</p>
<p>Eseguire il backup in occasione dei backup regolari. Queste informazioni sono dinamiche, ma la perdita di aggiornamenti non è catastrofica per Lync Server se è necessario ripristinare l'ultimo backup regolare. Se gli elenchi Contatti sono critici per l'organizzazione, è possibile eseguire il backup di questi dati più di frequente.</p></td>
</tr>
<tr class="even">
<td><p>Dati di archiviazione</p></td>
<td><p>Database di archiviazione (database: LcsLog.mdf)</p>
<p>Sarà possibile archiviare questi dati in Exchange 2013, se è stata abilitata l'opzione di integrazione di Microsoft Exchange. In caso contrario, questi dati verranno mantenuti in un database di archiviazione di Lync Server, che può essere collocato con un altro database di Lync Server oppure può essere autonomo su un server database separato.</p></td>
<td><p>Contenuto di messaggistica istantanea e riunioni.</p>
<p>Questi dati non sono critici per Lync Server, ma possono esserlo per l'organizzazione per motivi di regolamentazione. Stabilire la pianificazione dei backup di conseguenza.</p>
<p>Lync Server supporta solo il modello di recupero con registrazione minima per i database di archiviazione. Con questo modello, i database vengono ripristinati nel punto dell'ultimo backup completo, il che significa che non è possibile ripristinare un database nel punto di errore o in base a una data e un'ora specifiche.</p></td>
</tr>
<tr class="odd">
<td><p>Dati di monitoraggio</p></td>
<td><p>Database di monitoraggio (LcsCDR.mdf e QoeMetrics.mdf)</p>
<p>Questi database possono essere collocati insieme a un altro database di Lync Server oppure possono essere autonomi su un server database separato.</p></td>
<td><p>Registrazione dettagli chiamata (LcsCDR.mdf) e metriche QoE (QoeMetrics.mdf).</p>
<p>La registrazione dettagli chiamata contiene dati dinamici che possono essere critici per l'azienda. Stabilire la pianificazione dei backup valutando se questi record sono necessari o meno per motivi di regolamentazione.</p>
<p>Le informazioni su QoE sono dinamiche. La perdita di questi dati non è critica per il funzionamento di Lync Server, ma può esserlo per l'azienda. Stabilire la pianificazione dei backup in base al grado di criticità delle informazioni per l'organizzazione.</p>
<p>Lync Server supporta solo il modello di recupero con registrazione minima per i database di monitoraggio. Con questo modello, i database vengono ripristinati nel punto dell'ultimo backup completo, il che significa che non è possibile ripristinare un database nel punto di errore o in base a una data e un'ora specifiche.</p></td>
</tr>
<tr class="even">
<td><p>Dati di Chat persistente</p></td>
<td><p>Database di Chat persistente (mgd.mdf).</p>
<p>Questo database può essere collocato insieme a un altro database di Lync Server oppure può essere autonomo su un server database separato.</p></td>
<td><p>I dati di Chat persistente sono contenuti di chat effettivi inseriti in chat room. Questi dati sono spesso essenziali per l'azienda.</p>
<p>È possibile scegliere di usare il backup di SQL Server oppure esportare il database utilizzando il cmdlet <strong>Export-CsPersistentChatData</strong>, disponibile in Lync Server. Per il recupero dei dati, è possibile importare e ripristinare il database fino al punto dell'ultimo backup completo, ovvero non è possibile ripristinare il database fino al punto di errore.</p></td>
</tr>
</tbody>
</table>


## Requisiti dei dati dell'archivio file

In una distribuzione di Enterprise Edition, l'archivio file di Lync Server si trova in genere in un file server. In una distribuzione di Standard Edition, l'archivio file di Lync Server si trova per impostazione predefinita nell'server Standard Edition. In genere, è disponibile un unico archivio file di Lync Server condiviso per un sito. L'archivio file di Chat persistente utilizza la stessa condivisione file dell'archivio file di Lync Server.

I percorsi degli archivi file sono identificati dal formato \\\\server\\nome condivisione. Per individuare i percorsi specifici degli archivi file, aprire Generatore di topologie ed esaminare il nodo **Archivi file**.

Nella tabella seguente sono identificati gli archivi file di cui è necessario eseguire il backup e il ripristino.

### Archivi file

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di dati</th>
<th>Dove sono archiviati</th>
<th>Descrizione/Quando eseguire il backup</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Archivio file di Lync Server</p></td>
<td><p>In genere in un file server, in un cluster di file o in un server Standard Edition</p></td>
<td><p>Contenuto delle riunioni, metadati del contenuto delle riunioni, log di conformità delle riunioni, file di dati delle applicazioni, file di aggiornamento per i dispositivi, file audio per le applicazioni Response Group, Parcheggio di chiamata e Annuncio e file inseriti in chat room di Chat persistente.</p>
<p>Eseguire il backup in occasione dei backup regolari.</p></td>
</tr>
</tbody>
</table>


## Altri requisiti di backup

Per aiutare ad assicurare la possibilità di ripristinare i servizi di Lync Server in caso di errore, è necessario eseguire il backup di alcuni componenti necessari che non fanno parte di Lync Server stesso. I componenti seguenti non vengono sottoposti a backup o ripristino come parte del processo di backup e ripristino di Lync Server descritto in questo documento:

  - **Servizi di dominio Active Directory** È necessario eseguire il backup di Servizi di dominio Active Directory (AD DS) utilizzando gli strumenti di Active Directory contemporaneamente all'esecuzione del backup di Lync Server. È importante che AD DS sia sempre sincronizzato con Lync Server, per evitare problemi che si possono verificare quando Lync Server prevede di ricevere oggetti contatto non corrispondenti a quelli in AD DS. In AD DS vengono archiviate le impostazioni seguenti, che vengono utilizzate da Lync Server:
    
      - URI SIP dell'utente e altre impostazioni utente.
    
      - Oggetti contatto per applicazioni quali Response Group e Operatore Conferenza.
    
      - Puntatore all'archivio di gestione centrale.
    
      - Account di autenticazione Kerberos (oggetto computer facoltativo) e gruppi di sicurezza di Lync Server.
    
    Per informazioni dettagliate sul backup e il ripristino di AD DS in Windows Server 2008, vedere "Guida dettagliata al backup e al ripristino di Servizi di dominio Active Directory" all'indirizzo <http://go.microsoft.com/fwlink/?linkid=209105>.

  - **Autorità di certificazione e certificati**   Attenersi ai criteri dell'organizzazione per eseguire il backup dell'autorità di certificazione (CA) e dei certificati. Se si utilizzano chiavi private esportabili, è possibile eseguire il backup del certificato come chiave privata e quindi esportarla seguendo le procedure riportate in questo documento per il ripristino di Lync Server. Se si utilizza un CA interna, è possibile ripeterne l'iscrizione se è necessario ripristinare Lync Server. È importante conservare la chiave privata in un posto sicuro dove sarà disponibile in caso di problemi con un computer.

  - **System Center Operations Manager**   Se si utilizza Microsoft System Center Operations Manager (in precedenza Microsoft Operations Manager) per il monitoraggio della distribuzione di Lync Server, è possibile facoltativamente eseguire il backup dei dati che vengono creati durante il monitoraggio di Lync Server. Utilizzare il processo di backup di SQL Server standard per eseguire il backup dei file di System Center Operations Manager. Questi file non vengono ripristinati durante il recupero.

  - **Configurazione dei gateway PSTN (Public Switched Telephone Network)**   Se si utilizzano VoIP aziendale o Survivable Branch Appliance, è necessario eseguire il backup della configurazione dei gateway PSTN. Per informazioni dettagliate sul backup e il ripristino delle configurazioni di gateway PSTN, contattare il fornitore.

  - **Versioni coesistenti di Lync Server o Office Communications Server** Se la distribuzione di Lync Server 2013 coesiste con Lync Server 2010 o una versione precedente di Office Communications Server, non è possibile utilizzare le procedure descritte in questo documento per il backup o il ripristino della versione precedente. È invece necessario utilizzare le procedure documentate specificamente per la versione precedente. Per informazioni dettagliate sul backup e il ripristino di Lync Server 2010, vedere <http://go.microsoft.com/fwlink/?linkid=265417>. Per informazioni dettagliate sul backup e il ripristino di Microsoft Office Communications Server 2007 R2, vedere <http://go.microsoft.com/fwlink/?linkid=168162>.

  - **Informazioni sull'infrastruttura** È necessario eseguire il backup delle informazioni sull'infrastruttura, ad esempio configurazione di firewall, bilanciamento del carico e IIS (Internet Information Services), record DNS (Domain Name System) e indirizzi IP e configurazione di DHCP (Dynamic Host Configuraton Protocol). Per informazioni dettagliate sul backup di questi componenti, contattare i rispettivi fornitori.

  - **Microsoft Exchange e servizio di messaggistica unificata di Microsoft Exchange** Eseguire il backup e il ripristino di Microsoft Exchange e Messaggistica unificata di Exchange come illustrato nella documentazione relativa a Microsoft Exchange. Per informazioni dettagliate sul backup e il ripristino di Exchange Server 2013, vedere <http://go.microsoft.com/fwlink/?linkid=285384>. Per informazioni dettagliate sul backup e il ripristino di Exchange Server 2010, vedere <http://go.microsoft.com/fwlink/?linkid=209179>.
    
    Si noti che Lync Server 2013 introduce la possibilità di archiviare gli elenchi contatti degli utenti, le foto ad alta definizione degli utenti e i dati di archiviazione in Exchange 2013. Per informazioni sul backup di questi tipi di dati, vedere l'elenco seguente:
    
      - Il backup delle **foto ad alta definizione** viene eseguito come parte del backup di Exchange Server.
    
      - L'**archivio contatti unificato** è una delle novità disponibili in Lync Server 2013. L'archivio contatti unificato consente agli utenti di mantenere tutte le informazioni sui contatti in Exchange 2013.
        
        È consigliabile assicurarsi che i backup siano aggiornati per gli utenti in merito all'archiviazione dei contatti utente nell'archivio contatti unificato o nel server Back End Lync. Gli scenari seguenti illustrano le circostanze in cui la migrazione dei contatti utente nell'archivio contatti unificato può provocare problemi per il processo di backup e ripristino.
        
        **Scenario 1:** viene eseguita la migrazione dei contatti utente all'archivio contatti unificato e il ripristino viene eseguito da un backup di Lync Server effettuato prima della migrazione dei contatti utente. In questo scenario i contatti utente potranno risultare non aggiornati per al massimo una giornata, fino all'inizio della migrazione dei contatti utente in Exchange da parte dell'attività di migrazione di Lync Server. Si noti che, poiché la migrazione dei contatti utente archivio contatti unificato è stata eseguita in precedenza, verranno utilizzate le informazioni sui contatti di Exchange. In questo scenario non è necessario alcun intervento da parte dell'amministratore.
        
        **Scenario 2:** i contatti utente sono stati archiviati in precedenza nell'archivio contatti unificato, ma è stato quindi eseguito il rollback. Viene eseguito un ripristino da un backup di Lync Server effettuato quando i contatti utente sono stati archiviati nell'archivio contatti unificato. In questo scenario è possibile che un messaggio di errore di `Error: Incorrect Exchange Version` nei log del client o del server Lyss indichi che si tratta di un problema. L'utente potrà accedere all'elenco contatti in Lync 2013 direttamente da Exchange, ma lo stato del client non corrisponderà allo stato di Lync Server. Per risolvere questo problema, è necessario che un amministratore esegua i cmdlet **Invoke-CsUCSRollback** per gli utenti interessati.
    
      - I **dati di archiviazione** possono essere archiviati in Exchange 2013. Questi dati non sono critici per Lync Server, ma possono essere critici per fini normativi interni dell'organizzazione. Se i dati di archiviazione vengono memorizzati in Exchange e sono critici per l'organizzazione, eseguire le procedure di backup e di ripristino di Exchange. Si noti che i dati di archiviazione memorizzati in Exchange non possono essere spostati di nuovo in Lync Server. Non è inoltre possibile spostare in Exchange in alcun modo i dati già archiviati nel database di archiviazione di Lync.

