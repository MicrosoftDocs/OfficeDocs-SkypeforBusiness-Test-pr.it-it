---
title: 'Lync Server 2013: Trasferimento e inoltro di chiamata'
TOCTitle: Trasferimento e inoltro di chiamata
ms:assetid: 978610ec-63c7-4cf6-ad7a-9ef91559bf12
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994051(v=OCS.15)
ms:contentKeyID: 52062202
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Trasferimento e inoltro di chiamata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Quando è interessato un endpoint PSTN, il routing in base alla posizione analizza la posizione dell'endpoint del chiamante e l'endpoint a cui verrà trasferita o inoltrata la chiamata (destinazione di trasferimento/inoltro). Determina quindi se la chiamata deve essere trasferita o inoltrata a seconda della posizione di entrambi gli endpoint.

Nella tabella seguente è illustrato lo scenario di un utente Lync impegnato in una chiamata a un endpoint PSTN che trasferisce la chiamata a un altro utente Lync. A seconda della posizione del sito di rete dell'endpoint di destinazione del trasferimento, il routing in base alla posizione influisce sul trasferimento o sull'inoltro della chiamata.

### Avvio del trasferimento o dell'inoltro della chiamata

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Utente che avvia il trasferimento o l'inoltro della chiamata</th>
<th>L'endpoint di destinazione si trova nello stesso sito di rete dell'utente che avvia il trasferimento o l'inoltro della chiamata</th>
<th>L'endpoint di destinazione si trova in uno sito di rete diverso rispetto a quello dell'utente che avvia il trasferimento o l'inoltro della chiamata</th>
<th>L'endpoint di destinazione si trova in un sito di rete sconosciuto o non abilitato per il routing in base alla posizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utente Lync</p></td>
<td><p>L'inoltro o il trasferimento della chiamata è consentito</p></td>
<td><p>L'inoltro o il trasferimento della chiamata non è consentito</p></td>
<td><p>L'inoltro o il trasferimento della chiamata non è consentito</p></td>
</tr>
</tbody>
</table>

  

Esempio: un utente Lync impegnato in una chiamata a un endpoint PSTN trasferisce la chiamata a un altro utente Lync nello stesso sito di rete. In questo caso il trasferimento della chiamata è consentito.

Nella tabella seguente è illustrato lo scenario in cui uno di due utenti Lync impegnati in una chiamata trasferisce la chiamata a un endpoint PSTN. A seconda della posizione dell'utente a cui viene trasferita la chiamata, nella tabella viene descritto l'impatto del routing in base alla posizione sulla chiamata.

### Trasferimento o inoltro della chiamata all'endpoint PSTN

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Destinazione dell'endpoint del trasferimento o dell'inoltro della chiamata</th>
<th>Utenti Lync nello stesso sito di rete</th>
<th>Utenti Lync in siti di rete diversi</th>
<th>Uno o più utenti Lync in un sito di rete sconosciuto o non abilitato per il routing in base alla posizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Endpoint PSTN</p></td>
<td><p>Inoltro o trasferimento di chiamata consentito dai criteri di routing vocale del sito dell'utente trasferito</p></td>
<td><p>Inoltro o trasferimento di chiamata consentito dai criteri di routing vocale del sito dell'utente trasferito</p></td>
<td><p>Inoltro o trasferimento di chiamata consentito dai criteri vocali dell'utente trasferito solo tramite trunk non abilitati per il routing in base alla posizione</p></td>
</tr>
</tbody>
</table>

  
Esempio: uno di due utenti Lync impegnati in una chiamata e nella stesso sito di rete trasferisce la chiamata a un endpoint PSTN. In questo caso il trasferimento della chiamata è consentito.

## Vedere anche

#### Ulteriori risorse

[Scenari per il routing in base alla posizione in Lync Server 2013](lync-server-2013-scenarios-for-location-based-routing.md)

