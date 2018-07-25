---
title: 'Lync Server 2013: Pianificazione della capacità per il parcheggio di chiamata'
TOCTitle: Pianificazione della capacità per il parcheggio di chiamata
ms:assetid: 75520310-760a-4b1b-bcc1-4d724d13f87a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg416493(v=OCS.15)
ms:contentKeyID: 49301003
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione della capacità per il parcheggio di chiamata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella tabella riportata di seguito viene descritto il modello utenti di Parcheggio di chiamata che è possibile utilizzare come base per i requisiti di pianificazione della capacità.

> [!important]  
> Si tenga presente che, per la pianificazione della capacità nelle situazioni di ripristino di emergenza, ciascun pool di una coppia di pool deve essere in grado di gestire carichi di lavoro per i servizi Parcheggio di chiamata in entrambi i pool.

### Modello utente del parcheggio di chiamata

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Metrica</th>
<th>Per ogni pool Front End (con 8 server Front End Server)</th>
<th>Per ogni server Standard Edition</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Frequenza di parcheggio</p></td>
<td><p>8 al minuto</p></td>
<td><p>1 al minuto</p></td>
</tr>
<tr class="even">
<td><p>Frequenza di recupero delle chiamate parcheggiate</p></td>
<td><p>8 al minuto</p></td>
<td><p>1 al minuto</p></td>
</tr>
<tr class="odd">
<td><p>Durata media del parcheggio</p></td>
<td><p>60 secondi</p></td>
<td><p>60 secondi</p></td>
</tr>
</tbody>
</table>

