---
title: 'Lync Server 2013: Requisiti hardware e software per il server Director'
TOCTitle: Requisiti hardware e software per il server Director
ms:assetid: 747b701e-7f97-46fe-91c5-1e8d9addf9f7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398560(v=OCS.15)
ms:contentKeyID: 49300986
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti hardware e software per il server Director in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questa sezione sono incluse informazioni dettagliate sui requisiti hardware e software per il Server Directore sugli scenari di collocazione supportati per il Server Director.

## Requisiti hardware per il Server Director

Nella tabella seguente sono elencati i requisiti hardware per i Server Director:

### Requisiti hardware per il server Director

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente hardware</th>
<th>Requisito minimo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CPU</p></td>
<td><ul>
<li><p>Processore a 64 bit, quad-core, 2.0 GHz o superiore</p></li>
<li><p>Processore doppio a 64 bit, dual-core, 2.0 GHz o superiore</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Memoria</p></td>
<td><p>4 gigabyte (GB)</p></td>
</tr>
<tr class="odd">
<td><p>Disco</p></td>
<td><ul>
<li><p>Unità disco rigido 10K RPM (HDD)</p></li>
<li><p>Unità SSD (Solid State Drive) ad alte prestazioni, equivalenti o superiori rispetto alle unità disco rigido 10K RPM HDD</p></li>
<li><p>Dischi 2x RAID 10 (con striping e mirroring) 15K RPM per file di dati del database</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Rete</p></td>
<td><ul>
<li><p>Scheda di rete doppia a 1 gigabit al secondo (Gbps) (consigliata)</p></li>
<li><p>Scheda di rete singola a 1 Gbps (supportata)</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Requisiti software per il Server Director

Il ruolo del Server Director può essere distribuito solo in server che eseguono Lync Server 2013 Enterprise Edition.

È necessario uno dei sistemi operativi a 64 bit seguenti per Director:

  - Sistema operativo Windows Server 2008 R2 Standard con Service Pack 1

  - Sistema operativo Windows Server 2008 R2 Enterprise con Service Pack 1

  - Sistema operativo Windows Server 2008 R2 Datacenter con Service Pack 1

  - Sistema operativo Windows Server 2012 Standard

  - Sistema operativo Windows Server 2012 Datacenter

Per Lync Server 2013 è inoltre richiesta l'installazione dei programmi e degli aggiornamenti menzionati nell'argomento [Requisiti e supporto per i server aggiuntivi in Lync Server 2013](lync-server-2013-additional-server-support-and-requirements.md).

## Collocazione supportata

Il ruolo del server Server Director non può essere distribuito nella stessa posizione di alcun altro ruolo del server in Lync Server 2013. Tuttavia, se non si distribuisce un Server Director, il ruolo sarà assunto dal Front End Server.

