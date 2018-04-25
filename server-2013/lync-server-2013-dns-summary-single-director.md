---
title: 'Lync Server 2013: Riepilogo di DNS - singolo server Director'
TOCTitle: Riepilogo di DNS - singolo server Director
ms:assetid: 790ecb56-92cd-41f4-baf6-c290a707aa4d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205021(v=OCS.15)
ms:contentKeyID: 49301051
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo di DNS - singolo server Director in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella tabella seguente è incluso un riepilogo dei record DNS necessari per supportare un Server Director singolo. Il ruolo del Server Director richiede record DNS simili al Front End Server. Il numero di record necessari è riportato nei nomi alternativi soggetto necessari sul certificato di Server Director. Diversamente dal Front End Server, il Server Director non ospita account utente o servizi di mobilità.

### Record DNS necessari per il Server Director

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
<td><p>sip.contoso.com</p></td>
<td><p>Server Director</p></td>
<td><p>SIP in ingresso dalla interfaccia Edge interna del server perimetrale</p></td>
</tr>
<tr class="odd">
<td><p>DNS interno/A</p></td>
<td><p>dialin.contoso.com</p></td>
<td><p>Server Director</p></td>
<td><p>Servizi Web Accesso esterno pubblicati da proxy inverso</p></td>
</tr>
<tr class="even">
<td><p>DNS interno/A</p></td>
<td><p>meet.contoso.com</p></td>
<td><p>Server Director</p></td>
<td><p>Servizi Web Accesso Riunione pubblicati da proxy inverso</p></td>
</tr>
<tr class="odd">
<td><p>DNS interno/A</p></td>
<td><p>webdirexternal.contoso.com</p></td>
<td><p>Server Director</p></td>
<td><p>Servizi Web esterni Ticket Web per Server Director pubblicati e definiti dal proxy inverso</p></td>
</tr>
</tbody>
</table>

