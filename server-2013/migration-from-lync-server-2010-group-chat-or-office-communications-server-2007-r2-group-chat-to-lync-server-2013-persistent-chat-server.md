---
title: Migrazione da Lync Server 2010, Group Chat o Office Communications Server 2007 R2 Group Chat al server chat persistente di Lync Server 2013
TOCTitle: Migrazione da Lync Server 2010, Group Chat o Office Communications Server 2007 R2 Group Chat al server chat persistente di Lync Server 2013
ms:assetid: 5b4d3db1-6eba-4932-b49c-f60bcf9488f9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615442(v=OCS.15)
ms:contentKeyID: 49300655
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Migrazione da Lync Server 2010, Group Chat o Office Communications Server 2007 R2 Group Chat al server chat persistente di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-06_

Negli argomenti di questa sezione viene illustrato il processo di migrazione da Lync Server 2010, Group Chat o Office Communications Server 2007 R2Group Chat a Lync Server 2013, server Chat persistente. Se si desidera che la distribuzione di Lync Server 2013, server Chat persistente coesista con una distribuzione di Lync Server 2010, Group Chat o Office Communications Server 2007 R2Group Chat, in questa guida è possibile trovare inoltre alcune informazioni fondamentali per l'utilizzo di un ambiente misto. Le informazioni nella guida sono incentrate principalmente sulla migrazione dei dati per server Chat persistente. Per gli utenti che eseguono la migrazione da versioni legacy di Lync Server a Lync Server 2013, vedere [Migrazione da Lync Server 2010 a Lync Server 2013](migration-from-lync-server-2010-to-lync-server-2013.md) e [Migrazione da Office Communications Server 2007 R2 a Lync Server 2013](migration-from-office-communications-server-2007-r2-to-lync-server-2013.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>In questo argomento si presuppone che Lync Server 2013 sia già stato installato in coesistenza con Lync Server 2010 o Office Communications Server 2007 R2.</td>
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
<td>Questa guida descrive i passaggi normalmente necessari per eseguire ogni fase della migrazione. Non sono descritti tutti gli scenari di migrazione o tutte le topologie di distribuzione legacy possibili. Per questi motivi, potrebbe non essere necessario eseguire tutti i passaggi descritti oppure potrebbero servirne altri, a seconda della distribuzione. Nella guida sono inoltre disponibili alcuni esempi dei passaggi di verifica, forniti allo scopo di illustrare quali aspetti ed elementi considerare per assicurarsi che ogni fase venga completata correttamente, man mano che si procede nella migrazione. È possibile modificare tali passaggi di verifica per adattarli allo specifico processo di migrazione.</td>
</tr>
</tbody>
</table>


Questa guida include informazioni specifiche per l'aggiornamento della distribuzione esistente e non spiega come modificare la topologia esistente. Non viene descritta l'implementazione delle nuove funzionalità. Se una procedura dettagliata è descritta altrove, in questa guida vengono forniti riferimenti al documento o alla sezione del documento appropriato.

Nel documento vengono utilizzati termini specifici, con le definizioni seguenti.

  - *migrazione*   
    Spostamento della distribuzione da una versione precedente di server Chat persistente, nota in precedenza come Group Chat Server, a Lync Server 2013, server Chat persistente.

<!-- end list -->

  - *aggiornamento*   
    Installazione di una versione più recente del software in un computer server o client.

<!-- end list -->

  - *coesistenza*   
    Ambiente temporaneo esistente durante la migrazione, quando è stata completata la migrazione di alcune funzionalità a Lync Server 2013, server Chat persistente e altre rimangono ancora in una versione precedente di Group Chat Server.

server Chat persistente è un'estensione dell'infrastruttura di Lync Server 2013. A seconda della topologia in uso, è possibile eseguire la migrazione di Lync Server 2010, Group Chat o Office Communications Server 2007 R2Group Chat a Lync Server 2013server Chat persistente. Per informazioni dettagliate sulle topologie disponibili e sui requisiti tecnici e software per la migrazione di Group Chat Server, vedere [Pianificazione del server Chat persistente in Lync Server 2013](lync-server-2013-planning-for-persistent-chat-server.md) nella documentazione relativa alla pianificazione.

Se l'organizzazione richiede il supporto della conformità, questa funzionalità viene ora installata automaticamente in ogni server Chat persistente. Non è più necessario un server separato per la conformità.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>È necessario installare server Chat persistente in un file system NTFS per garantire un livello adeguato di sicurezza del file system. Il file system FAT32 non è supportato per server Chat persistente.<br />
Se l'organizzazione richiede il supporto della conformità, questa funzionalità viene ora installata automaticamente in ogni server Chat persistente. Non è più necessario un server separato per la conformità. Per ulteriori dettagli sulle modifiche introdotte in Lync Server 2013server Chat persistente, vedere <a href="lync-server-2013-new-persistent-chat-server-features.md">Nuove funzionalità del server Chat persistente in Lync Server 2013</a> nella documentazione introduttiva.</td>
</tr>
</tbody>
</table>


## Contenuto della sezione

  - [Scenario di migrazione standard - informazioni generali](standard-migration-scenario-high-level.md)

  - [Processo di migrazione - Dettagli](migration-process-details.md)

  - [Considerazioni sulla coesistenza](coexistence-considerations.md)

