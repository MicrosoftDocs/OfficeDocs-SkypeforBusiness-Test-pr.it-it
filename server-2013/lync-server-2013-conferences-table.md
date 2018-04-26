---
title: 'Lync Server 2013: Tabella Conferences'
TOCTitle: Tabella Conferences
ms:assetid: c3da6271-b3c6-4898-894f-10456ec794d0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412964(v=OCS.15)
ms:contentKeyID: 49301880
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella Conferences in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In ogni record di questa tabella sono contenuti dettagli delle chiamate relativi a una conferenza.


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
<td><p>Primaria/o</p></td>
<td><p>Data e ora di acquisizione della richiesta di conferenza da parte dell'agente di registrazione dettagli chiamata. Valore utilizzato solo come chiave primaria per identificare in modo univoco un'istanza di conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero di ID per identificare la sessione. Valore utilizzato in combinazione con <strong>SessionIdTime</strong> per identificare in modo univoco l'istanza della conferenza.*</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConferenceUriId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>URI della conferenza. Per ulteriori informazioni, vedere la <a href="lync-server-2013-conferenceuris-table.md">Tabella ConferenceUris in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>ConfInstance</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p> </p></td>
<td><p>Utile per conferenze ricorrenti. A ogni istanza di una conferenza ricorrente viene assegnato lo stesso <strong>ConferenceUri</strong> , ma il valore <strong>ConfInstance</strong> sarà diverso.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConferenceStartTime</strong></p></td>
<td><p>datetime</p></td>
<td><p> </p></td>
<td><p>Data e ora di fine della conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>ConferenceEndTime</strong></p></td>
<td><p>datetime</p></td>
<td><p> </p></td>
<td><p>Data e ora di fine della conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><strong>PoolId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Numero di ID per identificare il pool in cui viene acquisita la conferenza. Per ulteriori informazioni, vedere la <a href="lync-server-2013-pools-table.md">Tabella Pools in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>OrganizerId</strong></p></td>
<td><p>Int</p></td>
<td><p>Esterna</p></td>
<td><p>Numero di ID per identificare l'URI dell'organizzatore della conferenza. Per ulteriori informazioni, vedere la <a href="lync-server-2013-users-table.md">Tabella Users in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Flag</strong></p></td>
<td><p>smallint</p></td>
<td><p></p></td>
<td><p>Maschera di bit che contiene gli attributi della conferenza. I valori possibili sono:</p>
<ul>
<li><p>0X01</p></li>
<li><p>Synthetic</p></li>
<li><p>Transaction</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Processed</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>Campo interno utilizzato dal servizio di monitoraggio.</p>
<p>Questo campo è stato introdotto in Microsoft Lync Server 2013.</p></td>
</tr>
</tbody>
</table>


\* Per la maggior parte delle sessioni il valore di SessionIdSeq sarà 1. Se due sessioni iniziano esattamente alla stessa ora, il valore SessionIdSeq per una sarà 1, per l'altra sarà 2 e così via.

