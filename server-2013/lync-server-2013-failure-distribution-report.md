---
title: 'Lync Server 2013: Rapporto distribuzione errori'
TOCTitle: Rapporto distribuzione errori
ms:assetid: 365c7beb-24d4-40f5-92e7-4978b9688916
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558635(v=OCS.15)
ms:contentKeyID: 49300161
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rapporto distribuzione errori in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il Rapporto distribuzione errori classifica le sessioni non riuscite nelle categorie seguenti:

  - Motivi diagnostica principali

  - Modalità principali

  - Pool principali

  - Origini principali

  - Componenti principali

  - Utenti di origine principali

  - Utenti di destinazione principali

  - Agenti utenti di origine principali

Queste categorie possono essere utilizzate per localizzare con precisione il problema e, in alcuni casi, stabilirne la causa. Si supponga ad esempio di aver registrato 242 sessioni audio/video non riuscite in un giorno specifico. Analizzando il Rapporto distribuzione errori, si può riscontrare che 237 di queste sessioni non riuscite hanno avuto luogo nel pool Dublin. Questa informazione rappresenta un punto di partenza valido nell'individuazione e nella diagnosi delle cause che sono alla base degli errori. Facendo clic sul pool Dublin nella categoria **Pool principali** , verrà visualizzato un Rapporto distribuzione errori per il pool specifico. A questo punto è possibile iniziare ad analizzare le cause dei problemi che hanno interessato il pool Dublin.

## Visualizzazione del Rapporto distribuzione errori

È possibile accedere al Rapporto distribuzione errori da uno qualsiasi dei rapporti seguenti facendo clic sulla metrica **Errore previsto** o **Errore imprevisto** :

  - [Rapporto errori principali in Lync Server 2013](lync-server-2013-top-failures-report.md)

  - [Rapporto di diagnostica conferenze in Lync Server 2013](lync-server-2013-conference-diagnostic-report.md)

  - [Rapporto di diagnostica attività peer-to-peer in Lync Server 2013](lync-server-2013-peer-to-peer-activity-diagnostic-report.md)

Dal Rapporto distribuzione errori è possibile fare clic su una delle metriche seguenti per visualizzare il [Rapporto Elenco errori in Lync Server 2013](lync-server-2013-failure-list-report.md):

  - Motivi diagnostica principali (sessioni)

  - Modalità principali (sessioni)

  - Pool principali (sessioni)

  - Origini principali (sessioni)

  - Componenti principali (sessioni)

  - Utenti di origine principali (sessioni)

  - Utenti di destinazione principali (sessioni)

  - Agenti utenti di origine principali (sessioni)

## Uso del Rapporto distribuzione errori

A seconda delle dimensioni del monitor e della risoluzione dello schermo, è possibile che alcuni dei dati mostrati nel Rapporto distribuzione errori vengano troncati quando vengono visualizzati. Ciò accade soprattutto nel caso di metriche come gli agenti utente che possono avere etichette particolarmente lunghe. Ad esempio un agente utente con un nome come "UCCAPI/4.0.7400.0 OC/4.0.7400.0 (Microsoft Lync 2013)" può essere visualizzato solo parzialmente:

