---
title: 'Lync Server 2013: Rapporto attività utente'
TOCTitle: Rapporto attività utente
ms:assetid: 3aa6fef2-ea02-4f0f-93e8-fa2e0a953d79
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558638(v=OCS.15)
ms:contentKeyID: 49300257
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rapporto attività utente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nel Rapporto attività utente viene fornito un elenco dettagliato delle sessioni peer-to-peer e di conferenza per ogni utente in riferimento a un periodo di tempo specifico. Diversamente da molti rapporti di monitoraggio, il Rapporto attività utente associa ogni chiamata al singolo utente. Ad esempio le sessioni peer-to-peer specificano gli URI SIP della persona che ha effettuato la chiamata (Da utente) e della persona che ha ricevuto la chiamata (A utente). Se si espandono le informazioni relative a una conferenza, è possibile visualizzare un elenco di tutti i partecipanti con l'indicazione del ruolo che hanno svolto nella conferenza.

Spesso si fa riferimento al Rapporto attività utente come al rapporto "help desk", in quanto il rapporto viene spesso utilizzato dal personale dell'help desk per recuperare informazioni sulla sessione per un utente specifico. È possibile applicare un filtro in base alle chiamate effettuate o ricevute da un singolo utente semplicemente digitando l'URI SIP dell'utente nella casella Prefisso URI utente.

Se si effettua questa operazione, il Rapporto attività utente restituirà le informazioni relative a ogni utente con un URI SIP che inizia con la stringa specificata. Se ad esempio si digita **ken** nella casella URI, il Rapporto attività utente troverà **Ken** .Myer@litwareinc.com, ma rileverà anche gli utenti seguenti:

  - **ken** azi@litwareinc.com

  - **ken** burg@litwareinc.com

  - **Ken** .Sanchez@litwareinc.com

  - **Ken** nedy@litwareinc.com

Per assicurare che vengano restituite solo le informazioni per Ken Myer, digitare l'URI completo (Ken.Myer@litwareinc.com) nella casella di ricerca o almeno una parte dell'URI di Ken che permetta di distinguerlo in modo univoco dagli altri utenti nell'organizzazione. Ad esempio:

Ken.my

## Per accedere al Rapporto attività utente

È possibile accedere al Rapporto attività utente dalla home page di Relazioni monitoraggio ma anche facendo clic sulla metrica URI utente nel [Rapporto inventario telefoni IP in Lync Server 2013](lync-server-2013-ip-phone-inventory-report.md). Facendo clic sull'URI conferenza (di una conferenza specifica) dal Rapporto attività utente, viene visualizzato il Rapporto Dettagli conferenza. Analogamente, facendo clic sulla metrica Dettaglio per una chiamata peer-to-peer, viene visualizzato il [Rapporto Dettagli sessione peer-to-peer in Lync Server 2013](lync-server-2013-peer-to-peer-session-detail-report.md).

## Utilizzo ottimale del Rapporto attività utente

Il Rapporto attività utente include molte informazioni utili che talvolta risulta difficile trovare. Sono ad esempio incluse tutte le attività utente che vengono eseguite nell'organizzazione in un periodo di tempo specifico. Ciò significa che all'interno del rapporto sono presenti anche informazioni sugli utenti che hanno in qualche modo utilizzato Microsoft Lync Server 2013.


> [!WARNING]
> Tecnicamente è possibile che parte dell'attività utente non venga registrata: anche se Lync Server cerca di memorizzare le informazioni su tutte le chiamate telefoniche, può accadere che le informazioni di una chiamata non vengano memorizzate nel database. Lync Server è stato progettato per dare una visione estremamente accurata ma non necessariamente perfetta delle attività che vengono svolte in Lync Server 2013. Il fatto che non esiste alcuna garanzia che venga registrato il 100% di tutte le chiamate spiega il motivo per cui il monitoraggio di Lync Server non possa essere utilizzato come sistema di fatturazione.<BR>Un altro limite consiste nel fatto che il numero massimo di record visualizzabile in un rapporto di Relazioni monitoraggio è 1.000. Ciò significa che, a seconda della quantità di attività utente svolta e del periodo di tempo di riferimento, la query potrebbe non restituire tutti i dati effettivamente memorizzati nel database.



  - Quali utenti hanno effettivamente usato il sistema in questo periodo di tempo?

  - Qual è stato l'utente più attivo in questo periodo di tempo?

  - Gli utenti che effettuano il numero maggiore di chiamate telefoniche sono anche quelli che partecipano alla maggior parte di sessioni di messaggistica istantanea?

