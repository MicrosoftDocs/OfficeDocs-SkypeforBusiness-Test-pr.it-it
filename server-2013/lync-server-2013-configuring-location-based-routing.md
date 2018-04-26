---
title: 'Lync Server 2013: Configurazione del routing in base alla posizione'
TOCTitle: Configurazione del routing in base alla posizione
ms:assetid: 63cdc474-e80f-43b1-a237-9d9ed673300a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994036(v=OCS.15)
ms:contentKeyID: 52062171
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione del routing in base alla posizione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il routing in base alla posizione di Lync Server 2013 CU1 è una funzionalità di VoIP aziendale. Il routing in base alla posizione è una funzionalità di gestione delle chiamate che controlla il routing delle chiamate da parte di Lync Server 2013 CU1. Applica le limitazioni sul routing delle chiamate a destinazioni PBX o PSTN in base alla posizione del chiamante di Lync. Il routing in base alla posizione applica regole di autorizzazione delle chiamate alle chiamate PSTN che dipendono dalla posizione in rete del chiamante. Tale posizione viene determinata in base al sito di rete associato alla subnet di rete a cui è connesso il chiamante. La configurazione del routing in base alla posizione richiede innanzitutto la distribuzione di VoIP aziendale, quindi la configurazione delle aree, dei siti e delle subnet di rete. In questo modo si creano i presupposti per abilitare il routing in base alla posizione.

Prima di distribuire il routing in base alla posizione, è necessario distribuire VoIP aziendale e configurare le aree, i siti e le subnet di rete associate ai siti di rete. Al termine, è possibile configurare il routing in base alla posizione. Per la procedura di configurazione delle aree, dei siti e delle subnet di rete, vedere [Distribuzione delle funzionalità di VoIP aziendale avanzate in Lync Server 2013](lync-server-2013-deploying-advanced-enterprise-voice-features.md)

In questa sezione viene illustrata la configurazione del routing in base alla posizione con un esempio.

![Esempio di routing in base alla posizione di VoIP aziendale](images/JJ994036.b6ef5afc-36ac-406f-8ec2-a87532b20612(OCS.15).png "Esempio di routing in base alla posizione di VoIP aziendale")

  
La tabella seguente include gli utenti definiti in questo esempio.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di endpoint</th>
<th>Posizione</th>
<th>Utenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync</p></td>
<td><p>Ufficio di Delhi</p></td>
<td><p>DEL-LYNC-1,DEL-LYNC-2,DEL-LYNC-3</p></td>
</tr>
<tr class="even">
<td><p>Lync</p></td>
<td><p>Ufficio di Hyderabad</p></td>
<td><p>HYD-LYNC-1, HYD-LYNC-2, HYD-LYNC-3</p></td>
</tr>
<tr class="odd">
<td><p>Lync</p></td>
<td><p>Sconosciuta (ad esempio un hotel)</p></td>
<td><p>UNK-LYNC-1</p></td>
</tr>
<tr class="even">
<td><p>PBX</p></td>
<td><p>Ufficio di Delhi</p></td>
<td><p>DEL-PBX-1, DEL-PBX-2</p></td>
</tr>
<tr class="odd">
<td><p>PBX</p></td>
<td><p>Ufficio di Hyderabad</p></td>
<td><p>HYD-PBX-1, HYD-PBX-2</p></td>
</tr>
<tr class="even">
<td><p>PSTN</p></td>
<td><p>Sconosciuta</p></td>
<td><p>PSTN-1, PSTN-2, PSTN-3</p></td>
</tr>
</tbody>
</table>

  

Nella tabella seguente sono rappresentati tutti i sistemi illustrati in questo ambiente di esempio.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Sistema</th>
<th>Posizione</th>
<th>Nome</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Pool di Lync Server 2013 CU1</p></td>
<td><p>qualsiasi</p></td>
<td><p>LS-PL1</p></td>
</tr>
<tr class="even">
<td><p>Lync Server 2013 CU1, Mediation Server</p></td>
<td><p>qualsiasi</p></td>
<td><p>MS-PL1</p></td>
</tr>
<tr class="odd">
<td><p>Gateway PSTN 1</p></td>
<td><p>Delhi</p></td>
<td><p>DEL-GW</p></td>
</tr>
<tr class="even">
<td><p>Gateway PSTN 2</p></td>
<td><p>Hyderabad</p></td>
<td><p>HYD-GW</p></td>
</tr>
<tr class="odd">
<td><p>PBX 1</p></td>
<td><p>Delhi</p></td>
<td><p>DEL-PBX</p></td>
</tr>
<tr class="even">
<td><p>PBX 2</p></td>
<td><p>Hyderabad</p></td>
<td><p>RED-PBX</p></td>
</tr>
</tbody>
</table>


## Argomenti della sezione

  - [Configurazione di VoIP aziendale in Lync Server 2013](lync-server-2013-configuring-enterprise-voice.md)

  - [Implementazione di aree di rete, siti di rete e subnet in Lync Server 2013](lync-server-2013-deploying-network-regions-sites-and-subnets.md)

  - [Abilitazione del routing in base alla posizione in Lync Server 2013](lync-server-2013-enabling-location-based-routing.md)

## Vedere anche

#### Ulteriori risorse

[Distribuzione delle funzionalità di VoIP aziendale avanzate in Lync Server 2013](lync-server-2013-deploying-advanced-enterprise-voice-features.md)

