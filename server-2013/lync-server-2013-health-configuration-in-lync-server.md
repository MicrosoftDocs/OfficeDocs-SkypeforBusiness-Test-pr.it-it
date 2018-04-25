---
title: Configurazione dell'integrità in Lync Server 2013
TOCTitle: Configurazione dell'integrità in Lync Server 2013
ms:assetid: c00a8c8e-c2d2-4557-8c42-211c7cc96550
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205234(v=OCS.15)
ms:contentKeyID: 49301847
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione dell'integrità in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Grazie a diversi siti Web, articoli della Microsoft Knowledge Base e strumenti del Resource Kit di Lync Server, gli amministratori che riscontrano problemi durante l'esecuzione di Lync Server possono quasi sempre trovare una soluzione a tali problemi.

Non vi è ovviamente alcun modo per garantire la totale assenza di problemi relativi a Lync Server 2013 perché sul funzionamento di Lync Server possono incidere numerosi fattori, ad esempio arresti anomali della rete e guasti hardware, che il prodotto non può controllare. Implementando il monitoraggio dello stato, gli amministratori possono identificare potenziali problemi prima che diventino problemi a tutti gli effetti. Ad esempio, gli amministratori possono utilizzare il monitoraggio di Lync Server per identificare le tendenze. Un aumento costante del numero di conferenze audio/video ad esempio può suggerire la necessità di aggiungere capacità prima che si verifichi un sovraccarico del sistema.

In modo analogo, gli amministratori possono utilizzare System Center Operations Manager per eseguire attività come l'invio di avvisi in tempo reale al verificarsi di determinati eventi ed eseguire transazioni sintetiche che testano attivamente il sistema. Le transazioni sintetiche vengono utilizzate in Lync Server per verificare che gli utenti siano in grado di svolgere correttamente attività comuni come l'accesso al sistema, lo scambio di messaggi istantanei o l'esecuzione di chiamate verso un telefono sulla rete PSTN (Public Switched Telephone Network). Ad esempio, eseguendo periodicamente questi test, è possibile rendersi conto di probabili problemi relativi agli utenti che accedono a Lync Server e avere l'opportunità di risolverli prima che il team addetto all'assistenza tecnica venga subissato di chiamate dagli utenti che non riescono a stabilire una connessione. Utilizzando System Center Operations Manager per eseguire queste transazioni sintetiche, gli amministratori possono monitorare con regolarità la distribuzione di Lync Server continuamente per 24 ore ogni giorno dovendo solo rispondere agli eventuali avvisi generati.


> [!NOTE]
> Per Lync Server 2013, il Management Pack per System Center Operations Manager è inoltre in grado di rilevare problemi "esterni" che possono influire negativamente su Lync Server. Ad esempio, gli amministratori possono essere avvisati se Internet Information Services (IIS) è offline, le risorse di sistema in un computer Lync Server scendono al di sotto di un livello specificato oppure si verifica un problema hardware su un computer Lync Server.



La configurazione dello stato in Lync Server 2013 si basa su System Center Operations Manager e sull'utilizzo dei Management Pack di Lync Server. Tali Management Pack includono diverse nuove funzionalità e miglioramenti, tra cui:

  - **Disponibilità degli scenari da qualsiasi posizione.** Nel Management Pack di Lync Server 2010 è stato introdotto il concetto del monitoraggio della disponibilità degli scenari degli utenti finali con transazioni sintetiche. In Lync Server 2013 questi agenti dispongono di ulteriori transazioni sintetiche e possono essere eseguiti da una vasta gamma di posizioni all'interno dell'azienda, da sedi geografiche remote esterne, tramite Survivable Branch Appliance e distribuzioni di Lync Server 2010 per estendere la copertura, a distribuzioni di server perimetrali legacy.

  - **Log delle transazioni sintetiche.** Quando una transazione sintetica ha esito negativo, gli amministratori hanno accesso a log HTML utili per determinare cosa sia accaduto. Tra le informazioni fornite vi sono l'azione non riuscita, la latenza di ogni azione, la riga di comando utilizzata per eseguire il test e l'errore verificatosi.

  - **Maggiore copertura per segnalare l'affidabilità delle chiamate.** Nel Management Pack di Lync Server 2010 è stata introdotta la segnalazione dell'affidabilità delle chiamate, che consente di rilevare seri problemi di connettività che incidono sulle chiamate audio degli utenti finali. I Management Pack di Lync Server 2013 aggiungono copertura per la messaggistica istantanea peer-to-peer e altre funzionalità di conferenza di base per ottimizzare la copertura e ridurre i disturbi.

  - **Monitoraggio delle dipendenze.** Gli scenari di Lync Server possono avere esito negativo per diversi fattori esterni come IIS offline, CPU e risorse di memoria limitate o problemi del disco. I nuovi Management Pack verificano diverse dipendenze critiche in modo che gli amministratori siano consapevoli del relativo impatto.

  - **Miglioramento dei report.** È disponibile una serie di report che consentono agli amministratori di stimare la disponibilità degli scenari, pianificare la capacità e controllare i componenti su cui si verifica la maggior parte dei problemi.

