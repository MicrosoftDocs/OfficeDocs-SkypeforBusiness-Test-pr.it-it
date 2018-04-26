---
title: 'Lync Server 2013: Rapporto di messaggistica istantanea peer-to-peer'
TOCTitle: Rapporto di messaggistica istantanea peer-to-peer
ms:assetid: 19ec0145-2398-437b-8989-f780c179b798
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558620(v=OCS.15)
ms:contentKeyID: 49299836
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rapporto di messaggistica istantanea peer-to-peer in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nel rapporto di messaggistica istantanea peer-to-peer vengono fornite informazioni sulla tendenza delle sessioni di messaggistica istantanea suddivise per pool e per tipo di autenticazione. Il rapporto può inoltre indicare il numero totale di sessioni organizzate oppure segnalare il numero complessivo di messaggi istantanei inviati nel periodo specificato (ad esempio, Giorno o Ora).

## Accesso al rapporto di messaggistica istantanea peer-to-peer

È possibile accedere al rapporto di messaggistica istantanea peer-to-peer solo facendo clic su una delle metriche riportate di seguito nel [Rapporto riepilogativo attività peer-to-peer in Lync Server 2013](lync-server-2013-peer-to-peer-activity-summary-report.md):

  - Totale sessioni di messaggistica istantanea peer-to-peer

  - Totale messaggi istantanei peer-to-peer

## Utilizzo ottimale del rapporto di messaggistica istantanea peer-to-peer

Nel rapporto di messaggistica istantanea peer-to-peer vengono mostrati, per impostazione predefinita, il numero di messaggi per ora (o giorno, a seconda dell'impostazione configurata). Tuttavia, è anche possibile scegliere di visualizzare il giorno in base alle sessioni per ora. In tal caso, fare clic su **Nascondi/mostra parametri** nell'angolo superiore destro della finestra relativa ai rapporti e quindi fare clic su **Numero di sessioni** nell'elenco **Rapporto di** .

## Filtri

I filtri consentono di ottenere un set di dati più mirato o di visualizzare i dati restituiti in diversi modi. Nella tabella seguente sono riportati i filtri utilizzabili con il rapporto di messaggistica istantanea peer-to-peer.

### Filtri per il rapporto di messaggistica istantanea peer-to-peer

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
<td><p>Data e ora di inizio per l'intervallo di tempo. Per visualizzare i dati in base all'ora, inserire sia la data che l'ora di inizio come segue:</p>
<p>7/7/2012 1:00 PM</p>
<p>Se non si specifica l'ora di inizio, il rapporto inizia automaticamente alla 12:00 AM del giorno specificato. Per visualizzare i dati in base al giorno, immettere solo la data:</p>
<p>7/7/2012</p>
<p>Per visualizzare i dati in base alla settimana o al mese, immettere una data che rientri nella settimana o nel mese desiderato (non è necessario immettere il primo giorno della settimana o del mese):</p>
<p>7/3/2012</p>
<p>Le settimane vengono calcolate sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="even">
<td><p><strong>A</strong></p></td>
<td><p>Data e ora di fine per l'intervallo di tempo. Per visualizzare i dati in base all'ora, inserire sia la data che l'ora di fine come segue:</p>
<p>7/7/2012 1:00 PM</p>
<p>Se non si specifica l'ora di fine, il rapporto termina automaticamente alla 12:00 AM del giorno specificato. Per visualizzare i dati in base al giorno, immettere solo la data:</p>
<p>7/7/2012</p>
<p>Per visualizzare i dati in base alla settimana o al mese, immettere una data che rientra nella settimana o nel mese in base a cui deve essere effettuata la visualizzazione. Non è necessario immettere il primo giorno della settimana o del mese:</p>
<p>7/3/2012</p>
<p>Le settimane vengono calcolate sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Intervallo</strong></p></td>
<td><p>Intervallo di tempo. Selezionare una delle opzioni seguenti:</p>
<ul>
<li><p>Orario (è possibile visualizzare un massimo di 25 ore)</p></li>
<li><p>Giornaliero (è possibile visualizzare un massimo di 31 giorni)</p></li>
<li><p>Settimanale (è possibile visualizzare un massimo di 12 settimane)</p></li>
<li><p>Mensile (è possibile visualizzare un massimo di 12 mesi)</p></li>
</ul>
<p>Se le date di inizio e di fine superano il numero massimo di valori consentiti per l'intervallo selezionato, verrà visualizzato solo il numero massimo di valori, a partire dalla data di inizio. Se ad esempio si seleziona l'intervallo Giornaliero con 07/07/2012 come data di inizio e 2/28/2012 come data di fine, verranno visualizzati i dati dalla 8/7/2012 12:00 AM alla 9/7/2012 12:00 AM, ovvero i dati per un totale di 31 giorni.</p></td>
</tr>
<tr class="even">
<td><p><strong>Rapporto di</strong></p></td>
<td><p>Indica i valori da utilizzare nel rapporto. Selezionare una delle opzioni seguenti:</p>
<ul>
<li><p>Numero di sessioni</p></li>
<li><p>Numero messaggi</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Metrica del rapporto di messaggistica istantanea peer-to-peer in base al pool

Nella tabella seguente vengono riportate le informazioni fornite nel rapporto di messaggistica istantanea peer-to-peer.

### Metrica del rapporto di messaggistica istantanea peer-to-peer in base al pool

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
<td><p><strong>Pool</strong></p></td>
<td><p>No</p></td>
<td><p>Nome del pool di registrazione o del server perimetrale.</p></td>
</tr>
<tr class="even">
<td><p><strong>Data/Ora</strong></p></td>
<td><p>No</p></td>
<td><p>Data e ora in cui hanno avuto luogo le sessioni.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Totale</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni o di messaggi.</p></td>
</tr>
</tbody>
</table>


## Metrica delle sessioni di messaggistica istantanea peer-to-peer in base al tipo di autenticazione

Nella tabella seguente vengono riportate le informazioni fornite nel rapporto di messaggistica istantanea peer-to-peer per ogni tipo di autenticazione utilizzato dai partecipanti a una sessione peer-to-peer.

### Metrica delle sessioni di messaggistica istantanea peer-to-peer in base al tipo di autenticazione

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
<td><p><strong>Tipo di autenticazione</strong></p></td>
<td><p>No</p></td>
<td><p>Tipo di autenticazione utilizzato dai partecipanti alla sessione. I valori validi in genere sono i seguenti:</p>
<ul>
<li><p>Enterprise</p></li>
<li><p>Federato</p></li>
<li><p>PIC</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Data/Ora</strong></p></td>
<td><p>No</p></td>
<td><p>Data e ora in cui hanno avuto luogo le sessioni.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Totale</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni o di messaggi.</p></td>
</tr>
</tbody>
</table>

