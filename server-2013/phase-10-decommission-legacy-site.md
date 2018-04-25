---
title: 'Fase 10: rimuovere le autorizzazioni del sito legacy'
TOCTitle: 'Fase 10: rimuovere le autorizzazioni del sito legacy'
ms:assetid: d591a310-3b5c-4092-b19e-0349616e40df
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205300(v=OCS.15)
ms:contentKeyID: 49302093
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Fase 10: rimuovere le autorizzazioni del sito legacy

 

_**Ultima modifica dell'argomento:** 2012-10-16_

Negli argomenti seguenti vengono fornite informazioni per impostare i pool come non disponibili e per disattivare e rimuovere i server e i pool da una distribuzione legacy di Office Communications Server 2007 R2. Non tutte le procedure elencate in questa sezione sono obbligatorie. Leggere le informazioni in ognuno di questi argomenti per determinare quale procedura utilizzare per rimuovere la disponibilità.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ205186.Caution(OCS.15).gif" title="Caution" alt="Caution" />Attenzione:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Se in Lync Server 2013 sono state importate directory conferenze per conferenze con accesso esterno, è importante trasferire la proprietà di queste directory Lync Server 2013 prima di iniziare la rimozione dei pool. Se si rimuove un pool senza prima trasferire la proprietà delle directory conferenze, la funzionalità di accesso esterno non funzionerà più per tutte le riunioni spostate. È necessario eseguire il passaggio di trasferimento di proprietà una volta per ogni directory conferenze del pool legacy.</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Per informazioni sulla migrazione e l'aggiornamento delle applicazioni Microsoft Unified Communications Managed API (UCMA), prima della rimozione delle autorizzazione dell'ambiente legacy, vedere <a href="http://go.microsoft.com/fwlink/p/?linkid=269555">http://go.microsoft.com/fwlink/p/?LinkId=269555</a></td>
</tr>
</tbody>
</table>


## Contenuto della sezione

  - [Spostare le directory conferenze](move-conference-directories.md)

  - [Aggiornare i record SRV DNS](update-dns-srv-records_1.md)

  - [Rimozione di autorizzazioni di server e pool](decommissioning-servers-and-pools.md)

  - [Rimuovere BackCompatSite](remove-backcompatsite.md)