Per rispondere a domande come queste, è possibile esportare i dati recuperati dai rapporti di monitoraggio in un foglio di calcolo di Excel. Successivamente si può utilizzare questo foglio di calcolo e/o un file di valori separati da virgole per analizzare i dati in modo analogo al Rapporto attività utenti. Si supponga ad esempio di avere esportato i dati di rapporto in Excel, quindi in un file di valori separati da virgole. A quel punto è possibile importare i dati dal file con estensione CSV in Windows PowerShell utilizzando un comando simile al seguente:

    $x = Import-Csv -Path "C:\Data\User_Activity_Report.csv"

Dopo che i dati sono stati importati, è possibile utilizzare comandi di Windows PowerShell per trovare risposta alle proprie domande. Il comando seguente, ad esempio, restituisce un elenco di utenti univoci che in almeno una sessione sono stati gli utenti di "Da utente":

    $x | Group-Object "From user" | Select Name | Sort-Object Name

In altri termini:

    Name
    ----
    David.Ahs@litwareinc.com
    Gilead.Amosnino@litwareinc.com
    Henrik.Jensen@litwareinc.com
    Ken.Myer@litwareinc.com
    Pilar.Ackerman@litwareinc.com

Questo comando elenca gli utenti univoci in base al numero totale di sessioni a cui hanno partecipato:

    $x | Group-Object "From user" | Select Count, Name | Sort-Object Count -Descending

Restituisce dati simili ai seguenti:

    Count    Name
    -----    ----
      523    Ken.Myer@litwareinc.com
       63    David.Ahs@litwareinc.com
       29    Pilar.Ackerman@litwareinc.com
       17    Gilead.Amosnino@litwareinc.com
       10    Henrik.Jensen@litwareinc.com

Questo comando limita le sessioni incluse nel rapporto a quelle che includevano l'audio come modalità:

    $x | Where-Object {$_.Modalities -match "audio"} | Group-Object "From user" | Select Count, Name | Sort-Object Count -Descending

Posizionando il mouse su un ID diagnostica mostrato nel rapporto, viene visualizzata una descrizione comando che descrive l'ID.

## Filtri

I filtri consentono di restituire un insieme di dati più circoscritto o di visualizzare in modi diversi i dati restituiti. Il Rapporto attività utente ad esempio consente di filtrare i dati restituiti in base a fattori come il tipo di attività, ovvero sessioni peer-to-peer o di conferenza, oppure in base all'indirizzo SIP dell'utente in modo da visualizzare le attività per un solo utente. È inoltre possibile scegliere come raggruppare i dati. In questo caso, gli utilizzi vengono raggruppati per ora, giorno, settimana o mese.

Nella tabella riportata di seguito vengono elencati i filtri che è possibile utilizzare con il Rapporto attività utente.

