---
title: 'Lync Server 2013: Tabella UserAgent'
TOCTitle: Tabella UserAgent
ms:assetid: d6bda1c0-b053-457a-9ffa-2ae859788775
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398939(v=OCS.15)
ms:contentKeyID: 49302113
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella UserAgent in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella UserAgent è una tabella di supporto in cui viene archiviato un elenco dei diversi agenti utente che hanno partecipato a sessioni registrate nel database. Ogni record della tabella rappresenta un agente utente.


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
<td><p><strong>UserAgentKey</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero univoco che identifica l'agente utente.</p></td>
</tr>
<tr class="even">
<td><p><strong>UserAgent</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>Univoco</p></td>
<td><p>Stringa dell'agente utente.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UAType</strong></p></td>
<td><p>smallint</p></td>
<td><p> </p></td>
<td><p>1 corrisponde a un Mediation Server.</p>
<p>2 corrisponde a un A/V Conferencing Server.</p>
<p>4 corrisponde a Lync.</p>
<p>8 corrisponde a un telefono IP.</p>
<p>16 corrisponde alla console Live Meeting.</p>
<p>32 corrisponde a Deployment Validation Tool (DVT).</p>
<p>64 corrisponde a Lync in computer Macintosh.</p>
<p>128 corrisponde a Office Communications Server 2007 R2 Attendant.</p>
<p>256 corrisponde al servizio Annuncio conferenza.</p>
<p>512 corrisponde a Operatore automatico conferenza.</p>
<p>1024 corrisponde all'applicazione Response Group.</p>
<p>2048 corrisponde a Controllo vocale esterno.</p></td>
</tr>
</tbody>
</table>

