---
title: 'Lync Server 2013: attività settimanali'
TOCTitle: Attività settimanali
ms:assetid: d564839b-b49d-4c5d-b67e-dc5abb0f6980
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn722432(v=OCS.15)
ms:contentKeyID: 62281965
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Attività settimanali in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-08-17_

Le attività settimanali si riferiscono in genere alla raccolta e all'analisi di registri e rapporti.

## Archiviare i registri eventi

Se non sono stati configurati per la sovrascrittura di eventi, a seconda delle necessità, i registri eventi devono essere archiviati ed eliminati periodicamente. Questa operazione è importante soprattutto per i registri protezione, che possono essere richiesti quando si esaminano eventuali tentativi di violazione della protezione.

L'organizzazione dovrà definire criteri e procedure per l'archiviazione dei registri.

## Creare rapporti

Creare rapporti sullo stato per supportare la pianificazione della capacità, la verifica dei contratti di servizio e l'analisi delle prestazioni. Utilizzare i dati forniti giornalmente dal registro eventi e dal Monitor di sistema per creare rapporti sull'utilizzo della CPU, della memoria e dei dischi, oppure servirsi di System Center Operations Manager per generare rapporti sulla disponibilità e sul tempo di attività.

L'organizzazione dovrà definire criteri e procedure per i rapporti sullo stato.

## Rapporti operazioni non consentite

Ogni settimana condurre un controllo settimanale sui rapporti delle operazioni non consentite inerenti a Lync Server. Il controllo deve includere quanto segue:

  - Principali operazioni non consentite generate, risolte e in sospeso.

  - Soluzioni per le operazioni non consentite non risolte.

  - Aggiornamento dei rapporti che includa i ticket dei nuovi problemi.

  - Aggiornamento di un archivio documenti per le guide alla risoluzione dei problemi e le relazioni finali in caso di interruzioni.

Siccome la scelta del sistema di tracciamento delle operazioni consentite è indipendente da Lync Server, non sono disponibili puntatori o istruzioni specifiche. Consultare la documentazione relativa al sistema prescelto dall'organizzazione.

## Verificare le prestazioni e i registri IIS

Condurre un'analisi settimanale delle prestazioni e dei registri di Internet Information Services (IIS). Per ulteriori informazioni sulle modalità di monitoraggio delle prestazioni e dei registri IIS, vedere [Panoramica sulla registrazione di eventi IIS (Internet Information Services) di Windows Server 2003](http://go.microsoft.com/fwlink/?linkid=36077). Nell'analisi deve essere incluso quanto segue:

  - Contatori della cache servizio Web per monitorare la cache del servizio WWW.

  - Contatori di pagine ASP per monitorare le applicazioni eseguite come ASP.