### Filtri per il Rapporto attività utente

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Da</strong></p></td>
<td><p>Data/ora di inizio dell'intervallo di tempo. Per visualizzare i dati in base all'ora, immettere sia la data che l'ora di inizio come indicato di seguito:</p>
<p>7/17/2012 1:00 PM</p>
<p>Se non si specifica l'ora di inizio, il rapporto inizia automaticamente alla mezzanotte del giorno specificato. Per visualizzare i dati in base al giorno, immettere solo la data:</p>
<p>7/17/2012</p>
<p>Per visualizzare i dati in base alla settimana o al mese, immettere una data che rientra nella settimana o nel mese in base a cui deve essere effettuata la visualizzazione. Non è necessario immettere il primo giorno della settimana o del mese:</p>
<p>7/13/2012</p>
<p>Le settimane vengono calcolate sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="even">
<td><p><strong>A</strong></p></td>
<td><p>Data/ora di fine dell'intervallo di tempo. Per visualizzare i dati in base all'ora, immettere sia la data che l'ora di fine come indicato di seguito:</p>
<p>7/17/2012 1:00 PM</p>
<p>Se non si specifica l'ora di fine, il rapporto termina automaticamente alla mezzanotte del giorno specificato. Per visualizzare i dati in base al giorno, immettere solo la data:</p>
<p>7/17/2012</p>
<p>Per visualizzare i dati in base alla settimana o al mese, immettere una data che rientra nella settimana o nel mese in base a cui deve essere effettuata la visualizzazione. Non è necessario immettere il primo giorno della settimana o del mese:</p>
<p>7/13/2012</p>
<p>Le settimane vengono calcolate sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Tipo di attività</strong></p></td>
<td><p>Tipo di attività. Selezionare uno dei valori seguenti:</p>
<ul>
<li><p>[Tutto]</p></li>
<li><p>Peer-to-peer</p></li>
<li><p>Conferenza</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Modalità</strong></p></td>
<td><p>La modalità disponibile dipende dal tipo di attività selezionato. Se il tipo di attività è Peer-to-peer, è possibile selezionare come modalità Messaggistica istantanea, Trasferimento di file, Condivisione applicazioni, Voce o Video.</p>
<p>Se il tipo di attività è Conferenza, è possibile selezionare Messaggistica istantanea, Telefono, Conferenza Web, Condivisione applicazioni, Voce/Video o Telefonia.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Categoria sessione</strong></p></td>
<td><p>Indica l'esito dell'attività in questione. Selezionare uno dei valori seguenti:</p>
<ul>
<li><p>[Tutto]</p></li>
<li><p>Esito positivo</p></li>
<li><p>Errore previsto</p></li>
<li><p>Errore imprevisto</p></li>
</ul>
<p>Per &quot;errore previsto&quot; si intende un errore che si prevede si verificherà. Se ad esempio un utente ha impostato il proprio stato su Non disturbare, è previsto che le chiamate effettuate per tale utente abbiano esito negativo. Per &quot;errore imprevisto&quot; si intende un errore che si verifica in un sistema considerato integro. Una chiamata ad esempio non dovrebbe interrompersi quando il chiamante viene messo in attesa. Se la chiamata si interrompe, l'evento verrà contrassegnato come errore imprevisto.</p></td>
</tr>
<tr class="even">
<td><p><strong>Prefisso URI utente</strong></p></td>
<td><p>Indirizzo SIP dell'utente. Per visualizzare solo i record relativi all'utente Ken Myer, è necessario immettere l'indirizzo SIP di Ken Myer, ad esempio:</p>
<p>sip:davidegarghentini@litwareinc.com</p></td>
</tr>
</tbody>
</table>


## Metrica per le sessioni peer-to-peer

Nella tabella riportata di seguito vengono elencate le informazioni fornite nel Rapporto attività utente per le sessioni peer-to-peer, ovvero le sessioni che coinvolgono solo due partecipanti.

### Metrica per le sessioni peer-to-peer

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Elemento utilizzabile per eseguire l'ordinamento?</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Dettagli</strong></p></td>
<td><p>No</p></td>
<td><p>Quando si fa clic su questo elemento, nel rapporto viene mostrato il Rapporto Dettagli sessione peer-to-peer per la sessione selezionata.</p></td>
</tr>
<tr class="even">
<td><p><strong>Da utente</strong></p></td>
<td><p>Sì</p></td>
<td><p>Indirizzo SIP dell'utente che ha avviato la sessione peer-to-peer.</p></td>
</tr>
<tr class="odd">
<td><p><strong>A utente</strong></p></td>
<td><p>Sì</p></td>
<td><p>Indirizzo SIP dell'utente che ha partecipato alla sessione peer-to-peer.</p></td>
</tr>
<tr class="even">
<td><p><strong>Modalità</strong></p></td>
<td><p>Sì</p></td>
<td><p>Tipo di comunicazione utilizzato nella sessione, ad esempio messaggistica istantanea, audio o trasferimento file.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Ora invito</strong></p></td>
<td><p>Sì</p></td>
<td><p>Data e ora di invio dell'invito iniziale a partecipare alla sessione peer-to-peer.</p></td>
</tr>
<tr class="even">
<td><p><strong>Ora risposta</strong></p></td>
<td><p>Sì</p></td>
<td><p>Data a ora in cui l'utente invitato ha accettato l'invito per la sessione.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Ora fine</strong></p></td>
<td><p>Sì</p></td>
<td><p>Data e ora di fine della sessione peer-to-peer.</p></td>
</tr>
<tr class="even">
<td><p><strong>ID diagnostica</strong></p></td>
<td><p>Sì</p></td>
<td><p>Identificatore univoco nel formato di un'intestazione ms-diagnostics associato a un messaggio SIP in cui spesso vengono fornite informazioni utili per la risoluzione dei problemi. Le intestazioni di diagnostica sono facoltative (è possibile che in alcune sessioni SIP non siano incluse queste intestazioni) e gli ID diagnostica sono spesso indicati solo per sessioni in cui si sono verificati problemi di un determinato tipo.</p></td>
</tr>
</tbody>
</table>


