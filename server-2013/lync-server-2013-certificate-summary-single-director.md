---
title: 'Lync Server 2013: Riepilogo dei certificati - singolo server Director'
TOCTitle: Riepilogo dei certificati - singolo server Director
ms:assetid: 1b769a76-cbf3-46e9-a955-f6cde5faff93
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204720(v=OCS.15)
ms:contentKeyID: 49299838
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo dei certificati - singolo server Director in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

I requisiti di certificato per un solo Server Director consistono in un certificato predefinito con lo stesso nome soggetto e nomi soggetto alternativi per i servizi che il Server Director può ricevere. È inoltre presente un certificato token OAuth ai fini dell'autenticazione da server a server.

### Certificati per il Director

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
<td><p>dir01.contoso.net</p></td>
<td><p>dir01.contoso.net</p>
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
<td><div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La lunghezza minima della chiave è pari a 1024, ma si potrebbe ricevere un messaggio che informa che la lunghezza minima consigliata è pari a 2048 bit.</td>
</tr>
</tbody>
</table>

</div>
<p>Il certificato OAuthTokenIssuer è un certificato a finalità singola, per l'autenticazione dei server in un ambiente a larga scala, e può essere richiesto a un'autorità di certificazione interna o pubblica. Questo certificato è obbligatorio.</p>
<p></p></td>
</tr>
</tbody>
</table>

