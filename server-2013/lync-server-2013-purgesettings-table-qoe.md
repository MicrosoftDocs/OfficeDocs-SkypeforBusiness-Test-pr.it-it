---
title: Tabella PurgeSettings (QoE) in Lync Server 2013
TOCTitle: Tabella PurgeSettings (QoE) in Lync Server 2013
ms:assetid: 31b85d1c-3f32-4f67-94bf-9389cdd282c5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204788(v=OCS.15)
ms:contentKeyID: 49300102
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella PurgeSettings (QoE) in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella tabella PurgeSettings sono contenute informazioni che specificano se e quando i record QoE (qualità percepita dagli utenti) obsoleti verranno eliminati automaticamente dal database QoE. È possibile ottenere informazioni relative all'eliminazione anche in Microsoft Lync Server 2013 Management Shell eseguendo il comando seguente:

    Get-CsQoEConfiguration

Questa tabella è stata introdotta in Microsoft Lync Server 2013.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Colonna</strong></th>
<th><strong>Tipo di dati</strong></th>
<th><strong>Chiave/Indice</strong></th>
<th><strong>Dettagli</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ID</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria</p></td>
<td><p>Identificatore univoco per la raccolta delle impostazioni di eliminazione QoE.</p></td>
</tr>
<tr class="even">
<td><p><strong>EnablePurge</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>Se impostato su True (1) Microsoft Lync Server 2013 eliminerà periodicamente i record obsoleti dal database QoE. L'eliminazione verrà eseguita ogni giorno all'ora specificata dall'impostazione PurgeHour. Se impostato su False (0), i record non verranno eliminati automaticamente dal database. Il valore predefinito è True.</p></td>
</tr>
<tr class="odd">
<td><p><strong>KeepQoEDataForDays</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Specifica la giacenza dei record QoE (in giorni) che verranno eliminati dal database. Se l'eliminazione è abilitata, i record QoE precedenti a questo valore verranno rimossi dal database. Il valore predefinito è 60 giorni.</p></td>
</tr>
<tr class="even">
<td><p><strong>PurgeHour</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Specifica l'ora locale del giorno in cui verrà eseguita l'eliminazione dei dati del database. L'ora del giorno viene specificata nel formato 24 ore; 0 rappresenta la mezzanotte e 23 rappresenta le 11 di sera. Tenere presente che è possibile specificare solo l'ora del giorno: il valore 10 (a indicare le 10 del mattino) è consentito, mentre non lo è il valore 10,5 (a indicare le 10.30 del mattino). Il valore predefinito è 1 (1 del mattino). Specifica l'ora locale del giorno in cui verrà eseguita l'eliminazione dei dati del database. L'ora del giorno viene specificata nel formato 24 ore; 0 rappresenta la mezzanotte e 23 rappresenta le 11 di sera. Tenere presente che è possibile specificare solo l'ora del giorno: il valore 10 (a indicare le 10 del mattino) è consentito, mentre non lo è il valore 10,5 (a indicare le 10.30 del mattino). Il valore predefinito è 1 (1 del mattino).</p></td>
</tr>
</tbody>
</table>

