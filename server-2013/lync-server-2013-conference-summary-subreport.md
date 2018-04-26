---
title: Sottoreport riepilogativo conferenze
TOCTitle: Sottoreport riepilogativo conferenze
ms:assetid: 2fc1d2bf-34f5-4093-a6e2-250ec1f1b004
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204779(v=OCS.15)
ms:contentKeyID: 49300072
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Sottoreport riepilogativo conferenze

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il sottorapporto riepilogativo conferenze offre una visualizzazione generale delle sessioni di conferenza non riuscite. Tali sessioni vengono ulteriormente suddivise per tipo: sessioni Focus e sessioni MCU.

## Filtri

I filtri consentono di restituire un set di dati più appropriato, nonché visualizzare i dati restituiti in diversi modi. Nella tabella che segue sono elencati i filtri che è possibile usare con il sottorapporto riepilogativo conferenze.

### Filtri del sottorapporto riepilogativo conferenze

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
<td><p>Data/ora di inizio per l'intervallo di tempo. Per visualizzare i dati per ora, immettere sia la data che l'ora di inizio in questo modo:</p>
<p>07/07/2012 13.00</p>
<p>Se non si immette una data/ora di inizio, il rapporto inizia automaticamente alle 00.00 del giorno specificato. Per visualizzare i dati in base al giorno, immettere solo la data:</p>
<p>07/07/2012</p>
<p>Per visualizzare i dati per settimana o per mese, immettere una data compresa nella settimana o nel mese che si desidera visualizzare (non è necessario immettere il primo giorno della settimana o del mese):</p>
<p>03/07/2012</p>
<p>Le settimane vanno sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="even">
<td><p><strong>A</strong></p></td>
<td><p>Data/ora di fine per l'intervallo di tempo. Per visualizzare i dati in base all'ora, inserire sia la data che l'ora di fine come segue:</p>
<p>07/07/2012 13.00</p>
<p>Se non si immette una data/ora di fine, il rapporto termina automaticamente alle 00.00 del giorno specificato. Per visualizzare i dati per giorno, immettere solo la data:</p>
<p>07/07/2012</p>
<p>Per visualizzare i dati per settimana o mese, immettere una data compresa nella settimana o nel mese che si desidera visualizzare (non è necessario immettere il primo giorno della settimana o del mese):</p>
<p>03/07/2012</p>
<p>Le settimane vanno sempre dal lunedì alla domenica.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Pool</strong></p></td>
<td><p>Nome di dominio completo (FQDN) del pool di registrazione o del server perimetrale. È possibile selezionare un singolo pool oppure fare clic su <strong>[Tutto]</strong> per visualizzare i dati di tutti i pool. Le voci disponibili in questo elenco a discesa vengono inserite automaticamente in base ai record presenti nel database.</p></td>
</tr>
</tbody>
</table>


## Metriche

Nella tabella seguente sono elencate le informazioni fornite nel sottoreport riepilogativo conferenze.

### Metriche del sottorapporto riepilogativo conferenze

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Possibilità di ordinare i dati in base a questo elemento</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Totale conferenze</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di conferenze effettuate.</p></td>
</tr>
<tr class="even">
<td><p><strong>Totale sessioni conferenza</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni di conferenza. Una singola conferenza può includere più sessioni, ad esempio una sessione Focus e una sessione MCU.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Frequenza generale errori sessione</strong></p></td>
<td><p>No</p></td>
<td><p>Percentuale di tutte le conferenze non riuscite.</p></td>
</tr>
<tr class="even">
<td><p><strong>Sessioni Focus</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni Focus.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Frequenza errori Focus</strong></p></td>
<td><p>No</p></td>
<td><p>Percentuale di sessioni Focus non riuscite.</p></td>
</tr>
<tr class="even">
<td><p>Sessioni MCU</p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni MCU.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Frequenza errori MCU</strong></p></td>
<td><p>No</p></td>
<td><p>Percentuale di sessioni MCU non riuscite.</p></td>
</tr>
<tr class="even">
<td><p><strong>Sessioni MCU per modalità</strong></p></td>
<td><p>No</p></td>
<td><p>Numero totale di sessioni MCU, raggruppate per modalità (ad esempio IM Conferencing).</p></td>
</tr>
<tr class="odd">
<td><p><strong>Frequenza errori per modalità</strong></p></td>
<td><p>No</p></td>
<td><p>Percentuale di sessioni MCU non riuscite, raggruppate per modalità (ad esempio IM Conferencing).</p></td>
</tr>
</tbody>
</table>

