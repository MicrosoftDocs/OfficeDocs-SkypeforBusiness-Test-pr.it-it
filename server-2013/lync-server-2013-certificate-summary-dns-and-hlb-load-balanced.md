---
title: 'Lync Server 2013: Riepilogo dei certificati - bilanciamento del carico DNS e bilanciamento del carico hardware'
TOCTitle: Riepilogo dei certificati - bilanciamento del carico DNS e bilanciamento del carico hardware
ms:assetid: 8318a1a4-b423-47b7-95e6-9541adfad391
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205047(v=OCS.15)
ms:contentKeyID: 49301169
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo dei certificati - bilanciamento del carico DNS e bilanciamento del carico hardware in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

I requisiti dei certificati per un Server Director con bilanciamento del carico DNS e bilanciamento del carico hardware consistono in un certificato predefinito avente un nome soggetto e nome alternativo soggetto per servizi che il Server Director è in grado di ricevere. Un certificato è richiesto per ciascun Server Director nel pool. È importante ricordare che il bilanciamento del carico hardware bilancia soltanto il traffic proveniente dal proxy inverso. Inoltre, esiste un certificato OAuth Token a fini di autenticazione server-to-server, installato su ciascun server.

### Certificati per Server Director

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente</th>
<th>Nome soggetto</th>
<th>Nomi alternativo soggetto</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Predefinito</p></td>
<td><p>dirpool01.contoso.net</p></td>
<td><p>dirpool01.contoso.net</p>
<p>dir01.contoso.net</p>
<p>dialin.contoso.com</p>
<p>meet.contoso.com</p>
<p>lyncdiscoverinternal.contoso.com</p>
<p>lyncdiscover.contoso.com</p>
<p>(Facoltativamente) *.contoso.com</p></td>
<td><p>I certificati per Server Director possono essere richiesti presso un'autorità di certificazione gestita internamente, o presso un'autorità di certificazione pubblica.</p>
<p>Il Server Director risponde alle richieste del proxy inverso nel perimetro, o dal server perimetrale. I client interni non utilizzano il Server Director.</p>
<p>In alternativa, una voce con caratteri jolly per gli URL semplici</p></td>
</tr>
<tr class="even">
<td><p>OAuthTokenIssuer</p></td>
<td><p>dir01.contoso.net</p></td>
<td><p>Nessuna voce</p></td>
<td>

> [!IMPORTANT]
> La lunghezza minima della chiave è pari a 1024, ma si potrebbe ricevere un messaggio che informa che la lunghezza minima consigliata è pari a 2048 bit.

<p>Il certificato OAuthTokenIssuer è un certificato a finalità singola, per l'autenticazione dei server in un ambiente a larga scala, e può essere richiesto a un'autorità di certificazione interna o pubblica. Questo certificato è obbligatorio.</p></td>
</tr>
</tbody>
</table>

