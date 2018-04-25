---
title: 'Lync Server 2013: Tabella Dialogs'
TOCTitle: Tabella Dialogs
ms:assetid: 487a430b-af66-4ea6-b28e-4e33cfdb7f9e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425954(v=OCS.15)
ms:contentKeyID: 49300427
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella Dialogs in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella Dialogs è una tabella di supporto in cui sono archiviate le informazioni relative ai DialogID per le sessioni peer-to-peer.


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
<td><p>Data/ora della richiesta della sessione. Questo valore viene utilizzato insieme a SessionIDSeq per identificare in modo univoco una sessione.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero ID per identificare la sessione. Utilizzato insieme a SessionIDTime per identificare in modo univoco una sessione.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ExternalChecksum</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Checksum di ExternalID. Questo campo viene utilizzato per aumentare la velocità delle ricerche nei database.</p></td>
</tr>
<tr class="even">
<td><p><strong>ExternalId</strong></p></td>
<td><p>varbinary(775)</p></td>
<td><p> </p></td>
<td><p>ID dialogo SIP, archiviato come valore binario. Il formato del valore binario è il seguente:</p>
<p>dialog;from-tag;to-tag</p>
<p>Questi dati possono essere convertiti in formato testo utilizzando la sintassi seguente:</p>
<p><code>cast(cast(ExternalId as varbinary(max)) as varchar(max))</code></p></td>
</tr>
</tbody>
</table>

