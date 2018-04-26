---
title: 'Lync Server 2013: Testare il routing vocale'
TOCTitle: Testare il routing vocale
ms:assetid: d3aae909-fef6-440f-b144-0b62dc82bf5d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398915(v=OCS.15)
ms:contentKeyID: 49302086
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Testare il routing vocale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-24_

È possibile utilizzare la scheda **Test routing vocale** del Pannello di controllo di Lync Server per configurare gli scenari di test case. Per definire un test case, specificare il dial plan, il criterio vocale, l'utilizzo PSTN e la route vocale in base ai quali testare un numero di telefono specificato.

Prima di distribuire la configurazione del routing vocale, è consigliabile testarla su diversi numeri di telefono per assicurarsi che i risultati siano quelli previsti.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>È possibile utilizzare i comandi <strong>Esporta test case</strong> e <strong>Importa test case</strong> per salvare i test case del routing vocale e importarli per l'uso su un altro computer.</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/JJ205186.Caution(OCS.15).gif" title="Caution" alt="Caution" />Attenzione:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Se si elimina una parte della configurazione del routing vocale, ad esempio un dial plan, un criterio vocale, una route vocale o un utilizzo del telefono, è necessario controllare e aggiornare i test case del routing vocale. Il Pannello di controllo di Lync Server non invia un avviso agli utenti quando i test case non sono più validi a causa delle modifiche apportate alle configurazioni.</td>
</tr>
</tbody>
</table>


## Argomenti della sezione

  - [Creare un test case di routing vocale in Lync Server 2013](lync-server-2013-create-a-voice-routing-test-case.md)

  - [Esportare test case di routing vocale in Lync Server 2013](lync-server-2013-export-voice-routing-test-cases.md)

  - [Importare test case di routing vocale in Lync Server 2013](lync-server-2013-import-voice-routing-test-cases.md)

  - [Esecuzione di test del routing vocale in Lync Server 2013](lync-server-2013-running-voice-routing-tests.md)

