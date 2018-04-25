---
title: Tabella CodecDescription in Lync Server 2013
TOCTitle: Tabella CodecDescription in Lync Server 2013
ms:assetid: 3598acb8-7ea6-4748-8417-149c971c32a2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204797(v=OCS.15)
ms:contentKeyID: 49300146
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella CodecDescription in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella CodecDescription associa identificatori codec univoci al codec corrispondente. I codec vengono usati per codificare i segnali digitali per la trasmissione, quindi per decodificare tali segnali per la riproduzione. Questa tabella è stata introdotta in Microsoft Lync Server 2013


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
<td><p><strong>CodecDescriptionKey</strong></p></td>
<td><p>smallint</p></td>
<td><p>Primaria/o</p></td>
<td><p>Identificatore univoco assegnato al codec.</p></td>
</tr>
<tr class="even">
<td><p><strong>CodecDescription</strong></p></td>
<td><p>varchar(256)</p></td>
<td><p>Univoca/o</p></td>
<td><p>Descrizione univoca del codec corrispondente a CodecDescriptionKey.</p></td>
</tr>
</tbody>
</table>

