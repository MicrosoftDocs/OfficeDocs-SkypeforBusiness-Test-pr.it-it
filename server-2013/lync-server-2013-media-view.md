---
title: Visualizzazione Media
TOCTitle: Visualizzazione Media
ms:assetid: 1a7b2e59-082e-4188-98ae-48ae9bd3494a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ687981(v=OCS.15)
ms:contentKeyID: 49887462
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione Media

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella visualizzazione Media vengono archiviate le informazioni sul tipo di supporto utilizzato in una sessione peer-to-peer. Qualora si utilizzino più supporti, nella tabella saranno presenti più record per una sessione. Questa visualizzazione è stata introdotta in Microsoft Lync Server 2013.


> [!NOTE]
> La visualizzazione Media non deve essere utilizzata per calcolare la durata di utilizzo del supporto in una sessione. Questa visualizzazione contiene i dettagli di segnalazione dello scambio di supporti in una sessione. Lo scambio dei supporti viene effettuato mediante la richiesta INVITE, mentre StartTime indica l'ora in cui la richiesta INVITE è stata inviata. L'ora dell'invito non corrisponde necessariamente all'ora di inizio del supporto poiché questo viene avviato solo dopo che la sessione è stata accettata.



Oltre a quelle indicate di seguito, nella visualizzazione Media sono riportate tutte le colonne descritte nell'argomento [Visualizzazione SessionDetails](lync-server-2013-sessiondetails-view.md).


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Colonna</th>
<th>Tipo di dati</th>
<th>Dettagli</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Media</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Tipo di supporto. Per ulteriori informazioni, vedere <a href="lync-server-2013-medialist-table.md">Tabella MediaList in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>MediaStartTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Ora di invio di una richiesta di supporto.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MediaEndTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Ora di fine della sessione.</p></td>
</tr>
</tbody>
</table>

