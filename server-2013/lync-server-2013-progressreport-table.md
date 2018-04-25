---
title: 'Lync Server 2013: Tabella ProgressReport'
TOCTitle: Tabella ProgressReport
ms:assetid: 38e5f060-5e9b-4185-87b2-7ef61c4bb75f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425864(v=OCS.15)
ms:contentKeyID: 49300229
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella ProgressReport in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

I rapporti sullo stato sono basati sui dati caricati dal client nel database al termine di una chiamata o di una sessione. Tali rapporti verranno scritti solo per le chiamate e le sessioni ritenute utili da Lync Server 2013 a fini diagnostici.

I campi ErrorTime, ErrorReportSeq e ProgressReportSeq non fanno necessariamente riferimento a errori, bensì a messaggi in cui viene indicato lo stato delle chiamate o dei messaggi.


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
<td><p><strong>ErrorTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Primaria, esterna</p></td>
<td><p>Data e ora della segnalazione degli errori di stato inclusa nel rapporto sullo stato. Per ulteriori informazioni, vedere la <a href="lync-server-2013-errorreport-table.md">Tabella ErrorReport in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>ErrorId</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria, esterna</p></td>
<td><p>Numero ID utilizzato insieme a ErrorTime e ProgressReportSeq per identificare in modo univoco un rapporto sullo stato. Per ulteriori informazioni, vedere la <a href="lync-server-2013-errorreport-table.md">Tabella ErrorReport in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ErrorReportSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria, esterna</p></td>
<td><p>Numero ID utilizzato insieme a ErrorTime e ProgressReportSeq per identificare in modo univoco una segnalazione errori. Per ulteriori informazioni, vedere la <a href="lync-server-2013-errorreport-table.md">Tabella ErrorReport in Lync Server 2013</a>.</p>
<p>Questo campo è stato introdotto in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>ProgressReportSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero ID per identificare il rapporto sullo stato. Utilizzato insieme a ErrorTime ed ErrorReportSeq per identificare in modo univoco un rapporto sullo stato.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MsDiagId</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>ID diagnostica del rapporto sullo stato.</p>
<p>Questo campo è stato introdotto in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>SourceId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Server che ha inviato la segnalazione errori (se il rapporto è stato inviato da un componente server). Per ulteriori informazioni, vedere la <a href="lync-server-2013-servers-table.md">Tabella Servers in Lync Server 2013</a>. Questo campo è stato introdotto in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ApplicationId</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Processo di Lync Server a cui fa riferimento il rapporto. Per ulteriori informazioni, vedere la tabella Application.</p></td>
</tr>
<tr class="even">
<td><p><strong>Dettagli</strong></p></td>
<td><p>image</p></td>
<td><p></p></td>
<td><p>Dettagli del rapporto sullo stato archiviati in formato binario per non occupare troppo spazio. I dati possono essere convertiti in formato testo utilizzando la sintassi seguente:</p>
<p>cast(cast(Detail as varbinary(max)) as varchar(max))</p></td>
</tr>
<tr class="odd">
<td><p><strong>TelemetryId</strong></p></td>
<td><p>uniqueIdentifier</p></td>
<td><p></p></td>
<td><p>Identificatore univoco che correla informazioni relative al tempo di partecipazione per i diversi componenti coinvolti in una conferenza.</p>
<p>Questo campo è stato introdotto in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionSetupTime</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Tempo (in millisecondi) necessario per un componente specifico per partecipare a una conferenza.</p>
<p>Questo campo è stato introdotto in Microsoft Lync Server 2013.</p></td>
</tr>
</tbody>
</table>