UCCAPI/4.0.7400.0 OC/4.0.7400.0 (Microsoft Ly...

Fortunatamente, è possibile visualizzare l'intera etichetta semplicemente posizionando il mouse sul valore troncato.

Una metrica interessante in base alla quale è possibile filtrare usando il Rapporto distribuzione errori è ID diagnostica. Se lo stesso valore di ID diagnostica viene fuori in altri rapporti, è possibile applicare il filtro in base all'ID nel Rapporto distribuzione errori e ottenere informazioni estremamente dettagliate su dove e con che frequenza l'ID è stato segnalato durante una sessione non riuscita.

## Filtri

I filtri consentono di restituire un insieme di dati più circoscritto o di visualizzare in modi diversi i dati restituiti. Il Rapporto distribuzione errori ad esempio consente di applicare filtri in base a elementi come il tipo di attività (sessione peer-to-peer o di conferenza) o l'ID diagnostica associato a ogni sessione non riuscita.

Nella tabella riportata di seguito vengono elencati i filtri che è possibile utilizzare con il Rapporto distribuzione errori.

### Filtri del Rapporto distribuzione errori

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
<p>7/7/2012 1:00 PM</p>
<p>Se non si specifica l'ora di inizio, il rapporto inizia automaticamente alla mezzanotte del giorno specificato. Per visualizzare i dati in base al giorno, immettere solo la data:</p>
<p>7/7/12</p>
<p>Per visualizzare i dati in base alla settimana o al mese, immettere una data che rientra nella settimana o nel mese in base a cui deve essere effettuata la visualizzazione. Non è necessario immettere il primo giorno della settimana o del mese:</p>
<p>3/7/12</p>
<p>Le settimane vengono calcolate sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="even">
<td><p><strong>A</strong></p></td>
<td><p>Data/ora di fine dell'intervallo di tempo. Per visualizzare i dati in base all'ora, immettere sia la data che l'ora di fine come indicato di seguito:</p>
<p>7/7/2012 1:00 PM</p>
<p>Se non si specifica l'ora di fine, il rapporto termina automaticamente alla mezzanotte del giorno specificato. Per visualizzare i dati in base al giorno, immettere solo la data:</p>
<p>7/7/12</p>
<p>Per visualizzare i dati in base alla settimana o al mese, immettere una data che rientra nella settimana o nel mese in base a cui deve essere effettuata la visualizzazione. Non è necessario immettere il primo giorno della settimana o del mese:</p>
<p>3/7/12</p>
<p>Le settimane vengono calcolate sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Pool</strong></p></td>
<td><p>Nome di dominio completo (FQDN) del pool di registrazione o del server perimetrale. È possibile selezionare un singolo pool o fare clic su <strong>[Tutto]</strong> per visualizzare i dati per tutti i pool. Questo elenco a discesa viene popolato automaticamente in base ai record del database.</p></td>
</tr>
<tr class="even">
<td><p><strong>Tipo di attività</strong></p></td>
<td><p>Tipo di attività in base al quale applicare il filtro. Selezionare uno dei valori seguenti:</p>
<ul>
<li><p>[Tutto]</p></li>
<li><p>Peer-to-peer</p></li>
<li><p>Conferenza</p></li>
</ul></td>
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
<td><p><strong>ID diagnostica</strong></p></td>
<td><p>Identificatore univoco nel formato di un'intestazione ms-diagnostics associato a un messaggio SIP in cui spesso vengono fornite informazioni utili per la risoluzione dei problemi. Le intestazioni di diagnostica sono facoltative (è possibile che in alcune sessioni SIP non siano incluse queste intestazioni) e gli ID diagnostica sono spesso indicati solo per sessioni in cui si sono verificati problemi di un determinato tipo.</p></td>
</tr>
</tbody>
</table>


## Metrica dei motivi di diagnostica principali

Nella tabella riportata di seguito vengono elencate le informazioni fornite nel Rapporto distribuzione errori in base all'ID diagnostica segnalato con maggiore frequenza.

### Metrica dei motivi di diagnostica principali

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
<td><p><strong>Classificazione</strong></p></td>
<td><p>No</p></td>
<td><p>Classificazione relativa di sessioni non riuscite in base agli ID diagnostica. L'ID diagnostica è un identificatore univoco nel formato di un'intestazione ms-diagnostics associato a un messaggio SIP in cui spesso vengono fornite informazioni utili per la risoluzione dei problemi.</p></td>
</tr>
<tr class="even">
<td><p><strong>Motivi diagnostica</strong></p></td>
<td><p>No</p></td>
<td><p>ID diagnostica generato in una sessione.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Sessioni</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni non riuscite in cui è stato generato l'ID diagnostica specificato.</p></td>
</tr>
</tbody>
</table>


## Metrica delle modalità principali

Nella tabella riportata di seguito vengono elencate le informazioni fornite nel Rapporto distribuzione errori in base alle modalità di sessione in cui si sono verificati più errori.

### Metrica delle modalità principali

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
<td><p><strong>Classificazione</strong></p></td>
<td><p>No</p></td>
<td><p>Classificazione relativa di sessioni non riuscite in base al tipo di sessione, ad esempio un trasferimento file peer-to-peer o di conferenza audio/video.</p></td>
</tr>
<tr class="even">
<td><p><strong>Modalità</strong></p></td>
<td><p>No</p></td>
<td><p>Tipo di sessione.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Sessioni</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni non riuscite con la modalità specificata.</p></td>
</tr>
</tbody>
</table>


## Metrica dei pool principali

Nella tabella riportata di seguito vengono elencate le informazioni fornite nel Rapporto distribuzione errori in base ai pool in cui si sono verificati più errori.

### Metrica dei pool principali

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
<td><p><strong>Classificazione</strong></p></td>
<td><p>No</p></td>
<td><p>Classificazione relativa di sessioni non riuscite in base al pool di registrazione o al pool di registrazione o al server perimetrale in cui è stata eseguita la sessione.</p></td>
</tr>
<tr class="even">
<td><p><strong>Pool</strong></p></td>
<td><p>No</p></td>
<td><p>Nome del pool di registrazione o del server perimetrale.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Sessioni</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni non riuscite per pool di registrazione o server perimetrale.</p></td>
</tr>
</tbody>
</table>


## Metrica delle origini principali

Nella tabella riportata di seguito vengono elencate le informazioni fornite nel Rapporto distribuzione errori in base ai computer in cui si sono verificati più errori.

### Metrica delle origini principali

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
<td><p><strong>Classificazione</strong></p></td>
<td><p>No</p></td>
<td><p>Classificazione relativa di sessioni non riuscite per computer.</p></td>
</tr>
<tr class="even">
<td><p><strong>Origini</strong></p></td>
<td><p>No</p></td>
<td><p>Nome del computer associato alla sessione non riuscita.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Sessioni</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni non riuscite per computer.</p></td>
</tr>
</tbody>
</table>


## Metrica dei componenti principali

Nella tabella riportata di seguito vengono elencate le informazioni fornite nel Rapporto distribuzione errori in base ai componenti di Microsoft Lync Server 2010 in cui si sono verificati più errori.

### Metrica dei componenti principali

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
<td><p><strong>Classificazione</strong></p></td>
<td><p>No</p></td>
<td><p>Classificazione relativa di sessioni non riuscite in base al componente di Lync Server 2010, ad esempio ExumRouting, GroupChat, MediationServer.</p></td>
</tr>
<tr class="even">
<td><p><strong>Componenti</strong></p></td>
<td><p>No</p></td>
<td><p>Nome del componente associato alla sessione non riuscita.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Sessioni</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni non riuscite per componente.</p></td>
</tr>
</tbody>
</table>


## Metrica degli utenti di origine delle chiamate

Nella tabella seguente vengono elencate le informazioni fornite nel Rapporto distribuzione errori in base agli utenti per cui si sono verificati più errori quando hanno tentato di chiamare un altro utente (utenti "Da").

### Metrica degli utenti di origine delle chiamate

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
<td><p><strong>Classificazione</strong></p></td>
<td><p>No</p></td>
<td><p>Classificazione relativa di sessioni non riuscite in base all'utente invitato a partecipare alla sessione.</p></td>
</tr>
<tr class="even">
<td><p><strong>Da utenti</strong></p></td>
<td><p>No</p></td>
<td><p>Indirizzo SIP dell'utente invitato a partecipare alla sessione.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Sessioni</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni non riuscite per utente.</p></td>
</tr>
</tbody>
</table>


## Metrica degli utenti destinatari delle chiamate

Nella tabella seguente vengono elencate le informazioni fornite nel Rapporto distribuzione errori in base agli utenti per cui si sono verificati più errori quando un altro utente ha tentato di chiamarli (utenti "A").


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
<td><p><strong>Classificazione</strong></p></td>
<td><p>No</p></td>
<td><p>Classificazione relativa di sessioni non riuscite in base all'utente che ha avviato la sessione.</p></td>
</tr>
<tr class="even">
<td><p><strong>A utenti</strong></p></td>
<td><p>No</p></td>
<td><p>Indirizzo SIP dell'utente che ha avviato la sessione.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Sessioni</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni non riuscite per utente.</p></td>
</tr>
</tbody>
</table>


## Metrica degli agenti utente

Nella tabella riportata di seguito vengono elencate le informazioni fornite nel Rapporto distribuzione errori in base al software endpoint in cui si sono verificati più errori.

### Metrica degli agenti utente

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
<td><p><strong>Classificazione</strong></p></td>
<td><p>No</p></td>
<td><p>Classificazione relativa di sessioni non riuscite in base all'agente utente (software) associato alla sessione, ad esempio RTCC/4.0.0.0 Routing in ingresso/4.0.0.0.</p></td>
</tr>
<tr class="even">
<td><p><strong>Da agenti utente</strong></p></td>
<td><p>No</p></td>
<td><p>Nome dell'agente utente coinvolto nella sessione non riuscita.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Sessioni</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni non riuscite per agente.</p></td>
</tr>
</tbody>
</table>

