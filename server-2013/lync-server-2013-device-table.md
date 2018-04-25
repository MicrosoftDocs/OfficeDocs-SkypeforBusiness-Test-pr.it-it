---
title: 'Lync Server 2013: Tabella Device'
TOCTitle: Tabella Device
ms:assetid: d5a4f777-bc12-4ce8-bc0d-867d5e22b436
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398930(v=OCS.15)
ms:contentKeyID: 49302119
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella Device in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella Device è una tabella di supporto in cui vengono archiviate informazioni sui diversi dispositivi di acquisizione o di rendering. Ogni record della tabella rappresenta un dispositivo.


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
<td><p><strong>DeviceKey</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero univoco che identifica il dispositivo.</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceName</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p>DeviceName + DeviceType è univoco</p></td>
<td><p>Nome del dispositivo.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceType</strong></p></td>
<td><p>bit</p></td>
<td><p>DeviceName + DeviceType è univoco</p></td>
<td><p>Tipo di dispositivo. 1 corrisponde a un dispositivo di acquisizione, 0 a un dispositivo di rendering.</p></td>
</tr>
</tbody>
</table>

