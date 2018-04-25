---
title: 'Lync Server 2013: Tabella Media'
TOCTitle: Tabella Media
ms:assetid: 1e1b427f-59b5-4564-bde5-1002a80439ee
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398268(v=OCS.15)
ms:contentKeyID: 49299867
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella Media in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Ogni record rappresenta un tipo di supporto multimediale utilizzato in una sessione peer-to-peer. Una sessione viene rappresentata da più record nella tabella se viene utilizzato più di un tipo di supporto multimediale.


> [!NOTE]
> Non utilizzare la tabella Media per calcolare la durata media di una sessione. Questa tabella contiene i dettagli di segnalazione dello scambio multimediale in una sessione. Lo scambio multimediale viene eseguito dalla richiesta INVITE e StartTime indica l'ora di invio di tale richiesta. L'ora di invito non corrisponde necessariamente all'ora di inizio dello scambio multimediale, poiché questo inizia solo dopo che il destinatario ha accettato la sessione. EndTime in genere indica l'ora di fine della sessione.




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
<td><p><strong>SessionIdTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Primaria, esterna</p></td>
<td><p>Ora della richiesta di sessione. Valore utilizzato in combinazione con <strong>SessionIdSeq</strong> per identificare in modo univoco una sessione. Vedere la <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a> per ulteriori informazioni.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria, esterna</p></td>
<td><p>Numero di ID per identificare la sessione. Utilizzato in combinazione con <strong>SessionIdTime</strong> per identificare in modo univoco una sessione. Per ulteriori informazioni, vedere <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MediaId</strong></p></td>
<td><p>tinyint</p></td>
<td><p>Primaria, esterna</p></td>
<td><p>Numero univoco che identifica il tipo di elemento multimediale. Vedere <a href="lync-server-2013-medialist-table.md">Tabella MediaList in Lync Server 2013</a> per ulteriori informazioni.</p></td>
</tr>
<tr class="even">
<td><p><strong>StartTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Primaria/o</p></td>
<td><p>Indica l'ora di invio di una richiesta di scambio multimediale e non l'ora di inizio dello scambio multimediale effettivo. <strong>StartTime</strong> include il tempo di configurazione della sessione.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EndTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>Ora di fine della sessione.</p></td>
</tr>
</tbody>
</table>

