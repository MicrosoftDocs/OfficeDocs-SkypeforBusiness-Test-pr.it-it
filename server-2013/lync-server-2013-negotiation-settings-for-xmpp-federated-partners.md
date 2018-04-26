---
title: 'Lync Server 2013: Impostazioni di negoziazione per i partner federati XMPP'
TOCTitle: Impostazioni di negoziazione per i partner federati XMPP
ms:assetid: ef773942-ef92-4f71-85a1-738dfebdfa00
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ552456(v=OCS.15)
ms:contentKeyID: 49302412
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Impostazioni di negoziazione per i partner federati XMPP in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Le impostazioni per i tipi di negoziazione nella configurazione di un Partner XMPP offrono un'ampia gamma di possibili combinazioni. Non tutte le combinazioni sono valide. Nella tabella illustrata in questo argomento vengono elencate le impostazioni valide e quelle non valide. Le configurazioni più comuni sono presentate nella prima tabella, mentre la seconda tabella contiene tutte le possibili combinazioni. Si noti che non è possibile avere SASL *(Simple Authentication and Security Layer)* **a meno che** TLS *(Transport Layer Security)* non sia anch'esso disponibile. SASL viene inviato in un formato non crittografato (leggibile) e non dovrebbe mai essere trasmesso se non viene protetto in altro modo, ad esempio con TLS.

### Metodi comuni di negoziazione per la federazione XMPP

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>TLS (Transport Layer Security)</th>
<th>SASL (Simple Authentication and Security Layer)</th>
<th>Autenticazione dialback</th>
<th>Metodi di autenticazione previsti</th>
<th>Note</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Obbligatorio</p></td>
<td><p>Obbligatorio</p></td>
<td><p>False</p></td>
<td><p>SASL su TLS</p></td>
<td><p>L'obbligatorietà di TLS e SASL aiuta ad assicurare la protezione del flusso di messaggi SASL. Il dialback non è disponibile e non può essere utilizzato come metodo di fallback se il partner federato XMPP non ha impostato TLS su obbligatorio o facoltativo.</p></td>
</tr>
<tr class="even">
<td><p>Obbligatorio</p></td>
<td><p>Facoltativo</p></td>
<td><p>True</p></td>
<td><p>SASL su TLS, dialback TLS, dialback TCP</p></td>
<td><p>Impostando TLS come obbligatorio, se il partner federato XMPP ha impostato SASL su facoltativo o su obbligatorio, viene utilizzato SASL. Se SASL non è disponibile, verrà utilizzato il dialback su TLS.</p></td>
</tr>
<tr class="odd">
<td><p>Facoltativo</p></td>
<td><p>Facoltativo</p></td>
<td><p>True</p></td>
<td><p>SASL su TLS, dialback TLS, dialback TCP</p></td>
<td><p>Molto flessibili nel metodo di negoziazione offerto, queste impostazioni si avvalgono delle impostazioni dei partner della federazione XMPP. Se TLS è facoltativo o obbligatorio per il partner ma SASL non è supportato, sarà disponibile il dialback TLS. Se TLS e SASL sono impostati su facoltativo o obbligatorio per il partner, viene utilizzata la selezione ottimale di TLS su SASL.</p></td>
</tr>
<tr class="even">
<td><p>Non supportato</p></td>
<td><p>Non supportato</p></td>
<td><p>True</p></td>
<td><p>Dialback TCP</p></td>
<td><p>In molti casi il dialback TCP è l'unica soluzione possibile. Meno desiderabile di altre opzioni, offre comunque un buon grado di attendibilità.</p></td>
</tr>
</tbody>
</table>


### Matrice dei metodi di negoziazione per la federazione XMPP - Completa

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>TLS (Transport Layer Security)</th>
<th>SASL (Simple Authentication and Security Layer)</th>
<th>Autenticazione dialback</th>
<th>Metodo di autenticazione previsto</th>
<th>Note, avvisi o errori di configurazione non valida</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Obbligatorio</p></td>
<td><p>Obbligatorio</p></td>
<td><p>True</p></td>
<td><p>SASL su TLS</p></td>
<td><div class="alert">

> [!WARNING]
> Se SASL e TSL sono entrambi obbligatori, il dialback non verrà utilizzato.


</div></td>
</tr>
<tr class="even">
<td><p>Obbligatorio</p></td>
<td><p>Obbligatorio</p></td>
<td><p>False</p></td>
<td><p>SASL su TLS</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Facoltativo</p></td>
<td><p>Obbligatorio</p></td>
<td><p>True</p></td>
<td><p>SASL su TLS, dialback TLS, dialback TCP</p></td>
<td><div class="alert">

> [!WARNING]
> SASL richiede TLS. Impostando TLS come facoltativo, potrebbero verificarsi errori di negoziazione delle sessioni.


