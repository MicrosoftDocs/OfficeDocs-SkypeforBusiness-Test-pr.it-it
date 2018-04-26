---
title: 'Lync Server 2013: Piattaforme hardware server'
TOCTitle: Piattaforme hardware server
ms:assetid: c964c1c0-0153-472b-88ad-a38866e0df0c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398835(v=OCS.15)
ms:contentKeyID: 49301973
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Piattaforme hardware server per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

I ruoli del server di Lync Server 2013 e i computer che eseguono gli strumenti di amministrazione di Lync Server richiedono hardware a 64 bit.

L'hardware specifico utilizzato per la distribuzione di Lync Server 2013 può variare a seconda dei requisiti di dimensione e utilizzo. In questa sezione viene descritto l'hardware consigliato. Sebbene si tratti di suggerimenti e non di requisiti, l'utilizzo di hardware che non soddisfa tali indicazioni potrebbe generare rallentamenti significativi delle prestazioni e altri problemi.

## Piattaforma hardware consigliata

Per garantire prestazioni ottimali, è consigliabile eseguire Lync Server in server con componenti hardware che soddisfano i requisiti indicati nella tabella seguente. Se si utilizzano componenti hardware meno potenti, è possibile che si verifichino problemi funzionali o di prestazioni insufficienti. Si noti che questi requisiti hardware sono più elevati rispetto alle versioni precedenti di Lync Server, principalmente perché in Lync Server 2013 tutti i Front End Server eseguono SQL Server.


> [!NOTE]
> Il gruppo NIC è supportato e deve essere visibile a Lync Server. Per informazioni dettagliate, vedere <A href="http://go.microsoft.com/fwlink/p/?linkid=389910">Communications Server o Lync Server e il gruppo schede di rete</A>.



### Hardware consigliato per i server front-end, i server back-end, i server Standard Edition, i server Chat persistente, archivio della chat persistente e archivio di conformità della chat persistente (ruoli server back-end per il server Chat persistente)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente hardware</th>
<th>Scelta consigliata</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CPU</p></td>
<td><p>Processore doppio a 64 bit, hex-core, 2,26 GHz o superiore</p>
<p>I processori Intel Itanium non sono supportati per i ruoli del server di Lync Server.</p></td>
</tr>
<tr class="even">
<td><p>Memoria</p></td>
<td><p>32 gigabyte (GB)</p></td>
</tr>
<tr class="odd">
<td><p>Disco</p></td>
<td><ul>
<li><p>Otto o più unità disco rigido da 10.000 RPM con almeno 72 GB di spazio libero su disco</p>
<p>Due dei dischi dovrebbero utilizzare RAID 1 e sei dovrebbero utilizzare RAID 10.</p>
<p>-OPPURE-</p></li>
<li><p>Unità SSD (Solid State Drive) con prestazioni simili a otto unità disco meccanico da 10.000 RPM.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Rete</p></td>
<td><ul>
<li><p>Una scheda di rete dual port, 1 Gbps o superiore (due consigliate, da associare a un singolo indirizzo MAC e a un singolo indirizzo IP)</p></li>
</ul></td>
</tr>
</tbody>
</table>


### Hardware consigliato per server perimetrali, Mediation Server autonomi e server Director

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente hardware</th>
<th>Scelta consigliata</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CPU</p></td>
<td><ul>
<li><p>Processore doppio a 64 bit, quad-core, 2,0 GHz o superiore</p>
<p>-OPPURE-</p></li>
<li><p>Processore a 4 vie, a 64 bit, dual-core, 2.0 GHz o superiore</p></li>
</ul>
<p>I processori Intel Itanium non sono supportati per i ruoli del server di Lync Server.</p></td>
</tr>
<tr class="even">
<td><p>Memoria</p></td>
<td><p>16 gigabyte (GB)</p></td>
</tr>
<tr class="odd">
<td><p>Disco</p></td>
<td><ul>
<li><p>Quattro o più unità disco rigido da 10.000 RPM con almeno 72 GB di spazio libero su disco</p>
<p>I dischi dovrebbero presentare una configurazione 2x RAID 1.</p>
<p>-OPPURE-</p></li>
<li><p>Unità SSD (Solid State Drive) con prestazioni simili a quattro unità disco meccanico da 10.000 RPM.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Rete</p></td>
<td><ul>
<li><p>Una scheda di rete dual port, 1 Gbps o superiore (due consigliate, da associare a un singolo indirizzo MAC e a un singolo indirizzo IP)</p></li>
</ul></td>
</tr>
</tbody>
</table>