## Metrica per le sessioni di conferenza

Nella tabella riportata di seguito vengono elencate le informazioni fornite nel Rapporto attività utente per le sessioni di conferenza, ovvero le sessioni che coinvolgono tre o più partecipanti.

### Metrica per le sessioni di conferenza

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Elemento utilizzabile per eseguire l'ordinamento?</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>URI conferenza</strong></p></td>
<td><p>Sì</p></td>
<td><p>Identificatore di conferenza univoco. Quando si fa clic su questo elemento, nel rapporto viene mostrato il Rapporto Dettagli conferenza per la sessione selezionata. Quando si espande questo elemento, nel rapporto vengono mostrate le informazioni sui partecipanti della conferenza. Per informazioni, vedere la sezione &quot;Metrica per i partecipanti di una conferenza&quot; più avanti in questo argomento.</p></td>
</tr>
<tr class="even">
<td><p><strong>Organizzatore</strong></p></td>
<td><p>Sì</p></td>
<td><p>Indirizzo SIP dell'utente che ha organizzato la conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Pool</strong></p></td>
<td><p>Sì</p></td>
<td><p>Nome dell'eventuale server perimetrale utilizzato nella conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>Ora inizio</strong></p></td>
<td><p>Sì</p></td>
<td><p>Data e ora di inizio della conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Ora fine</strong></p></td>
<td><p>Sì</p></td>
<td><p>Data e ora di fine della conferenza.</p></td>
</tr>
</tbody>
</table>


## Metrica per i partecipanti di una conferenza

Nella tabella riportata di seguito vengono elencate le informazioni fornite nel Rapporto attività utente per ogni partecipante di una conferenza.

### Metrica per i partecipanti di una conferenza

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Elemento utilizzabile per eseguire l'ordinamento?</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Ruolo</strong></p></td>
<td><p>No</p></td>
<td><p>Ruolo dell'utente nella conferenza, ad esempio Relatore.</p></td>
</tr>
<tr class="even">
<td><p><strong>Partecipante</strong></p></td>
<td><p>No</p></td>
<td><p>Indirizzo SIP dell'utente.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Connettività</strong></p></td>
<td><p>No</p></td>
<td><p>Tipo di connessione di rete, ad esempio &quot;Dall'interno&quot; per una connessione interna o &quot;Da PSTN&quot; per gli utenti connessi tramite chiamata in ingresso.</p></td>
</tr>
<tr class="even">
<td><p><strong>Ora partecipazione</strong></p></td>
<td><p>No</p></td>
<td><p>Data e ora in cui l'utente ha partecipato alla conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Ora uscita</strong></p></td>
<td><p>No</p></td>
<td><p>Data e ora in cui l'utente è uscito dalla conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>ID diagnostica</strong></p></td>
<td><p>No</p></td>
<td><p>Identificatore univoco nel formato di un'intestazione ms-diagnostics associato a un messaggio SIP in cui spesso vengono fornite informazioni utili per la risoluzione dei problemi. Le intestazioni di diagnostica sono facoltative (è possibile che in alcune sessioni SIP non siano incluse queste intestazioni) e gli ID diagnostica sono spesso indicati solo per sessioni in cui si sono verificati problemi di un determinato tipo.</p></td>
</tr>
</tbody>
</table>