Nei Management Pack è inoltre inclusa una serie di funzionalità che consentono di rilevare e diagnosticare eventuali problemi, dando visibilità in tempo reale sullo stato della distribuzione di Lync Server. Queste funzionalità sono elencate nella tabella riportata di seguito.

### Funzionalità dei Management Pack

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Transazioni sintetiche</p></td>
<td><p>Cmdlet di Windows PowerShell che possono essere eseguiti da diverse posizioni per verificare che gli scenari degli utenti finali, ad esempio per l'accesso, la presenza, la messaggistica istantanea e le conferenze, siano prontamente disponibili per gli utenti finali.</p></td>
</tr>
<tr class="even">
<td><p>Avvisi di affidabilità delle chiamate</p></td>
<td><p>Query di database per le registrazioni dettagli chiamata. Tali registrazioni vengono scritte dai Front End Server per indicare se gli utenti finali sono riusciti a connettersi a una chiamata o il motivo per cui una chiamata si è interrotta. Queste query generano avvisi che segnalano quando un numero elevato di utenti finali ha problemi di connettività per chiamate peer-to-peer o funzionalità di conferenza di base.</p></td>
</tr>
<tr class="odd">
<td><p>Avvisi sulla qualità multimediale</p></td>
<td><p>Query di database che esaminano i report sulla qualità percepita dagli utenti (QoE) pubblicati dai client alla fine di ogni chiamata. Queste query generano avvisi che segnalano gli scenari in cui è probabile che gli utenti percepiscano una scarsa qualità multimediale durante le chiamate e le conferenze. I dati si basano su metriche chiave, come la latenza e la perdita di pacchetti, che notoriamente contribuiscono in modo diretto alla qualità delle chiamate.</p></td>
</tr>
<tr class="even">
<td><p>Stato dei componenti</p></td>
<td><p>I singoli componenti server generano avvisi mediante log eventi e contatori delle prestazioni. Questi avvisi indicano le condizioni di errore che possono influire in modo significativo su uno o più scenari degli utenti finali. Questi avvisi inoltre indicano diverse altre condizioni di errore, tra cui i servizi non in esecuzione, alte percentuali di problemi, un'elevata latenza dei messaggi o i problemi di connettività.</p></td>
</tr>
<tr class="odd">
<td><p>Stato delle dipendenze</p></td>
<td><p>I problemi possono essere causati da una vasta gamma di motivi esterni. I Management Pack ora eseguono il monitoraggio e raccolgono dati per alcune delle dipendenze esterne più importanti che possono indicare seri problemi, inclusi la disponibilità di IIS, l'utilizzo di CPU e memoria dei server e dei processi e le metriche del disco.</p></td>
</tr>
</tbody>
</table>


Gli avvisi generati dal sistema sono stati classificati in tre categorie generali:

  - **Avvisi di alta priorità.** Questi avvisi indicano le condizioni che causeranno interruzioni dei servizi per gruppi estesi di utenti. Un guasto di un componente in un singolo computer ad esempio non costituisce un avviso di alta priorità perché Lync Server 2013 ha funzionalità di disponibilità elevata incorporate. Gli avvisi di alta priorità rappresentano invece problemi sufficientemente gravi da richiedere l'attenzione degli amministratori anche in piena notte. I problemi rilevati dalle transazioni sintetiche e i servizi offline, ad esempio per conferenze audio/video, sono considerati avvisi di alta priorità.

  - **Avvisi di media priorità.**. Questi avvisi indicano le condizioni che incidono su un sottoinsieme di utenti o segnalano un degrado della qualità delle chiamate. Sono inclusi problemi quali guasti dei componenti, latenza per stabilire una chiamata o un peggioramento della qualità audio durante una chiamata. Gli avvisi di questa categoria sono con stato e indicano lo stato corrente del problema. Si supponga ad esempio che i tempi per stabilire una chiamata superino la soglia di avviso. Se questi tempi tornano normali, tali avvisi vengono risolti automaticamente in System Center Operations Manager. È prevedibile che un amministratore esamini tali avvisi nello stesso giorno lavorativo.

  - **Altri avvisi.** Sono avvisi di componenti che possono incidere su un utente o un sottoinsieme specifico di utenti. Ad esempio, il servizio Rubrica non riesce ad analizzare la voce di Active Directory di un determinato utente. È prevedibile che gli amministratori si occupino di tali avvisi quando hanno tempo a disposizione.

## Contenuto della sezione

  - [Configurazione di Lync Server per l'utilizzo con System Center Operations Manager](lync-server-2013-configuring-lync-server-to-work-with-system-center-operations-manager.md)

  - [Utilizzo della registrazione dettagliata per le transazioni sintetiche](lync-server-2013-using-rich-logging-for-synthetic-transactions.md)

  - [Utilizzo di Microsoft SQL Server 2008 R2 come database di System Center Operations Manager](lync-server-2013-using-microsoft-sql-server-2008-r2-as-your-system-center-operations-manager-database.md)

