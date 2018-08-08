---
title: "Lync Server 2013: Certif.: pool di Director c/ scalab. implem.,  bilanciam. carico hw"
TOCTitle: Riepilogo dei certificati - pool di server Director con scalabilità implementata, servizio di bilanciamento del carico hardware
ms:assetid: 45940add-8027-418d-b79a-9033b494762f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204846(v=OCS.15)
ms:contentKeyID: 49300385
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo dei certificati - pool di server Director con scalabilità implementata, servizio di bilanciamento del carico hardware in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

I requisiti del certificato per un Server Director con un servizio di bilanciamento del carico hardware prevedono l'uso di un certificato predefinito che contiene un nome oggetto e nomi alternativi dell'oggetto per i servizi che il pool di server Director può ricevere. Viene richiesto un certificato per ogni Server Director del pool. Inoltre, esiste un certificato rilasciato dal token OAuth installato in ogni server per scopi di autenticazione da server a server.

### Certificati per un server Director in scala che utilizza un servizio di bilanciamento hardware

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
<p>Il Server Director risponde alle richieste del proxy inverso nel perimetro, o dal server perimetrale.</p>
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

