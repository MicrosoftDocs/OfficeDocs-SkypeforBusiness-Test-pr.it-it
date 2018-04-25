---
title: Avvio di Lync da un'altra applicazione
TOCTitle: Avvio di Lync da un'altra applicazione
ms:assetid: 573b30b1-6590-4b24-8e96-a41be57cb0ef
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398376(v=OCS.15)
ms:contentKeyID: 52062158
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Avvio di Lync da un'altra applicazione

 

_**Ultima modifica dell'argomento:** 2015-03-09_

È possibile utilizzare parametri della riga di comando per avviare rapidamente Lync 2013. Se ad esempio un utente fa clic su un numero di telefono in un'altra applicazione, questa può avviare un'istanza di Lync 2013 ed effettuare una chiamata a tale numero.

Lync 2013 supporta inoltre il riconoscimento di un elenco delimitato da punti e virgola di nomi di contatto per le conferenze con più utenti.

Se Lync 2013 è configurato per l'accesso automatico all'avvio, l'avvio di Lync 2013 con parametri della riga di comando consentirà di aprire la finestra principale di Lync. Se Lync non è configurato per l'accesso automatico all'avvio, verrà visualizzata la finestra di accesso.

Nella tabella seguente vengono descritti i parametri disponibili.

### Parametri della riga di comando di Lync 2013

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Estensione</th>
<th>Formato dei dati</th>
<th>Azione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>tel:</p></td>
<td><p>URI TEL</p></td>
<td><p>Apre la finestra di conversazione per una chiamata audio, ma non compone il numero specificato.</p></td>
</tr>
<tr class="even">
<td><p>callto:</p></td>
<td><p>tel:, sip: o URI TEL digitabile</p></td>
<td><p>Apre la finestra di conversazione per una chiamata audio, ma non compone il numero specificato.</p></td>
</tr>
<tr class="odd">
<td><p>sip:</p></td>
<td><p>URI SIP</p></td>
<td><p>Apre la finestra di conversazione con l'URI (Uniform Resource Identifier) SIP specificato nell'elenco dei partecipanti.</p></td>
</tr>
<tr class="even">
<td><p>Sips:</p></td>
<td><p>URI SIP</p></td>
<td><p>Se si configura Lync 2013 per l'utilizzo del protocollo TLS (Transport Layer Security), il funzionamento è uguale a quello di sip:. Se non si utilizza TLS, viene visualizzata una finestra di dialogo per informare l'utente che è necessario un livello di sicurezza più elevato.</p></td>
</tr>
<tr class="odd">
<td><p>conf:</p></td>
<td><p>URI SIP della conferenza a cui partecipare</p></td>
<td><p>Se l'URI è self, crea un'istanza del componente Focus e attiva la visualizzazione solo dell'elenco dei partecipanti. In caso contrario, attiva la visualizzazione dell'elenco dei partecipanti ma non invia una richiesta INVITE.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>im:</p></td>
<td><p>URI SIP</p></td>
<td><p>Visualizza una finestra di conversazione solo per la messaggistica istantanea con l'URI SIP. Accetta più URI SIP specificati all'interno di parentesi angolari (&lt;&gt;) senza alcun separatore.</p>
<pre><code>im:&lt;sip:user1@host&gt;&lt;sip:user2@host&gt;</code></pre></td>
</tr>
</tbody>
</table>


Nella tabella seguente sono disponibili esempi di questi parametri della riga di comando.

### Esempi di parametri della riga di comando

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Istanza</th>
<th>Risultati</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tel:+14255550101</p></td>
<td><p>Apre una visualizzazione solo telefonica con +14255550101.</p></td>
</tr>
<tr class="even">
<td><p>Callto:tel:+ 14255550101</p></td>
<td><p>Apre una visualizzazione solo telefonica con +14255550101.</p></td>
</tr>
<tr class="odd">
<td><p>Callto:sip:kazuto@litwareinc.com</p></td>
<td><p>Apre una visualizzazione solo telefonica con kazuto@litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p>sip:kazuto@litwareinc.com</p></td>
<td><p>Apre una finestra di conversazione con kazuto@litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p>conf:sip:https://meet.contoso.com/kazuto/7322994</p></td>
<td><p>Apre una finestra di conversazione e visualizza le opzioni per l'aggiunta dell'audio della riunione.</p></td>
</tr>
</tbody>
</table>

