---
title: 'Lync Server 2013: Squillo simultaneo'
TOCTitle: Squillo simultaneo
ms:assetid: df02f919-4d50-4832-9300-6c51f8b4fc56
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994079(v=OCS.15)
ms:contentKeyID: 52062454
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Squillo simultaneo in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Quando la parte chiamata ha abilitato lo squillo simultaneo, il routing in base alla posizione analizza la posizione del chiamante e gli endpoint delle parti chiamate, per determinare se la chiamata deve essere instradata.

La tabella seguente illustra un utente che ha configurato lo squillo simultaneo. La destinazione dello squillo simultaneo è un utente che si trova nello stesso sito di rete, in un sito di rete diverso, oppure in un sito di rete sconosciuto.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiamata PSTN in arrivo per</th>
<th>Nello stesso sito di rete del destinatario</th>
<th>In un sito di rete diverso da quello del destinatario</th>
<th>In un sito di rete sconosciuto o non abilitato per il routing in base alla posizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utente Lync</p></td>
<td><p>Squillo simultaneo consentito</p></td>
<td><p>Squillo simultaneo non consentito</p></td>
<td><p>Squillo simultaneo non consentito</p></td>
</tr>
</tbody>
</table>

  
La tabella seguente illustra una chiamata da un utente Lync (o chiamante Lync) nello stesso sito di rete, in un sito di rete diverso o da un sito di rete sconosciuto. Il destinatario della chiamata ha configurato come destinazione dello squillo simultaneo un endpoint PSTN, ad esempio un cellulare. In questo scenario, il routing in base alla posizione determinerà se la chiamata deve essere instradata o meno alla destinazione dello squillo simultaneo.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Destinazione squillo simultaneo</th>
<th>Nello stesso sito di rete del destinatario</th>
<th>In un sito di rete diverso da quello del destinatario</th>
<th>In un sito di rete sconosciuto o non abilitato per il routing in base alla posizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Endpoint PSTN</p></td>
<td><p>Squillo simultaneo consentito attraverso i criteri di routing vocale del sito del chiamante</p></td>
<td><p>Squillo simultaneo consentito attraverso i criteri di routing vocale del sito del chiamante</p></td>
<td><p>Squillo simultaneo consentito attraverso i criteri di routing vocale del chiamante ai trunk non abilitati per il routing in base alla posizione</p></td>
</tr>
</tbody>
</table>


## Vedere anche

#### Ulteriori risorse

[Scenari per il routing in base alla posizione in Lync Server 2013](lync-server-2013-scenarios-for-location-based-routing.md)

