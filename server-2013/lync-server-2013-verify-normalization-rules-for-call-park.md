---
title: 'Lync Server 2013: Verificare le regole di normalizzazione per il parcheggio di chiamata'
TOCTitle: Verificare le regole di normalizzazione per il parcheggio di chiamata
ms:assetid: deaa170f-041e-45cb-8eab-f02931ab541e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398981(v=OCS.15)
ms:contentKeyID: 49302195
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verificare le regole di normalizzazione per il parcheggio di chiamata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-11_

I codici orbit di Parcheggio di chiamata non devono essere normalizzati. Controllare i dial plan per verificare che i codici orbit non siano normalizzati. Se è necessario creare un'ulteriore regola di normalizzazione per evitare che i codici orbit vengano normalizzati, seguire la procedura illustrata in [Creare un dial plan in Lync Server 2013](lync-server-2013-create-a-dial-plan.md) per definire una nuova regola di normalizzazione, ad esempio che **Sequenza per la corrispondenza** identifichi l'intervallo di codici orbit e che **Formato di conversione** sia uguale a **$1**. Se ad esempio l'intervallo di codici orbit di Parcheggio di chiamata è 7000 - 7999, il valore di **Sequenza per la corrispondenza** sarà **^(7\\d{3})$** e il valore di **Formato di conversione** sarà **$1**.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Assicurarsi che la regola di normalizzazione predefinita nei dial plan non contenga <strong>^(\d*)</strong>. In caso contrario, la regola di normalizzazione Parcheggio di chiamata non verrà mai eseguita.</td>
</tr>
</tbody>
</table>


## Vedere anche

#### Attività

[Creare un dial plan in Lync Server 2013](lync-server-2013-create-a-dial-plan.md)

