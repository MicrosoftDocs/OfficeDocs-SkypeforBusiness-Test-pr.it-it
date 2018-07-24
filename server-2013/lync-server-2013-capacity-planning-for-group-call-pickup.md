---
title: Pianificazione della capacità per la risposta alle chiamate di gruppo
TOCTitle: Pianificazione della capacità per la risposta alle chiamate di gruppo
ms:assetid: 0d654a19-6cf0-4118-903d-ec2c4e519253
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ984297(v=OCS.15)
ms:contentKeyID: 52062093
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione della capacità per la risposta alle chiamate di gruppo

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella tabella seguente viene descritto il modello utente della funzionalità di risposta alle chiamate di gruppo che è possibile utilizzare come base per i requisiti di pianificazione della capacità.

> [!important]  
> La risposta alle chiamate di gruppo si basa sull'applicazione Parcheggio di chiamata. Tenere presente che, per la pianificazione della capacità di ripristino di emergenza, ciascun pool di una coppia di pool deve essere in grado di gestire i carichi di lavoro per i servizi di Parcheggio di chiamata, inclusa la risposta alle chiamate di gruppo, in entrambi i pool.

### Modello utente della risposta alle chiamate di gruppo

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Metrica</th>
<th>Per ogni pool Front End (con 8 server front-end)</th>
<th>Per ogni server Standard Edition</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Numero consigliato di utenti per gruppo</p></td>
<td><p>50</p></td>
<td><p>50</p></td>
</tr>
<tr class="even">
<td><p>Numero di gruppi consigliato</p></td>
<td><p>500</p></td>
<td><p>60</p></td>
</tr>
<tr class="odd">
<td><p>Numero massimo di utenti per pool abilitato alla risposta alle chiamate di gruppo</p></td>
<td><p>25.000</p></td>
<td><p>3.000</p></td>
</tr>
<tr class="even">
<td><p>Frequenza massima di chiamate in arrivo agli utenti totali abilitati per la risposta alle chiamate di gruppo per pool per minuto</p></td>
<td><p>500</p></td>
<td><p>60</p></td>
</tr>
<tr class="odd">
<td><p>Frequenza massima di chiamate recuperate dagli utenti con la funzionalità di risposta alle chiamate di gruppo per pool per minuto</p></td>
<td><p>200</p></td>
<td><p>25</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> <UL>
> 
> 
> 
> <li>
> <P>Per i pool Front End con meno di otto Front End Server, calcolare la metrica in modo lineare. Ad esempio, se il pool Front End dispone di un Front End Server, calcolare il carico massimo come 1/8 dei valori mostrati nella tabella.</P>
> 
> 
> 
> <li>
> <P>È possibile diminuire o aumentare il numero consigliato di utenti per gruppo e il numero di gruppi purché non si superi il numero massimo di utenti per pool. Ad esempio, il server Standard Edition può disporre di 120 gruppi con 25 utenti per gruppo perché il numero di utenti abilitati per la risposta alla chiamata di gruppo non supera il numero massimo del modello utente (120 gruppi per 25 utenti significa 3.000 utenti abilitati per la risposta alle chiamate di gruppo).</P></LI></UL>


