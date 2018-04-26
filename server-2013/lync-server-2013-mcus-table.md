---
title: 'Lync Server 2013: Tabella Mcus'
TOCTitle: Tabella Mcus
ms:assetid: 271b7963-8fd8-4d92-a701-1a62aaf895ee
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425742(v=OCS.15)
ms:contentKeyID: 49299978
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella Mcus in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella Mcus è una tabella di supporto. In ogni record vengono archiviate informazioni relative a un servizio di conferenza. Possono essere inclusi il servizio di conferenza di messaggistica istantanea e il servizio di conferenza di telefonia (che vengono eseguiti come processi nei Front End Server), nonché il servizio di conferenza Web e il servizio di conferenza A/V.


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
<td><p><strong>McuId</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero univoco che identifica questo server per conferenze.</p></td>
</tr>
<tr class="even">
<td><p><strong>McuUri</strong></p></td>
<td><p>nvarchar(450)</p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p><strong>McuTypeId</strong></p></td>
<td><p>inyint</p></td>
<td><p>Esterna</p></td>
<td><p>Tipo di server per conferenze, ad esempio conf:chat (per la messaggistica istantanea) o conf:audio-video. Per ulteriori informazioni, vedere la <a href="lync-server-2013-uritypes-table.md">Tabella UriTypes in Lync Server 2013</a>.</p></td>
</tr>
</tbody>
</table>

