---
title: Routing in base alla posizione e trasferimenti di chiamata con consultazione
TOCTitle: Routing in base alla posizione e trasferimenti di chiamata con consultazione
ms:assetid: b12460c2-36c8-481f-b867-fe10dc1c0bdf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362836(v=OCS.15)
ms:contentKeyID: 56269972
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Routing in base alla posizione e trasferimenti di chiamata con consultazione

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Oltre ad applicare il routing in base alla posizione alle riunioni Lync, l'applicazione per conferenze con routing in base alla posizione applica anche limitazioni di routing in base alla posizione ai trasferimenti di chiamata con consultazione in uscita verso gli endpoint PSTN. Un trasferimento di chiamata con consultazione è una chiamata stabilita tra due parti in cui una delle parti trasferisce la chiamata a un nuovo utente. Ad esempio, un endpoint PSTN chiama l'utente A (destinatario della chiamata Lync). L'utente A determina che l'utente PSTN deve essere inoltrato all'utente B (utente di Lync). L'utente A chiama l'utente B tenendo l'utente PSTN in attesa. L'utente B accetta di parlare con l'utente PSTN. L'utente A trasferisce la chiamata in attesa all'utente B.

**Flusso dei trasferimenti di chiamata con consultazione**

![Diagramma del routing in base alla posizione per le conferenze](images/Dn362836.e4d43d6f-23d2-49c9-b12b-15248a743f92(OCS.15).jpg "Diagramma del routing in base alla posizione per le conferenze")

Quando un utente abilitato per il routing in base alla posizione inizia un trasferimento di chiamata con consultazione di un endpoint PSTN (come illustrato nella figura precedente), vengono create due chiamate attive, una tra l'utente PSTN e l'utente A di Lync e l'altra tra l'utente A e l'utente B di Lync. Il comportamento seguente viene imposto dall'applicazione per conferenze con routing in base alla posizione:

  - Se il trunk SIP che instrada la chiamata PSTN è autorizzato a reinstradarla al sito di rete in cui si trova l'utente B di Lync (la destinazione del trasferimento), il trasferimento di chiamata viene consentito, altrimenti il trasferimento di chiamata con consultazione viene bloccato. Questa autorizzazione viene eseguita se la posizione della parte trasferita è nello stesso sito di rete del trunk SIP che instrada la chiamata attiva all'endpoint PSTN.

  - Se il trunk SIP che instrada la chiamata PSTN in entrata non è autorizzato a instradare chiamate al sito di rete in cui si trova la parte trasferita (l'utente B di Lync) o se la parte trasferita si trova in un sito di rete sconosciuto, il trasferimento di chiamata con consultazione all'endpoint PSTN (la destinazione del trasferimento di chiamata) viene bloccato.

La tabella seguente descrive come vengono applicate le limitazioni di routing in base alla posizione dall'applicazione per conferenze con routing in base alla posizione per i trasferimenti di chiamata con consultazione. Sebbene gli endpoint PBX non siano associati direttamente a un sito di rete, il trunk SIP a cui il PBX è connesso può essere assegnato a un sito di rete. Di conseguenza, l'endpoint PBX può essere associato indirettamente a un sito di rete.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Sito di rete della parte trasferita della chiamata</p></td>
<td><p>Sito di rete della destinazione di trasferimento della chiamata</p></td>
<td><p>Comportamento</p></td>
</tr>
<tr class="even">
<td><p>Endpoint PSTN</p></td>
<td><p>Utente Lync nello stesso sito di rete (ad esempio sito 1)</p></td>
<td><p>Trasferimento con consultazione consentito</p></td>
</tr>
<tr class="odd">
<td><p>Endpoint PSTN</p></td>
<td><p>Utente Lync in siti di rete diversi (ad esempio sito 2)</p></td>
<td><p>Trasferimento con consultazione non consentito</p></td>
</tr>
<tr class="even">
<td><p>Endpoint PSTN</p></td>
<td><p>Utente Lync in un sito di rete sconosciuto</p></td>
<td><p>Trasferimento con consultazione non consentito</p></td>
</tr>
<tr class="odd">
<td><p>Endpoint PSTN</p></td>
<td><p>Utente Lync federato</p></td>
<td><p>Trasferimento con consultazione non consentito</p></td>
</tr>
<tr class="even">
<td><p>Endpoint PSTN</p></td>
<td><p>Endpoint PBX nello stesso sito (ad esempio sito 1)</p></td>
<td><p>Trasferimento con consultazione consentito</p></td>
</tr>
<tr class="odd">
<td><p>Endpoint PSTN</p></td>
<td><p>Endpoint PBX in un sito diverso (ad esempio sito 2)</p></td>
<td><p>Trasferimento con consultazione non consentito</p></td>
</tr>
<tr class="even">
<td><p>Endpoint PBX nello stesso sito (ad esempio sito 1)</p></td>
<td><p>Endpoint PSTN</p></td>
<td><p>Trasferimento con consultazione consentito</p></td>
</tr>
<tr class="odd">
<td><p>Endpoint PBX in un sito diverso (ad esempio sito 2)</p></td>
<td><p>Endpoint PSTN</p></td>
<td><p>Trasferimento con consultazione non consentito</p></td>
</tr>
<tr class="even">
<td><p>Endpoint PBX in qualsiasi sito</p></td>
<td><p>Utente Lync nello stesso sito di rete (ad esempio sito 1)</p></td>
<td><p>Trasferimento con consultazione consentito</p></td>
</tr>
<tr class="odd">
<td><p>Endpoint PBX in qualsiasi sito</p></td>
<td><p>Utente Lync in siti di rete diversi (ad esempio sito 2)</p></td>
<td><p>Trasferimento con consultazione consentito</p></td>
</tr>
<tr class="even">
<td><p>Endpoint PBX in qualsiasi sito</p></td>
<td><p>Utente Lync in un sito di rete sconosciuto</p></td>
<td><p>Trasferimento con consultazione consentito</p></td>
</tr>
<tr class="odd">
<td><p>Endpoint PBX in qualsiasi sito</p></td>
<td><p>Utente Lync federato</p></td>
<td><p>Trasferimento con consultazione consentito</p></td>
</tr>
</tbody>
</table>