</div></td>
</tr>
<tr class="even">
<td><p>Facoltativo</p></td>
<td><p>Obbligatorio</p></td>
<td><p>False</p></td>
<td><p>SASL su TLS</p></td>
<td><div class="alert">

> [!WARNING]
> SASL richiede TLS. Impostando TLS come facoltativo, potrebbero verificarsi errori di negoziazione delle sessioni.


</div></td>
</tr>
<tr class="odd">
<td><p>Non supportato</p></td>
<td><p>Obbligatorio</p></td>
<td><p>True</p></td>
<td><p>Dialback TCP</p></td>
<td><div class="alert">

> [!WARNING]
> SASL richiede TLS. Impostando TLS come facoltativo, potrebbero verificarsi errori di negoziazione delle sessioni.


</div></td>
</tr>
<tr class="even">
<td><p>Non supportato</p></td>
<td><p>Obbligatorio</p></td>
<td><p>False</p></td>
<td><div class="alert">

> [!WARNING]
> Configurazione non valida.


</div></td>
<td><div class="alert">

> [!WARNING]
> Poiché SASL richiede TLS, ma TLS non è disponibile, SASL/TLS ha esito negativo. Il dialback TCP è impostato su false e non può essere utilizzato.


</div></td>
</tr>
<tr class="odd">
<td><p>Obbligatorio</p></td>
<td><p>Facoltativo</p></td>
<td><p>True</p></td>
<td><p>SASL su TLS, dialback TLS</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Obbligatorio</p></td>
<td><p>Facoltativo</p></td>
<td><p>False</p></td>
<td><p>SASL su TLS</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Facoltativo</p></td>
<td><p>Facoltativo</p></td>
<td><p>True</p></td>
<td><p>SASL su TLS, dialback TLS, dialback TCP</p></td>
<td><div class="alert">

> [!WARNING]
> SASL richiede TLS. Impostando TLS come facoltativo, potrebbero verificarsi errori di negoziazione delle sessioni.


</div></td>
</tr>
<tr class="even">
<td><p>Facoltativo</p></td>
<td><p>Facoltativo</p></td>
<td><p>False</p></td>
<td><p>SASL su TLS</p></td>
<td><div class="alert">

> [!WARNING]
> SASL richiede TLS. Impostando TLS come facoltativo, potrebbero verificarsi errori di negoziazione delle sessioni.


</div></td>
</tr>
<tr class="odd">
<td><p>Non supportato</p></td>
<td><p>Facoltativo</p></td>
<td><p>True</p></td>
<td><p>Dialback TCP</p></td>
<td><div class="alert">

> [!WARNING]
> SASL richiede TLS. Impostando TLS come facoltativo, potrebbero verificarsi errori di negoziazione delle sessioni.


</div></td>
</tr>
<tr class="even">
<td><p>Non supportato</p></td>
<td><p>Facoltativo</p></td>
<td><p>False</p></td>
<td><div class="alert">

> [!WARNING]
> Configurazione non valida.


</div></td>
<td><div class="alert">

> [!WARNING]
> SASL richiede TLS. Impostando TLS come facoltativo, potrebbero verificarsi errori di negoziazione delle sessioni.


</div></td>
</tr>
<tr class="odd">
<td><p>Obbligatorio</p></td>
<td><p>Non supportato</p></td>
<td><p>True</p></td>
<td><p>Dialback TLS</p></td>
<td><p>La configurazione consente il dialback TLS.</p></td>
</tr>
<tr class="even">
<td><p>Obbligatorio</p></td>
<td><p>Non supportato</p></td>
<td><p>False</p></td>
<td><p>Configurazione non valida.</p></td>
<td><div class="alert">

> [!WARNING]
> È necessario abilitare SASL o Dialback.


</div></td>
</tr>
<tr class="odd">
<td><p>Facoltativo</p></td>
<td><p>Non supportato</p></td>
<td><p>True</p></td>
<td><p>Dialback TLS, dialback TCP</p></td>
<td><p>Basato sulle scelte di negoziazione dell'altro endpoint, il dialback TCP o TLS verrà accettato.</p></td>
</tr>
<tr class="even">
<td><p>Facoltativo</p></td>
<td><p>Non supportato</p></td>
<td><p>False</p></td>
<td><p>Configurazione non valida.</p></td>
<td><div class="alert">

> [!WARNING]
> È necessario abilitare SASL o Dialback.


</div></td>
</tr>
<tr class="odd">
<td><p>Non supportato</p></td>
<td><p>Non supportato</p></td>
<td><p>True</p></td>
<td><p>Dialback TCP</p></td>
<td><p>Il dialback TCP è l'unico metodo di negoziazione disponibile</p></td>
</tr>
<tr class="even">
<td><p>Non supportato</p></td>
<td><p>Non supportato</p></td>
<td><p>False</p></td>
<td><p>Configurazione non valida.</p></td>
<td><div class="alert">

> [!WARNING]
> È necessario abilitare SASL o Dialback.


</div></td>
</tr>
</tbody>
</table>

