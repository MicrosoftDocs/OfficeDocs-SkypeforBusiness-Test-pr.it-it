---
title: 'Lync Server 2013: Chiamate in arrivo'
TOCTitle: Chiamate in arrivo
ms:assetid: 65b9c1b4-6af7-4527-8c33-22c4442bd209
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994038(v=OCS.15)
ms:contentKeyID: 52062177
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Chiamate in arrivo in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il routing delle chiamate in arrivo per gli utenti abilitati per il routing in base alla posizione dipende dalla posizione dell'endpoint dell'utente. Il routing delle chiamate in arrivo funziona come descritto di seguito. Se un utente ha una chiamata in arrivo in un endpoint di un sito di rete abilitato per il routing in base alla posizione e l'endpoint si trova nello stesso sito di rete del gateway PSTN, la chiamata verrà instradata. Se un utente ha una chiamata in arrivo in un endpoint di un sito di rete abilitato per il routing in base alla posizione e l'endpoint si trova in un sito di rete diverso da quello del gateway PSTN, la chiamata non verrà instradata. Se l'utente non ha endpoint nello stesso sito di rete del gateway PSTN da cui proviene la chiamata, questa verrà instradata direttamente alla segreteria telefonica dell'utente e il destinatario della chiamata riceverà una notifica di chiamata senza risposta.

Le impostazioni di inoltro delle chiamate di un utente abilitato per il routing in base alla posizione continueranno a essere applicate, tuttavia le chiamate inoltrate saranno soggette alle limitazioni del routing in base alla posizione dell'utente.

Nella tabella seguente viene illustrato come il routing in base alla posizione influisce sul routing delle chiamate in arrivo a seconda della posizione dell'endpoint del destinatario della chiamata. Il sito di rete del gateway PSTN è abilitato per il routing in base alla posizione, che è l'unico metodo per instradare le chiamate PSTN a endpoint all'interno dello stesso sito di rete.

### Il destinatario riceve una chiamata in arrivo dal gateway PSTN

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>L'endpoint del destinatario si trova nello stesso sito di rete del gateway PSTN</th>
<th>L'endpoint del destinatario non si trova nello stesso sito di rete del gateway PSTN</th>
<th>L'endpoint del destinatario si trova in un sito di rete sconosciuto o non abilitato per il routing in base alla posizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Routing della chiamata PSTN in arrivo</p></td>
<td><p>Le chiamate in arrivo vengono instradate agli endpoint del destinatario</p></td>
<td><p>Le chiamate in arrivo non vengono instradate agli endpoint del destinatario</p></td>
<td><p>Le chiamate in arrivo non vengono instradate agli endpoint del destinatario</p></td>
</tr>
</tbody>
</table>

  

## Vedere anche

#### Ulteriori risorse

[Scenari per il routing in base alla posizione in Lync Server 2013](lync-server-2013-scenarios-for-location-based-routing.md)

