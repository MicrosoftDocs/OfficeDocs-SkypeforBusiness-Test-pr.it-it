---
title: 'Lync Server 2013: Pianificazione della capacità per Response Group'
TOCTitle: Pianificazione della capacità per Response Group
ms:assetid: a2459a69-1f45-4f2f-bca5-d4f442708e44
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412754(v=OCS.15)
ms:contentKeyID: 49301515
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione della capacità per Response Group in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella tabella riportata di seguito viene descritto il modello utenti di Response Group che è possibile utilizzare come base per i requisiti di pianificazione della capacità.


> [!NOTE]
> I numeri nella tabella seguente presuppongono l'utilizzo di file Wave (con estensione wav) a 16 bit, 16 kHz, mono per tutti i file audio Response Group. Se si utilizzano altri formati, ad esempio Windows Media Audio ( con estensione wma), i numeri possono variare.



> [!IMPORTANT]  
> Tenere presente che, per la pianificazione della capacità per il ripristino di emergenza, ogni pool di un pool accoppiato deve poter gestire i carichi di lavoro per tutti i Response Group in entrambi i pool.

### Modello utente Response Group

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Metrica</th>
<th>Per pool Enterprise Edition (con 8 Front End Server)</th>
<th>Per server Standard Edition</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Chiamate in entrata al secondo</p></td>
<td><p>16</p></td>
<td><p>2</p></td>
</tr>
<tr class="even">
<td><p>Chiamate simultanee connesse a IVR o MoH</p></td>
<td><p>480</p></td>
<td><p>60</p></td>
</tr>
<tr class="odd">
<td><p>Sessioni anonime simultanee (senza messaggistica istantanea)</p></td>
<td><p>224</p></td>
<td><p>28</p></td>
</tr>
<tr class="even">
<td><p>Sessioni anonime simultanee (con messaggistica istantanea)</p></td>
<td><p>64</p></td>
<td><p>8</p></td>
</tr>
<tr class="odd">
<td><p>Agenti attivi (formali e informali)</p></td>
<td><p>1200</p></td>
<td><p>1200</p></td>
</tr>
<tr class="even">
<td><p>Numero di gruppi di risposta</p></td>
<td><p>400</p></td>
<td><p>400</p></td>
</tr>
<tr class="odd">
<td><p>Numero di gruppi IVR (utilizzo del riconoscimento vocale)</p></td>
<td><p>200</p></td>
<td><p>200</p></td>
</tr>
</tbody>
</table>

