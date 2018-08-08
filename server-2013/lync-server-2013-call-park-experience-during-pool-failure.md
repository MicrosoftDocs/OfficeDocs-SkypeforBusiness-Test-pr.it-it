---
title: "Lync Server 2013: Esperienza del parcheggio durante un errore del pool"
TOCTitle: Esperienza del parcheggio di chiamata durante un errore del pool
ms:assetid: f6303e69-8771-492a-9e8b-c3d7ba231309
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205383(v=OCS.15)
ms:contentKeyID: 49302479
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Esperienza del parcheggio di chiamata in Lync Server 2013 durante un errore del pool

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Quando un pool Front End non è disponibile a causa di un evento imprevisto, le chiamate che sono state parcheggiate, ma non sono ancora state recuperate, vengono interrotte. Durante l'esecuzione di un failover in un pool di backup, gli utenti vengono reindirizzati al pool di backup e sono in modalità di resilienza. In modalità di resilienza gli utenti non possono parcheggiare le chiamate, ma possono mettere le chiamate in attesa e trasferirle. Completato il failover, è possibile parcheggiare nuovamente le chiamate e recuperarle normalmente. Durante il failback, gli utenti non possono parcheggiare le chiamate finché non sono usciti dalla modalità di resilienza.

Durante il ripristino di emergenza gli utenti che sono stati reindirizzati al pool di backup durante il processo di failover, utilizzano l' applicazione Parcheggio di chiamata distribuita nel pool di backup. Pertanto, gli utenti reindirizzati al pool di backup utilizzano le impostazioni del parcheggio di chiamata configurate per l' applicazione Parcheggio di chiamata nel pool di backup.

Nella tabella seguente viene riepilogata l'esperienza di Parcheggio di chiamata nelle varie fasi di ripristino di emergenza.

### Esperienza utente durante il ripristino di emergenza

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Stato chiamata</th>
<th>In caso di guasto</th>
<th>Durante il failover</th>
<th>Durante il failback</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Chiamata non ancora parcheggiata</p></td>
<td><p>La chiamata rimane connessa, ma non può essere parcheggiata.</p></td>
<td><ul>
<li><p>Durante il failover non è possibile parcheggiare la chiamata mentre gli utenti sono in modalità di resilienza, ma è possibile metterla in attesa e trasferirla.</p></li>
<li><p>Completato il failover, è possibile parcheggiare e recuperare la chiamata.</p></li>
</ul></td>
<td><ul>
<li><p>Durante il failback non è possibile parcheggiare la chiamata mentre gli utenti sono in modalità di resilienza, ma è possibile metterla in attesa e trasferirla.</p></li>
<li><p>Completato il failback, è possibile parcheggiare e recuperare la chiamata.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Chiamata parcheggiata, ma non ancora recuperata</p></td>
<td><p>La chiamata viene interrotta.</p></td>
<td><p>Nessuna chiamata in questo stato.</p></td>
<td><p>La chiamata resta parcheggiata.</p></td>
</tr>
<tr class="odd">
<td><p>Chiamata parcheggiata già recuperata</p></td>
<td><p>Le chiamate restano connesse.</p></td>
<td><p>Le chiamate restano connesse.</p></td>
<td><p>Le chiamate restano connesse.</p></td>
</tr>
</tbody>
</table>

