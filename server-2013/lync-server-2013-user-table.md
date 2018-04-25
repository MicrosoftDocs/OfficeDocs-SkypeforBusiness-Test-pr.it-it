---
title: 'Lync Server 2013: Tabella User'
TOCTitle: Tabella User
ms:assetid: 6b52047e-286d-47ab-b7bc-a9b266f62d82
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398505(v=OCS.15)
ms:contentKeyID: 49300884
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella User in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella User è una tabella di supporto in cui è archiviato un elenco dei diversi utenti che hanno partecipato alle sessioni registrate nel database. Ogni record della tabella rappresenta un utente.


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
<th><strong>Chiave/indice</strong></th>
<th><strong>Dettagli</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>UserKey</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero univoco che identifica l'utente.</p></td>
</tr>
<tr class="even">
<td><p><strong>URI</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p>Univoco</p></td>
<td><p>Stringa URI.</p></td>
</tr>
<tr class="odd">
<td><p><strong>URIType</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>1 è un tipo di URI sconosciuto.</p>
<p>2 è un URI utente.</p>
<p>4 è un URI conferenza.</p>
<p>8 è un URI telefono.</p></td>
</tr>
<tr class="even">
<td><p><strong>TenantKey</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Tenant dell'utente, cui viene fatto riferimento dalla tabella Tenant.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LastPoorCallTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>Ultimo indicatore di data e ora in cui si è verificata una chiamata audio di qualità scadente per l'utente.</p></td>
</tr>
<tr class="even">
<td><p><strong>NextUpdateTS</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>Solo per uso interno.</p></td>
</tr>
</tbody>
</table>

