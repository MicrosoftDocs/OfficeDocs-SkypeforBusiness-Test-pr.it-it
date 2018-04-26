---
title: 'Lync Server 2013: Riepilogo di DNS - bilanciamento del carico DNS e bilanciamento del carico hardware'
TOCTitle: Riepilogo di DNS - bilanciamento del carico DNS e bilanciamento del carico hardware
ms:assetid: d2132695-1956-4190-a98e-cd7255cbded6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205273(v=OCS.15)
ms:contentKeyID: 49302062
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo di DNS - bilanciamento del carico DNS e bilanciamento del carico hardware in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella tabella seguente è contenuto un riepilogo dei record DNS necessari per supportare il Server Director con bilanciamento del carico DNS e con bilanciamento del carico hardware. Il ruolo del Server Director richiede record DNS simili a quelli del Front End Server. Il numero di record necessari si rispecchia nei nomi alternativi del soggetto necessari nel certificato del Server Director. Diversamente dal Front End Server, il pool di server Director non ospita account utente o i servizi per dispositivi mobili.

### Record DNS necessari per il pool di server Director che utilizzano il bilanciamento del carico DNS e dispositivi di bilanciamento del carico hardware

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Posizione/TIPO/Porta</th>
<th>FQDN/Record DNS</th>
<th>Indirizzo IP/FQDN</th>
<th>Corrisponde a/Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DNS interno/A</p></td>
<td><p>dir01.contoso.net</p></td>
<td><p>Server Director</p></td>
<td><p>Record dell'host server Server Director utilizzato per la replica e per le connessioni server-server</p></td>
</tr>
<tr class="even">
<td><p>DNS interno/A</p></td>
<td><p>dirpool01.contoso.net</p></td>
<td><p>pool di server Director</p></td>
<td><p>Record dell'host per il pool di server Director con bilanciamento del carico DNS per le connessioni server-server</p></td>
</tr>
<tr class="odd">
<td><p>DNS interno/A</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>pool di server Director</p></td>
<td><p>SIP (Session Initiation Protocol) in ingresso dall'interfaccia interna del server perimetrale</p></td>
</tr>
<tr class="even">
<td><p>DNS interno/A</p></td>
<td><p>dialin.contoso.com</p></td>
<td><p>VIP con bilanciamento del carico hardware del pool di server Director</p></td>
<td><p>Servizi Web dialin pubblicati e con bilanciamento del carico hardware da proxy inverso</p></td>
</tr>
<tr class="odd">
<td><p>DNS interno/A</p></td>
<td><p>meet.contoso.com</p></td>
<td><p>VIP con bilanciamento del carico hardware del pool di server Director</p></td>
<td><p>Servizi Web meet pubblicati e con bilanciamento del carico hardware da proxy inverso</p></td>
</tr>
<tr class="even">
<td><p>DNS interno/A</p></td>
<td><p>webdirexternal.contoso.com</p></td>
<td><p>VIP con bilanciamento del carico hardware del pool di server Director</p></td>
<td><p>Servizi Web esterni del ticket Web con bilanciamento del carico hardware e pubblicati e definiti dal proxy inverso per il pool di server Director</p></td>
</tr>
</tbody>
</table>

