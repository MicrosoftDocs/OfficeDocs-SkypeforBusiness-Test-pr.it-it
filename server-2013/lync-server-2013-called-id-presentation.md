---
title: Presentazione dell'ID chiamato in Lync Server 2013
TOCTitle: Presentazione dell'ID chiamato in Lync Server 2013
ms:assetid: cf6c6af5-3418-411e-a50b-7a9cf8e100d4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721892(v=OCS.15)
ms:contentKeyID: 49887762
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Presentazione dell'ID chiamato in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

Con Lync Server 2010, il numero di telefono dell'utente chiamato, ovvero il numero di telefono chiamato, può essere convertito dal formato E.164 nel formato di composizione locale richiesto dal *peer trunk*, ovvero il gateway, il centralino (PBX) o il trunk SIP associato. A tale scopo, è necessario definire una o più regole per la conversione dell'URI di richiesta prima del routing al peer trunk.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La possibilità di associare una o più regole di conversione a una configurazione trunk di VoIP aziendale è un'<em>alternativa</em> alla configurazione di regole di conversione nel peer trunk. Non associare regole di conversione a una configurazione trunk di VoIP aziendale se sono state configurate regole di conversione nel peer trunk, perché le due regole potrebbero essere in conflitto.</td>
</tr>
</tbody>
</table>


È possibile utilizzare uno dei metodi seguenti per creare e modificare una regola di conversione:

  - Utilizzare lo strumento **Crea regola di conversione** per specificare i valori per le cifre iniziali, la lunghezza, le cifre da rimuovere e quelle da aggiungere, quindi lasciare che il formato e la regola di conversione corrispondenti vengano generati automaticamente dal Pannello di controllo di Lync Server.

  - Scrivere manualmente espressioni regolari per definire il formato di corrispondenza e la regola di conversione.


> [!NOTE]
> Per informazioni su come scrivere le espressioni regolari, vedere "Espressioni regolari di .NET Framework" all'indirizzo <A class=uri href="http://go.microsoft.com/fwlink/?linkid=140927%26clcid=0x410">http://go.microsoft.com/fwlink/?linkid=140927&amp;clcid=0x410</A>.



## Argomenti della sezione

  - [Creare o modificare una regola di conversione utilizzando lo strumento Crea regola di conversione](lync-server-2013-create-or-modify-a-translation-rule-by-using-the-build-a-translation-rule-tool.md)

  - [Creare o modificare manualmente una regola di conversione](lync-server-2013-create-or-modify-a-translation-rule-manually.md)

## Vedere anche

#### Concetti

[Presentazione dell'ID chiamante in Lync Server 2013](lync-server-2013-caller-id-presentation.md)

