---
title: Sottoreport riepilogativo P2P
TOCTitle: Sottoreport riepilogativo P2P
ms:assetid: fc36185a-3cc5-4167-8c93-8a755fa75ac7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205416(v=OCS.15)
ms:contentKeyID: 49302569
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Sottoreport riepilogativo P2P

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nel sottoreport riepilogativo P2P viene fornita una panoramica delle sessioni di comunicazione peer-to-peer non riuscite.

## Filtri

I filtri consentono di restituire un insieme di dati più circoscritto o di visualizzare in modi diversi i dati restituiti. Nella tabella riportata di seguito vengono elencati i filtri che è possibile utilizzare con il sottoreport riepilogativo P2P.

### Filtri del sottoreport riepilogativo P2P

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
<p>7/7/2012 13.00</p>
<p>Se non si immette una data/ora di inizio, il rapporto inizia automaticamente alle 00.00 del giorno specificato. Per visualizzare i dati in base al giorno, immettere solo la data:</p>
<p>7/7/2012</p>
<p>Per visualizzare i dati per settimana o mese, immettere una data inclusa nella settimana o nel mese che si desidera visualizzare (non è necessario immettere il primo giorno della settimana o del mese):</p>
<p>3/7/2012</p>
<p>Le settimane vanno sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="even">
<td><p><strong>A</strong></p></td>
<td><p>Data e ora di fine per l'intervallo di tempo. Per visualizzare i dati in base all'ora, inserire sia la data che l'ora di fine come segue:</p>
<p>7/7/2012 13.00</p>
<p>Se non si immette una data/ora di fine, il rapporto termina automaticamente alle 00.00 del giorno specificato. Per visualizzare i dati per giorno, immettere solo la data:</p>
<p>7/7/2012</p>
<p>Per visualizzare i dati per settimana o mese, immettere una data inclusa nella settimana o nel mese che si desidera visualizzare (non è necessario immettere il primo giorno della settimana o del mese):</p>
<p>3/7/2012</p>
<p>Le settimane vanno sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Pool</strong></p></td>
<td><p>Nome di dominio completo (FQDN) del pool di registrazione o del server perimetrale. È possibile selezionare un singolo pool o fare clic su <strong>[Tutto]</strong> per visualizzare i dati per tutti i pool. Questo elenco a discesa viene popolato automaticamente in base ai record del database.</p></td>
</tr>
</tbody>
</table>


## Metriche

Nella tabella seguente sono elencate le informazioni fornite nel sottoreport riepilogativo P2P.

### Metriche del sottoreport riepilogativo P2P

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
<td><p><strong>Totale sessioni</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni, comprendente le sessioni con esito positivo, le sessioni con esito negativo (per errori sia previsti che imprevisti) e le sessioni senza categoria.</p></td>
</tr>
<tr class="even">
<td><p><strong>Frequenza errori</strong></p></td>
<td><p>No</p></td>
<td><p>Percentuale delle sessioni peer-to-peer non riuscite.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Sessioni per modalità</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni raggruppate per modalità (ad esempio, messaggistica istantanea).</p></td>
</tr>
<tr class="even">
<td><p><strong>Frequenza errori per modalità</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni non riuscite raggruppate per modalità (ad esempio, messaggistica istantanea).</p></td>
</tr>
</tbody>
</table>

