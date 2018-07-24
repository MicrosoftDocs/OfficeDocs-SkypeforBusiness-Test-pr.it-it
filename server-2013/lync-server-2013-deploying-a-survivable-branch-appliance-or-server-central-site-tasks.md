---
title: 'Lync Server 2013: Distribuzione di Survivable Branch Appliance o Survivable Branch Server - Attività presso il sito centrale'
TOCTitle: Distribuzione di Survivable Branch Appliance o Survivable Branch Server - Attività presso il sito centrale
ms:assetid: 0f631a36-fc2e-41cd-8a0d-f27e84f4a89e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398189(v=OCS.15)
ms:contentKeyID: 49299695
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuzione di Survivable Branch Appliance o Survivable Branch Server con Lync Server 2013 - Attività presso il sito centrale

 

_**Ultima modifica dell'argomento:** 2012-10-18_

Le attività indicate in questa sezione devono essere eseguite presso il sito centrale. Se si sta distribuendo un Survivable Branch Server, saltare la prima attività.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Prima di eseguire le attività descritte in questa sezione, è necessario soddisfare le condizioni seguenti:<ul><li><p>Lync Server deve essere installato nel sito centrale.</p></li><li><p>Al gruppo RTCUniversalSBATechnicians deve essere aggiunto un tecnico addetto all'installazione presso il sito di succursale.</p></li></ul>
È inoltre consigliabile eseguire le operazioni seguenti:<ul><li><p>Distribuire un server DHCP in ogni sito di succursale per consentire ai client di ottenere gli indirizzi IP.</p></li><li><p>Come alternativa alla distribuzione di un server DHCP in ogni sito di succursale, abilitare DHCP di Lync Server nel Survivable Branch Appliance o nel Survivable Branch Server eseguendo il cmdlet <strong>Set-CsRegistrarConfiguration –EnableDHCPServer $true</strong> di Lync Server Management Shell. Per informazioni dettagliate, vedere la sezione dedicata ai requisiti hardware e software di <a href="lync-server-2013-branch-site-resiliency-requirements.md">Requisiti di resilienza dei siti di succursale per Lync Server 2013</a> nella documentazione relativa alla pianificazione.</p></li></ul></td>
</tr>
</tbody>
</table>


## Argomenti della sezione

  - [Aggiungere un Survivable Branch Appliance ad Active Directory in Lync Server 2013](lync-server-2013-add-a-survivable-branch-appliance-to-active-directory.md)

  - [Aggiungere siti di succursale alla topologia in Lync Server 2013](lync-server-2013-add-branch-sites-to-your-topology.md)

  - [Definire un Survivable Branch Appliance o un Survivable Branch Server in Lync Server 2013](lync-server-2013-define-a-survivable-branch-appliance-or-server.md)

