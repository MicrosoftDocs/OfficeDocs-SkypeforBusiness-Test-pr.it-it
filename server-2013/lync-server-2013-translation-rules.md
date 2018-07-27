---
title: 'Lync Server 2013: Regole di conversione'
TOCTitle: Regole di conversione
ms:assetid: 6e067bd4-4931-4385-81ac-2acae45a16d8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398520(v=OCS.15)
ms:contentKeyID: 49300908
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Regole di conversione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Lync Server 2013 di VoIP aziendale richiede che tutte le stringhe di composizione siano normalizzate nel formato E.164 ai fini dell'esecuzione della ricerca inversa di numeri. In Microsoft Lync Server 2010, le regole di traduzione sono supportate solo per i numeri chiamati. Queste regole, nuove in Microsoft Lync Server 2013, sono supportate anche per i numeri che chiamano. Il *trunk peer* ovvero il gateway, il centralino (PBX) o il trunk SIP associato, potrebbe richiedere l'utilizzo del formato di composizione locale per i numeri. Per convertire i numeri dal formato E.164 a quello locale, è possibile definire una o più regole di conversione per modificare l'URI richiesta prima di eseguirne il routing al trunk peer. È possibile, ad esempio, scrivere una regola di conversione per rimuovere +44 dall'inizio di una stringa di composizione e sostituirlo con 0144.

Eseguendo la conversione della route in uscita nel server, è possibile ridurre i requisiti di configurazione in ogni singolo trunk peer per tradurre i numeri di telefono in un formato di composizione locale. Nel pianificare quali e quanti gateway associare a un cluster di Mediation Server specifico, può essere utile raggruppare i trunk peer con requisiti di composizione locali simili in modo da ridurre il numero di regole di conversione necessarie e il tempo richiesto per scriverle.

> [!IMPORTANT]  
> L'associazione di una o più regole di conversione a una configurazione trunk VoIP aziendale può essere utilizzata come alternativa alla configurazione di regole di conversione nel trunk peer. Non associare regole di conversione a una configurazione trunk VoIP aziendale se sono state configurate regole di conversione nel trunk peer, perché le due regole potrebbero creare conflitti.

## Esempi di regole di traduzione

Gli esempi di regole di traduzione seguenti indicano come sviluppare regole nel server per convertire numeri dal formato E.164 a un formato locale per il trunk peer.

Per informazioni dettagliate su come implementare le regole di conversione, vedere [Definizione delle regole di conversione in Lync Server 2013](lync-server-2013-defining-translation-rules.md) nella documentazione relativa alla distribuzione.


<table>
<colgroup>
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
</colgroup>
<thead>
<tr class="header">
<th>Descrizione</th>
<th>Cifre iniziali</th>
<th>Lunghezza</th>
<th>Cifre da rimuovere</th>
<th>Cifre da aggiungere</th>
<th>Formato corrispondente</th>
<th>Conversione</th>
<th>Esempio</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Composizione convenzionale di interurbane negli Stati Uniti</p>
<p>(rimuovere il '+')</p></td>
<td><p>+1</p></td>
<td><p>Esattamente 12</p></td>
<td><p>1</p></td>
<td><p>0</p></td>
<td><p>^\+(1\d{10})$</p></td>
<td><p>$1</p></td>
<td><p>+14255551010 diventa 14255551010</p></td>
</tr>
<tr class="even">
<td><p>Composizione di interurbane internazionali negli Stati Uniti</p>
<p>(rimuovere il '+' e aggiungere 011)</p></td>
<td><p>+</p></td>
<td><p>Almeno 11</p></td>
<td><p>1</p></td>
<td><p>011</p></td>
<td><p>^\+(\d{9}\d+)$</p></td>
<td><p>011$1</p></td>
<td><p>+441235551010 diventa 011441235551010</p></td>
</tr>
</tbody>
</table>

