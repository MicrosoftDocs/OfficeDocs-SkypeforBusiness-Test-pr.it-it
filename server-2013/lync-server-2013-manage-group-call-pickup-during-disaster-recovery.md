---
title: Gestire la risposta alle chiamate di gruppo durante il ripristino di emergenza
TOCTitle: Gestire la risposta alle chiamate di gruppo durante il ripristino di emergenza
ms:assetid: 2d32f19f-c649-4a72-a4fb-edd338e3a7cc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945618(v=OCS.15)
ms:contentKeyID: 52062124
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestire la risposta alle chiamate di gruppo durante il ripristino di emergenza

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Quando un pool Front End non è disponibile a causa di un evento imprevisto, viene eseguito il failover del servizio nel pool di backup. Durante l'esecuzione di un failover in un pool di backup, gli utenti vengono reindirizzati al pool di backup e sono in modalità di resilienza. In modalità di resilienza gli utenti non possono rispondere a chiamate di altri utenti o far rispondere gli altri utenti alle proprie chiamate. Completato il failover, gli utenti possono nuovamente utilizzare la risposta alle chiamate di gruppo.

Durante il failback al pool primario, gli utenti vengono reindirizzati al pool primario e tornano in modalità di resilienza. La funzionalità di risposta alle chiamate di gruppo non è disponibile finché gli utenti non usciranno dalla modalità di resilienza.

In questa sezione vengono presentate delle considerazioni sulla risposta alle chiamate di gruppo durante il ripristino di emergenza e viene illustrata l'esperienza utente.

## Considerazioni per la risposta alle chiamate di gruppo durante il ripristino di emergenza

Durante il ripristino di emergenza gli utenti che sono stati reindirizzati al pool di backup durante il processo di failover utilizzano l'applicazione Parcheggio di chiamata in esecuzione nel pool di backup per i numeri di risposta alle chiamate di gruppo. Pertanto, il supporto per la risposta alle chiamate di gruppo durante il ripristino di emergenza richiede che l'applicazione Parcheggio di chiamata venga distribuita e abilitata sia nel pool primario che nel pool di backup.

Gli intervalli del numero di risposta alle chiamate di gruppo nella tabella di codici orbit del parcheggio di chiamata devono essere reindirizzati al pool di backup dopo che è stato completato il processo di failover al pool di backup. È necessario reindirizzare gli intervalli di numeri al pool primario dopo che è stato completato il processo di failback al pool primario. Per reindirizzare gli intervalli di risposta alle chiamate di gruppo, utilizzare il cmdlet **Set-CsCallParkOrbit**.

Se si distribuisce un nuovo pool con un altro nome di dominio completo (FQDN) per sostituire il pool primario, è necessario riassegnare al nome di dominio completo (FQDN) del nuovo pool tutti gli intervalli di numeri di risposta alle chiamate di gruppo associati al pool primario. Per riassegnare gli intervalli di numeri a un nuovo pool, è possibile utilizzare il cmdlet **Set-CsCallParkOrbit**. Per informazioni dettagliate sul cmdlet **Set-CsCallParkOrbit**, vedere [Set-CsCallParkOrbit](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCallParkOrbit).

## Esperienza di risposta alle chiamate di gruppo durante un errore del pool

Nella tabella seguente viene riepilogata l'esperienza di risposta alle chiamate di gruppo nelle varie fasi di ripristino di emergenza.

### Esperienza utente durante il ripristino di emergenza

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Stato chiamata</th>
<th>Failover nel pool di backup</th>
<th>Failback al pool primario</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nuove chiamate</p></td>
<td><p><strong>Durante il processo di failover:</strong></p>
<ul>
<li><p>La risposta alle chiamate di gruppo non è disponibile per gli utenti in modalità di resilienza</p></li>
</ul>
<p><strong>Dopo aver completato il failover:</strong></p>
<ul>
<li><p>La risposta alle chiamate di gruppo è disponibile quando gli utenti non sono in modalità di resilienza e gli intervalli dei numeri della risposta alle chiamate di gruppo vengono reindirizzati al pool di backup</p></li>
</ul></td>
<td><p><strong>Durante il processo di failback:</strong></p>
<ul>
<li><p>La risposta alle chiamate di gruppo non è disponibile per gli utenti in modalità di resilienza</p></li>
</ul>
<p><strong>Dopo aver completato il failback:</strong></p>
<ul>
<li><p>La risposta alle chiamate di gruppo è disponibile quando gli utenti non sono in modalità di resilienza e gli intervalli dei numeri della risposta alle chiamate di gruppo vengono reindirizzati al pool primario</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Chiamate nella coda della risposta alle chiamate di gruppo</p></td>
<td><p><strong>Durante il processo di failover:</strong></p>
<ul>
<li><p>Non è possibile rispondere alle chiamate in coda tramite la risposta alle chiamate di gruppo.</p></li>
</ul>
<p><strong>Dopo aver completato il failover:</strong></p>
<ul>
<li><p>Nessuna chiamata in questo stato</p></li>
</ul></td>
<td><p><strong>Durante il processo di failback:</strong></p>
<ul>
<li><p>Non è possibile rispondere alle chiamate in coda tramite la risposta alle chiamate di gruppo.</p></li>
</ul>
<p><strong>Dopo aver completato il failback:</strong></p>
<ul>
<li><p>Non è possibile rispondere alle chiamate in coda tramite la risposta alle chiamate di gruppo.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Chiamata stabilita</p></td>
<td><p><strong>Durante il processo di failover:</strong></p>
<ul>
<li><p>Le chiamate restano connesse</p></li>
</ul>
<p><strong>Dopo aver completato il failover:</strong></p>
<ul>
<li><p>Le chiamate restano connesse</p></li>
</ul></td>
<td><p><strong>Durante il processo di failback:</strong></p>
<ul>
<li><p>Le chiamate restano connesse</p></li>
</ul>
<p><strong>Dopo aver completato il failback:</strong></p>
<ul>
<li><p>Le chiamate restano connesse</p></li>
</ul></td>
</tr>
</tbody>
</table>

