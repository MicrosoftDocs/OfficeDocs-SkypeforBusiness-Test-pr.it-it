---
title: Rapporto Tempo di partecipazione alla conferenza
TOCTitle: Rapporto Tempo di partecipazione alla conferenza
ms:assetid: e64dc89a-25e4-4cb8-bcb1-51712e69ba5a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205344(v=OCS.15)
ms:contentKeyID: 49302288
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rapporto Tempo di partecipazione alla conferenza

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il rapporto Tempo di partecipazione alla conferenza consente di determinare il tempo richiesto agli utenti per partecipare a una conferenza. Nel rapporto viene visualizzato il tempo medio di partecipazione (in millisecondi) e sono inoltre disponibili informazioni suddivise che indicano il numero di utenti in grado di partecipare a una conferenza in massimo 2 secondi, il numero di utenti che hanno impiegato tra 2 e 5 secondi per partecipare e così via.

## Accesso al rapporto Tempo di partecipazione alla conferenza

È possibile accedere al rapporto Tempo di partecipazione alla conferenza dalla home page Relazioni monitoraggio.

## Filtri

I filtri consentono di restituire un set di dati più circoscritto o di visualizzare in modi diversi i dati restituiti. Nella tabella riportata di seguito vengono elencati i filtri che è possibile utilizzare con il rapporto Tempo di partecipazione alla conferenza.

### Filtri del rapporto Tempo di partecipazione alla conferenza

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
<td><p>Data/ora di inizio per l'intervallo di tempo. Per visualizzare i dati in base alle ore, inserire sia la data che l'ora di inizio come segue:</p>
<p>07/07/2012 13.00</p>
<p>Se non si immette una data di inizio, il rapporto inizia automaticamente alle 00.00 del giorno specificato. Per visualizzare i dati per giorno, immettere solo la data:</p>
<p>07/07/2012</p>
<p>Per visualizzare i dati per settimana o per mese, immettere una data inclusa nella settimana o nel mese che si desidera visualizzare (non è necessario immettere il primo giorno della settimana o del mese):</p>
<p>03/07/2012</p>
<p>Le settimane vanno sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="even">
<td><p><strong>A</strong></p></td>
<td><p>Data/ora di fine per l'intervallo di tempo. Per visualizzare i dati in base alle ore, inserire sia la data che l'ora di fine come segue:</p>
<p>07/07/2012 13.00</p>
<p>Se non si immette una data di fine, il rapporto finisce automaticamente alle 00.00 del giorno specificato. Per visualizzare i dati per giorno, immettere solo la data:</p>
<p>07/07/2012</p>
<p>Per visualizzare i dati per settimana o per mese, immettere una data inclusa nella settimana o nel mese che si desidera visualizzare (non è necessario immettere il primo giorno della settimana o del mese):</p>
<p>03/07/2012</p>
<p>Le settimane vanno sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Intervallo</strong></p></td>
<td><p>Intervallo di tempo. Selezionare uno dei seguenti:</p>
<ul>
<li><p>Orario (è possibile visualizzare un massimo di 25 ore)</p></li>
<li><p>Giornaliero (è possibile visualizzare un massimo di 31 giorni)</p></li>
<li><p>Settimanale (è possibile visualizzare un massimo di 12 settimane)</p></li>
<li><p>Mensile (è possibile visualizzare un massimo di 12 mesi)</p></li>
</ul>
<p>Se per le date di inizio e di fine si immette un numero di valori superiore al massimo consentito per l'intervallo selezionato, verrà visualizzato solo il numero massimo di valori (a partire dalla data di inizio). Se ad esempio si seleziona l'intervallo Giornaliero con la data di inizio 07/08/2012 e la data di fine 28/09/2012, verranno visualizzati i dati relativi ai giorni da 07/08/2012 alle 00.00 a 07/09/2012 alle 00.00, ovvero per un totale di 31 giorni.</p></td>
</tr>
<tr class="even">
<td><p><strong>Pool</strong></p></td>
<td><p>Nome di dominio completo (FQDN) del pool di registrazione o del server perimetrale. È possibile selezionare un singolo pool oppure fare clic su <strong>[Tutto]</strong> per visualizzare i dati di tutti i pool. Le voci disponibili in questo elenco a discesa vengono inserite automaticamente in base ai record presenti nel database.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Sessioni conferenza</strong></p></td>
<td><p>Tipo di sessione. I valori consentiti sono:</p>
<ul>
<li><p>[Tutto]</p></li>
<li><p>Sessioni Focus</p></li>
<li><p>Condivisione applicazioni</p></li>
<li><p>Conferenze audio/video</p></li>
</ul>
<p>Se si seleziona [Tutto], nella parte superiore del rapporto verrà visualizzato il tempo totale di partecipazione alla conferenza. Si noti che questi totali sono riferiti solo alle conferenze pianificate tramite Microsoft Exchange o Microsoft Outlook.</p></td>
</tr>
</tbody>
</table>


## Metriche

La tabella seguente elenca le informazioni disponibili nel rapporto Tempo di partecipazione alla conferenza.

### Metriche del rapporto Tempo di partecipazione alla conferenza

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Elemento in base a cui ordinare i dati?</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Data</strong></p>
<p>Il titolo effettivo di questa metrica varia in base all'intervallo selezionato.</p></td>
<td><p>No</p></td>
<td><p>Data e ora in cui ha avuto luogo la conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>Totale sessioni</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni, comprendente le sessioni con esito positivo, le sessioni con esito negativo (per errori sia previsti che imprevisti) e le sessioni senza categoria.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Media (ms)</strong></p></td>
<td><p>No</p></td>
<td><p>Quantità media di tempo (in millisecondi) impiegato dai partecipanti per partecipare alla conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>Sessioni &lt; 2 secondi, Volume</strong></p></td>
<td><p>No</p></td>
<td><p>Numero di partecipanti che sono riusciti a partecipare alla conferenza in meno di 2 secondi.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Sessioni &lt; 2 secondi, Percentuale</strong></p></td>
<td><p>No</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p><strong>Sessioni 2-5 secondi, Volume</strong></p></td>
<td><p>No</p></td>
<td><p>Numero di partecipanti che hanno impiegato da 2 a 5 secondi per partecipare alla conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Sessioni 2-5 secondi, Percentuale</strong></p></td>
<td><p>No</p></td>
<td><p>Percentuale del numero totale di partecipanti che hanno impiegato da 2 a 5 secondi per partecipare alla conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>Sessioni 5-10 secondi, Volume</strong></p></td>
<td><p>No</p></td>
<td><p>Numero di partecipanti che hanno impiegato da 5 a 10 secondi per partecipare alla conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Sessioni 5-10 secondi, Percentuale</strong></p></td>
<td><p>No</p></td>
<td><p>Percentuale del numero totale di partecipanti che hanno impiegato da 5 a 10 secondi per partecipare alla conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>Sessioni &gt; 10 secondi, Volume</strong></p></td>
<td><p>No</p></td>
<td><p>Numero di partecipanti che hanno impiegato più di 10 secondi per partecipare alla conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Sessioni &gt; 10 secondi, Percentuale</strong></p></td>
<td><p>No</p></td>
<td><p>Percentuale del numero totale di partecipanti che hanno impiegato più di 10 secondi per partecipare alla conferenza.</p></td>
</tr>
</tbody>
</table>

