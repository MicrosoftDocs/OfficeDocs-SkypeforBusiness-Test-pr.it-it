---
title: "#VALUE!"
TOCTitle: Riepilogo di DNS - pool di server Director con scalabilità implementata, servizio di bilanciamento del carico hardware
ms:assetid: 08ba48e6-bfa1-4ab0-bc89-d58ddb9c20af
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204655(v=OCS.15)
ms:contentKeyID: 49299603
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo di DNS - pool di server Director con scalabilità implementata, servizio di bilanciamento del carico in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella seguente contiene un riepilogo dei record DNS necessari per supportare il Server Director con bilanciamento del carico hardware. Il ruolo Server Director richiede record DNS simili a quelli del Front End Server. Il numero di record necessari è indicato dei nomi alternativi del soggetto richiesti nel certificato per il Server Director. A differenza del Front End Server, il pool di server Director non ospita account utente, né servizi per dispositivi mobili.

### Record DNS necessari per il pool di server Director utilizzando un servizio di bilanciamento del carico e il bilanciamento del carico DNS

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
<td><p>Record host del Server Director utilizzato per la replica e per le comunicazioni server-server</p></td>
</tr>
<tr class="even">
<td><p>DNS interno/A</p></td>
<td><p>dirpool01.contoso.net</p></td>
<td><p>VIP HLB del pool di server Director</p></td>
<td><p>Record host per il pool di server Director con bilanciamento del carico DNS</p></td>
</tr>
<tr class="odd">
<td><p>DNS interno/A</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>VIP con bilanciamento del carico hardware del pool di server Director</p></td>
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
<td><p>Servizi Web esterni Web Ticket con bilanciamento del carico hardware pubblicati e definiti dal proxy inverso per il pool di server Director</p></td>
</tr>
</tbody>
</table>

