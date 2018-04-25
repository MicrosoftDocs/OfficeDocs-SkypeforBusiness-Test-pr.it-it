---
title: Visualizzazione ProgressReport
TOCTitle: Visualizzazione ProgressReport
ms:assetid: b49f3fc7-0e2f-498f-8505-aaaf54e435f9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721857(v=OCS.15)
ms:contentKeyID: 49887716
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione ProgressReport

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella visualizzazione ProgressReport vengono archiviate le informazioni relative alle sessioni completate. Tali rapporti sullo stato verranno scritti solo per le chiamate e le sessioni ritenute utili da Lync Server 2013 a fini diagnostici. Questa visualizzazione è stata introdotta in Microsoft Lync Server 2013.


> [!NOTE]
> I campi ErrorTime, ErrorReportSeq e ProgressReportSeq non fanno necessariamente riferimento a errori, bensì a messaggi in cui viene indicato lo stato delle chiamate o dei messaggi.




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
<td><p><strong>ErrorTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Data e ora in cui si è verificato l'errore. Questo valore viene utilizzato insieme a ErrorReportSeq per identificare in modo univoco un errore.</p></td>
</tr>
<tr class="even">
<td><p><strong>ErrorReportSeq</strong></p></td>
<td><p>int</p></td>
<td><p>ID che identifica l'errore. Questo valore viene utilizzato insieme a ErrorTime per identificare in modo univoco un errore.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ProgressReportSeq</strong></p></td>
<td><p>int</p></td>
<td><p>ID che identifica il rapporto sullo stato. Questo valore viene utilizzato per distinguere i rapporti sullo stato della stessa segnalazione di errore.</p></td>
</tr>
<tr class="even">
<td><p><strong>MsDiagId</strong></p></td>
<td><p>int</p></td>
<td><p>ID diagnostica della segnalazione di errore.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Source</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Nome del server da cui ha avuto origine l'errore (se la segnalazione è stata inviata da un componente server).</p></td>
</tr>
<tr class="even">
<td><p><strong>Application</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Nome dell'applicazione da cui ha avuto origine l'errore (se la segnalazione è stata inviata da un componente server).</p></td>
</tr>
<tr class="odd">
<td><p><strong>TelemetryId</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p>Identificatore univoco che correla le informazioni relative alla data e ora di partecipazione per i diversi componenti coinvolti in una conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionSetupTime</strong></p></td>
<td><p>int</p></td>
<td><p>Intervallo di tempo, in millisecondi, necessario a un componente specifico per partecipare a una conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MsDiagHeader</strong></p></td>
<td><p>varchar(max)</p></td>
<td><p>Ulteriori informazioni sull'errore.</p></td>
</tr>
</tbody>
</table>

