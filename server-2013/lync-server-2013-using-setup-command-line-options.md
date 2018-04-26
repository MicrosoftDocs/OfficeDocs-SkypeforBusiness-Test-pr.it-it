---
title: Utilizzo delle opzioni della riga di comando per l'installazione
TOCTitle: Utilizzo delle opzioni della riga di comando per l'installazione
ms:assetid: 99878c3c-ff31-48e2-8424-580d7b07a7bf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205129(v=OCS.15)
ms:contentKeyID: 49301423
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Utilizzo delle opzioni della riga di comando per l'installazione

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La riga di comando di Setup.exe consente di eseguire un numero limitato di operazioni di configurazione di Office. Invece di usare le opzioni della riga di comando di Setup, in genere si usa lo Strumento di personalizzazione di Office e il file the Config.xml per la personalizzazione delle caratteristiche e della configurazione del prodotto.

La riga di comando di Setup.exe di Office riconosce le opzioni descritte nella tabella seguente.

### Opzioni della riga di comando del programma di installazione di Office

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Opzione della riga di comando</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>/admin</p></td>
<td><p>Esegue lo Strumento di personalizzazione di Office per creare un file di personalizzazione della configurazione (file con estensione msp).</p></td>
</tr>
<tr class="even">
<td><p>/adminfile [percorso]</p></td>
<td><p>Applica all'installazione il file di personalizzazione dell'installazione specificato. È possibile specificare il percorso di un determinato file di personalizzazione dell'installazione (msp) o della cartella in cui sono archiviati i file di personalizzazione.</p></td>
</tr>
<tr class="odd">
<td><p>/config [percorso]</p></td>
<td><p>Specifica il file Config.xml usato durante l'installazione. Usare l'opzione /config per specificare il file Config.xml personalizzato per le installazioni di Lync 2013, ad esempio: <code>/config \\server\share\Lync15\Lync.WW\Config.xml</code></p></td>
</tr>
<tr class="even">
<td><p>/modify Lync</p></td>
<td><p>Usato con un file Config.xml modificato per eseguire il programma di installazione in modalità manutenzione e apportare modifiche a un'installazione di Office esistente. È ad esempio possibile usare l'opzione /modify per aggiungere o rimuovere caratteristiche di Lync.</p></td>
</tr>
<tr class="odd">
<td><p>/repair Lync</p></td>
<td><p>Esegue il programma di installazione nel computer dell'utente per ripristinare Lync.</p></td>
</tr>
<tr class="even">
<td><p>/uninstall Lync</p></td>
<td><p>Esegue il programma di installazione per rimuovere Lync dal computer dell'utente.</p></td>
</tr>
</tbody>
</table>


Per informazioni dettagliate sull'uso delle opzioni della riga di comando, vedere [http://go.microsoft.com/fwlink/?linkid=267515\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=267515%26clcid=0x410).