Per ulteriori informazioni sulle modalità di monitoraggio delle prestazioni e dei registri IIS, vedere [Panoramica sulla registrazione di eventi IIS (Internet Information Services) di Windows Server 2003](http://go.microsoft.com/fwlink/?linkid=36077).

## Generare rapporti sui database

**Per generare rapporti nel database SQL, attenersi alla seguente procedura.**

1.  Aprire il Lync Server 2013.

2.  Nell'albero della console, espandere il nodo della foresta, quindi i **pool Enterprise** e infine fare clic sul pool per cui si desidera generare un rapporto di database.

3.  Nel riquadro dei dettagli, fare clic sulla scheda **Database**.

4.  Nella scheda **Database**, eseguire le operazioni seguenti:
    
    1.  Per visualizzare il nome del database, espandere **Impostazioni generali**.
    
    2.  Per recuperare le statistiche di riepilogo relative all'utente corrente per il pool, espandere **Rapporti riepilogo utenti** e quindi fare clic su **Vai** per visualizzare i risultati.
    
    3.  Per recuperare i dati correnti per utente per un utente del pool, espandere **Rapporti per utente**, immettere l'URI SIP dell'utente e quindi fare clic su **Vai** per visualizzare i risultati.

Per recuperare le statistiche di riepilogo relative alla conferenza corrente per il pool, espandere**Rapporti riepilogativi conferenze**e quindi fare clic su**Vai** per visualizzare i risultati.

## Verificare la disponibilità di aggiornamenti di Lync Server e della sicurezza

Individuare i nuovi aggiornamenti, service pack e aggiornamenti rapidi. All'occorrenza, sottoporli a test in un laboratorio apposito e organizzarne la distribuzione nei server di produzione mediante le procedure di controllo delle modifiche. Gli aggiornamenti dei componenti Lync Server sono da oggi inclusi nell'aggiornamento Windows. L'aggiornamento di tutti i componenti di Lync Server deve avvenire contemporaneamente in tutti i server applicabili che eseguono Lync Server.

## Eseguire Best Practice Analyzer di Lync Server 2013

Lo strumento Best Practices Analyzer di Lync Server 2013 è uno strumento diagnostico che raccoglie informazioni di configurazione e determina se la configurazione è impostata in base alle procedure consigliate da Microsoft. La documentazione di questo strumento è disponibile all'indirizzo [Best Practices Analyzer di Lync Server 2013](lync-server-2013-lync-server-best-practices-analyzer.md) e [Eseguire Best Practices Analyzer](https://technet.microsoft.com/it-it/library/gg398652\(v=ocs.15\)).

Lo strumento pone a confronto i dati di configurazione della distribuzione in uso con un insieme di regole predefinite per Lync Server e segnala potenziali problemi. Per ogni problema segnalato, vengono fornite la configurazione corrente nell'ambiente Lync Server e la configurazione consigliata.

Con il corretto accesso di rete, lo strumento è in grado di analizzare l'AD DS e i server su cui è in esecuzione Lync Server 2013 e svolgere le seguenti attività:

  - Eseguire preventivamente controlli per verificare che la configurazione sia impostata secondo le procedure consigliate

  - Generare un elenco di problemi, ad esempio impostazioni di configurazione non ottimali, opzioni non supportate o non consigliate

  - Valutare lo stato di integrità generale di un sistema

  - Risolvere problemi specifici

  - Richiedere all'utente di scaricare eventuali aggiornamenti disponibili

  - Fornire documentazione online e in locale sui problemi segnalati, inclusi suggerimenti per la soluzione

  - Generare informazioni di configurazione che è possibile acquisire per un utilizzo successivo

Verificare che RTCBPA.msi sia installato in tutti i server Lync Server 2013 e generare un rapporto settimanale di verifica dell'integrità. Esaminare i risultati e, se necessario, apportare correzioni.

## Esaminare le cifre relative alle prestazioni dei contratti di servizio

Esaminare i dati chiave delle prestazioni relativi alla settimana precedente. Confrontare le prestazioni con i requisiti del contratto di servizio. Individuare tendenze ed elementi che non sono conformi ai valori target.

## Esaminare il Management Pack di System Center Operations Manager e i rapporti sulla qualità dell'esperienza

Acquisire ed esaminare il Management Pack di Lync Server 2013 e i rapporti sulla qualità dell'esperienza.

## Creazione e visualizzazione di rapporti di database per i pool Enterprise

**Per generare rapporti sui pool, attenersi alla seguente procedura**

1.  Aprire il Lync Server 2013.

2.  Nell'albero della console, espandere il nodo della foresta, quindi i **pool Enterprise** e infine fare clic sul pool per cui si desidera generare un rapporto di database.

3.  Nel riquadro dei dettagli, fare clic sulla scheda **Database**.

4.  Nella scheda **Database**, eseguire le operazioni seguenti:
    
    1.  Per visualizzare il nome del database, espandere **Impostazioni generali**.
    
    2.  Per recuperare le statistiche di riepilogo relative all'utente corrente per il pool, espandere **Rapporti riepilogo utenti** e quindi fare clic su **Vai** per visualizzare i risultati.
    
    3.  Per recuperare i dati correnti per utente per un utente del pool, espandere **Rapporti per utente** immettere l'URI SIP dell'utente e quindi fare clic su **Vai** per visualizzare i risultati.

Per recuperare le statistiche di riepilogo relative alla conferenza corrente per il pool, espandere **Rapporti riepilogativi conferenze** e quindi fare clic su **Vai** per visualizzare i risultati.

Per ogni pool Enterprise, gli amministratori possono ricorrere alla scheda **Database** per visualizzare il nome del database, nonché per recuperare e visualizzare rapporti del database.

### Descrizioni e rapporti di database

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Sezione</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Rapporti riepilogo utenti</p></td>
<td><p>Dbanalyze /v /report:diag [/sqlserver:value]</p>
<p>In questa sezione sono disponibili informazioni aggregate sugli utenti di un pool, ad esempio il numero degli utenti abilitati, il numero di contatti medio per ogni utente e il numero di utenti per funzionalità specifiche.</p>
<p>Quando si utilizzano questi rapporti, può essere utile conoscere quanto segue:</p>
<ul>
<li><p>Un utente abilitato è un utente che ha ricevuto l'abilitazione per Lync Server 2013 tramite lo snap-in Utenti e computer di Active Directory.</p></li>
<li><p>Un utente attivo è un utente che ha eseguito l'accesso o la registrazione.</p></li>
<li><p>Nei rapporti di riepilogo è inoltre disponibile un insieme di informazioni statistiche sui contatti. Tali statistiche sono valide solo per gli utenti che hanno eseguito l'accesso almeno una volta e che dispongono di almeno un contatto. Di conseguenza, il numero minimo di contatti visualizzato non può essere in genere 0. Per via di questo comportamento, se un utente non ha alcun contatto ma è attivo in quanto ha eseguito la registrazione, in alcuni campi statistici potrebbe essere visualizzato: &lt;empty&gt;.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Rapporti per utente</p></td>
<td><p>Dbanalyze /v /report:disk [/sqlserver:value]</p>
<p>A differenza dei rapporti di riepilogo, elaborati sulla base di una popolazione di utenti, questi rapporti sono attinenti a un utente specifico.</p></td>
</tr>
<tr class="odd">
<td><p>Rapporti riepilogativi conferenze</p></td>
<td><p>Dbanalyze /v /report:conf [/sqlserver:value]</p>
<p>In questa sezione sono disponibili informazioni aggregate sulle statistiche di riepilogo delle conferenze per il pool, ad esempio, il numero di conferenze attive e il totale dei partecipanti.</p></td>
</tr>
<tr class="even">
<td><p>Rapporti riepilogo utenti</p></td>
<td><p>Dbanalyze /v /report:diag [/sqlserver:value]</p>
<p>In questa sezione sono disponibili informazioni aggregate sugli utenti di un pool, ad esempio il numero degli utenti abilitati, il numero di contatti medio per ogni utente e il numero di utenti per funzionalità specifiche.</p>
<p>Quando si utilizzano questi rapporti, può essere utile conoscere quanto segue:</p>
<ul>
<li><p>Un utente abilitato è un utente che ha ricevuto l'abilitazione per Lync Server 2013 tramite lo snap-in Utenti e computer di Active Directory.</p></li>
<li><p>Un utente attivo è un utente che ha eseguito l'accesso o la registrazione.</p></li>
<li><p>Nei rapporti di riepilogo è inoltre disponibile un insieme di informazioni statistiche sui contatti. Tali statistiche sono valide solo per gli utenti che hanno eseguito l'accesso almeno una volta e che dispongono di almeno un contatto. Di conseguenza, il numero minimo di contatti visualizzato non può essere in genere 0. Per via di questo comportamento, se un utente non ha alcun contatto ma è attivo in quanto ha eseguito la registrazione, in alcuni campi statistici potrebbe essere visualizzato: &lt;empty&gt;.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Rapporti per utente</p></td>
<td><p>Dbanalyze /v /report:disk [/sqlserver:value]</p>
<p>A differenza dei rapporti di riepilogo, elaborati sulla base di una popolazione di utenti, questi rapporti sono attinenti a un utente specifico.</p></td>
</tr>
<tr class="even">
<td><p>Rapporti riepilogativi conferenze</p></td>
<td><p>Dbanalyze /v /report:conf [/sqlserver:value]</p>
<p>In questa sezione sono disponibili informazioni aggregate sulle statistiche di riepilogo delle conferenze per il pool, ad esempio, il numero di conferenze attive e il totale dei partecipanti.</p></td>
</tr>
</tbody>
</table>


## Esecuzione di Bandwidth Utilization Analyzer

Bandwidth Utilization Analyzer è uno strumento che consente di creare rapporti con varie visualizzazioni dell'utilizzo della larghezza di banda da parte degli endpoint UC tra collegamenti WAN nella rete aziendale. Tali rapporti possono essere usati per ottenere informazioni sullo schema di utilizzo della larghezza di banda e per supportare la pianificazione della capacità della larghezza di banda. Scorre inoltre la capacità della larghezza di banda assegnata ai vari collegamenti.

Lo strumento esegue le operazioni seguenti:

  - Genera rapporti specifici per l'utilizzo dell'audio sulla rete

  - Favorisce una pianificazione della capacità più efficace e consente di scorrere la capacità della larghezza di banda assegnata ai vari collegamenti

Bandwidth Utilization Analyzer consente di generare tracce grafiche dei rapporti relativi alla capacità e all'utilizzo della larghezza di banda, come illustrato di seguito:

  - Tutti i collegamenti WAN nella rete aziendale

  - Filtro in base ai collegamenti WAN selezionati

  - Filtro in base ai collegamenti WAN che hanno superato la capacità del collegamento

  - Filtro in base ai collegamenti WAN che hanno sottoutilizzato la larghezza di banda allocata

  - Filtro in base ai collegamenti WAN che stavano raggiungendo livelli critici (utilizzo della larghezza di banda superiore al 90% della capacità della larghezza di banda del collegamento WAN)

  - Filtro in base al tipo di collegamento WAN: collegamenti rete-sito, collegamenti tra più aree di rete e collegamenti all'interno di un sito

  - Filtro in base all'area di rete

La documentazione di questo strumento è disponibile all'indirizzo[Documentazione sugli strumenti del Resource Kit di Lync Server 2013](https://technet.microsoft.com/it-it/library/jj945604\(v=ocs.15\)).

## Vedere anche

#### Ulteriori risorse

[Elenco di controllo delle attività settimanali](lync-server-2013-operations-checklists.md)

