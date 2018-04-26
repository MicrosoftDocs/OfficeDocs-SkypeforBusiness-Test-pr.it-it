---
title: Tabella SIPResponseMetaData in Lync Server 2013
TOCTitle: Tabella SIPResponseMetaData in Lync Server 2013
ms:assetid: cf723737-4a75-4352-829b-f4954aa59716
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205294(v=OCS.15)
ms:contentKeyID: 49302025
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella SIPResponseMetaData in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella tabella SIPResponseMetaDataTable è contenuto un elenco di codici di risposta SIP con la classificazione e la definizione di ogni codice. Questi codici vengono generati in risposta a eventi che influiscono sui dispositivi SIP e sulle sessioni di comunicazioni SIP. Il codice di risposta 403 ad esempio viene generato quando un dispositivo SIP invia una richiesta, che però non viene soddisfatta dal server.

Questa tabella è stata introdotta in Microsoft Lync Server 2013.


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
<td><p><strong>ResponseCode</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria</p></td>
<td><p>Valore numerico che rappresenta il codice di risposta SIP.</p></td>
</tr>
<tr class="even">
<td><p><strong>Class</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Classifica generale del codice di risposta. Sono incluse le classifiche seguenti:</p>
<ul>
<li><p>1: risposte informali</p></li>
<li><p>2: risposte con esito positivo</p></li>
<li><p>3: risposte di reindirizzamento</p></li>
<li><p>4: risposte di errore client</p></li>
<li><p>5: risposte di errore server</p></li>
<li><p>6: risposta di errore globale</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Description</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p></p></td>
<td><p>Descrizione del codice di risposta SIP. Il codice di risposta 181 ad esempio è associato alla descrizione seguente:</p>
<p>Call Is Being Forwarded</p></td>
</tr>
</tbody>
</table>

