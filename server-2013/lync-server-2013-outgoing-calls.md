---
title: 'Lync Server 2013: Chiamate in uscita'
TOCTitle: Chiamate in uscita
ms:assetid: 885ffe6f-cd51-4f21-8d4f-a1ff8d818858
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994049(v=OCS.15)
ms:contentKeyID: 52062204
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Chiamate in uscita in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il routing delle chiamate in uscita di utenti abilitati per il routing in base alla posizione dipende dalla posizione dell'endpoint dell'utente nella rete. Nella tabella seguente è illustrato l'effetto del routing in base alla posizione sul routing delle chiamate in uscita a seconda della posizione dell'endpoint del chiamante.

### Chiamante che effettua una chiamata in uscita alla rete PSTN

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Endpoint dell'utente posizionato in un sito di rete abilitato per il routing in base alla posizione</th>
<th>Endpoint dell'utente posizionato in un sito di rete sconosciuto o non abilitato per il routing in base alla posizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Autorizzazione delle chiamate in uscita</p></td>
<td><p>Le chiamate vengono autorizzate in base ai criteri vocali dell'utente</p></td>
<td><p>Le chiamate vengono autorizzate in base ai criteri vocali dell'utente</p></td>
</tr>
<tr class="even">
<td><p>Routing della chiamata in uscita</p></td>
<td><p>La chiamata viene instradata in base ai criteri di routing vocale del sito di rete</p></td>
<td><p>La chiamata viene instradata in base ai criteri vocali dell'utente e solo tramite trunk non abilitati per il routing in base alla posizione (se disponibili)</p></td>
</tr>
</tbody>
</table>


## Vedere anche

#### Ulteriori risorse

[Scenari per il routing in base alla posizione in Lync Server 2013](lync-server-2013-scenarios-for-location-based-routing.md)

