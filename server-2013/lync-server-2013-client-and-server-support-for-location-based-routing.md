---
title: 'Lync Server 2013: Supporto per client e server per il routing in base alla posizione'
TOCTitle: Supporto per client e server per il routing in base alla posizione
ms:assetid: 26c2ca3d-026d-4dd7-94fa-15ebb4406953
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994024(v=OCS.15)
ms:contentKeyID: 52062115
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supporto per client e server per il routing in base alla posizione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il routing in base alla posizione è applicato da Lync Server. Lync Server è in grado di identificare i siti di rete da cui si connettono gli utenti all'interno della rete aziendale. Poiché gli utenti remoti si trovano all'esterno della rete aziendale, la relativa posizione viene considerata come sconosciuta.

## Supporto per Lync Server

Per il routing in base alla posizione, è necessario distribuire Lync Server 2013 CU1 in tutti i pool Front End e i server Standard Edition in una determinata topologia. Se Lync Server 2013 CU1 non è installato in determinati componenti della topologia, le restrizioni del routing in base alla posizione non possono essere applicate completamente.

Nella tabella seguente è illustrata la combinazione dei ruoli del server e delle versioni supportati per il routing in base alla posizione.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Versione pool</th>
<th>versione Mediation Server</th>
<th>Supportato</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aggiornamento cumulativo per Lync Server 2013 - Febbraio 2013</p></td>
<td><p>Aggiornamento cumulativo per Lync Server 2013 - Febbraio 2013</p></td>
<td><p>sì</p></td>
</tr>
<tr class="even">
<td><p>Aggiornamento cumulativo per Lync Server 2013 - Febbraio 2013</p></td>
<td><p>Lync Server 2013</p></td>
<td><p>no</p></td>
</tr>
<tr class="odd">
<td><p>Aggiornamento cumulativo per Lync Server 2013 - Febbraio 2013</p></td>
<td><p>Lync Server 2010</p></td>
<td><p>no</p></td>
</tr>
<tr class="even">
<td><p>Aggiornamento cumulativo per Lync Server 2013 - Febbraio 2013</p></td>
<td><p>Office Communications Server 2007 R2</p></td>
<td><p>no</p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013</p></td>
<td><p>qualsiasi</p></td>
<td><p>no</p></td>
</tr>
<tr class="even">
<td><p>Lync Server 2010</p></td>
<td><p>qualsiasi</p></td>
<td><p>no</p></td>
</tr>
<tr class="odd">
<td><p>Office Communications Server 2007 R2</p></td>
<td><p>qualsiasi</p></td>
<td><p>no</p></td>
</tr>
</tbody>
</table>


## Supporto per client Lync

Nella tabella seguente sono riportati i client supportati dal routing in base alla posizione.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di client</th>
<th>Supportato</th>
<th>Dettagli</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync 2013</p></td>
<td><p>sì</p></td>
<td><p>Incluso aggiornamento cumulativo per Lync 2013 - Febbraio 2013</p></td>
</tr>
<tr class="even">
<td><p>Lync 2010</p></td>
<td><p>sì</p></td>
<td> </td>
</tr>
<tr class="odd">
<td><p>Office Communicator 2007 R2</p></td>
<td><p>no</p></td>
<td> </td>
</tr>
<tr class="even">
<td><p>Lync Phone Edition</p></td>
<td><p>sì</p></td>
<td> </td>
</tr>
<tr class="odd">
<td><p>Lync Attendant</p></td>
<td><p>sì</p></td>
<td> </td>
</tr>
<tr class="even">
<td><p>Lync per Windows 8</p></td>
<td><p>no</p></td>
<td> </td>
</tr>
<tr class="odd">
<td><p>Lync Mobile 2013</p></td>
<td><p>no</p></td>
<td><p>Per i client di Lync Mobile 2013, la funzionalità VoIP deve essere disabilitata per gli utenti con il routing in base alla posizione abilitato.</p></td>
</tr>
<tr class="even">
<td><p>Lync Mobile 2010</p></td>
<td><p>sì</p></td>
<td> </td>
</tr>
</tbody>
</table>

  


> [!NOTE]
> Per disabilitare la funzionalità VoIP per i client di Lync Mobile 2013, assegnare un criterio dei dispositivi mobili con l'impostazione Abilita audio/video IP disabilitata per tutti gli utenti per i quali è abilitato il routing in base alla posizione. Per ulteriori dettagli sui criteri dei dispositivi mobili, vedere <A href="new-csmobilitypolicy.md">New-CsMobilityPolicy</A>.



## Vedere anche

#### Ulteriori risorse

[Pianificazione del routing in base alla posizione in Lync Server 2013](lync-server-2013-planning-for-location-based-routing.md)

