---
title: 'Lync Server 2013: tblPreference'
TOCTitle: tblPreference
ms:assetid: f94eb128-f782-42ff-a568-ed3529573bc8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615052(v=OCS.15)
ms:contentKeyID: 49302524
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# tblPreference in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella tblPreference contiene le preferenze client degli utenti. In genere viene utilizzata dai client precedenti a Lync 2013.

### Colonne

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Colonna</th>
<th>Tipo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>prefLabel</p></td>
<td><p>nvarchar (255), not null</p></td>
<td><p>Etichetta in formato: &lt;uri sip utente&gt;|nomeutente.&lt;setpreferenze&gt;.</p></td>
</tr>
<tr class="even">
<td><p>prefSeqID</p></td>
<td><p>int, not null</p></td>
<td><p>Numero sequenziale (per etichetta) per scopi di controllo delle versioni.</p></td>
</tr>
<tr class="odd">
<td><p>prefContent</p></td>
<td><p>nvarchar (max)</p></td>
<td><p>Contenuto codificato.</p></td>
</tr>
<tr class="even">
<td><p>lastModifiedBy</p></td>
<td><p>int, not null</p></td>
<td><p>ID dell'entità che ha aggiornato la preferenza.</p></td>
</tr>
</tbody>
</table>


### Chiave

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Colonna</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&lt;prefLabel, prefSeqID&gt;</p></td>
<td><p>Chiave primaria.</p></td>
</tr>
</tbody>
</table>

