---
title: Tabella ConferenceJoinTimeThresholds in Lync Server 2013
TOCTitle: Tabella ConferenceJoinTimeThresholds in Lync Server 2013
ms:assetid: 3944d724-bdd8-4d1c-a2af-933ee8141529
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204809(v=OCS.15)
ms:contentKeyID: 49300226
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella ConferenceJoinTimeThresholds in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella ConferenceJoinTimeThresholds include i limiti di classificazione utilizzati dal rapporto riepilogativo Tempo di partecipazione alla conferenza. Questo rapporto riepiloga la quantità di tempo richiesto agli utenti per partecipare a una conferenza. I valori temporali vengono riportati come media e in una delle categorie seguenti:

  - Meno di 2 secondi.

  - Tra 2 e 5 secondi.

  - Tra 5 e 10 secondi.

  - Più di 10 secondi.

La tabella ConferenceJoinTimeThresholds include i valori di classificazione 2 secondi, 5 secondi e 10 secondi.

La tabella è stata introdotta in Microsoft Lync Server 2013.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Colonna</th>
<th>Tipo di dati</th>
<th>Chiave/indice</th>
<th>Dettagli</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Soglia</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Identificatore univoco della classificazione.</p></td>
</tr>
<tr class="even">
<td><p><strong>ThresholdValue</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Limite superiore per la classificazione. I valori consentiti sono:</p>
<ol>
<li><p>2</p></li>
<li><p>5</p></li>
<li><p>10</p></li>
</ol></td>
</tr>
</tbody>
</table>

