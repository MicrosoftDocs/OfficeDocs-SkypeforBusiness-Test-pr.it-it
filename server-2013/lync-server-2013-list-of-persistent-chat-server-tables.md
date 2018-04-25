---
title: 'Lync Server 2013: Elenco delle tabelle del server Chat persistente'
TOCTitle: Elenco delle tabelle del server Chat persistente
ms:assetid: 26c9e271-3516-4d90-b930-70fec4e359ea
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558628(v=OCS.15)
ms:contentKeyID: 49299968
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Elenco delle tabelle del server Chat persistente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Lo schema del database di Chat persistente è costituito dalle tabelle riportate di seguito.

## Sincronizzazione di Active Directory


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tabella</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-tbladcookie.md">tblADCookie in Lync Server 2013</a></p></td>
<td><p>Include i cookie di sincronizzazione LDAP (Lightweight Directory Access Protocol) correnti. Ogni riga corrisponde a un dominio di Servizi di dominio Active Directory monitorato attivamente da server Chat persistente per individuare le modifiche. In questa tabella vengono rappresentati solo i domini di Active Directory pertinenti per server Chat persistente.)</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblprincipalmemberdifference.md">tblPrincipalMemberDifference in Lync Server 2013</a></p></td>
<td><p>Include le modifiche delle appartenenze ai gruppi (sia i membri aggiunti che quelli rimossi) non ancora elaborate dagli ultimi passaggi di sincronizzazione di Active Directory ed è una delle tabelle temporanee, insieme alla tabella tblADUpdates, utilizzate nel primo passaggio di sincronizzazione di Active Directory.</p>
<p>Le modifiche delle appartenenza sono archiviate e/o elaborate solo per i gruppi che sono elencati nella tabella tblPrincipal o che includono membri già elencati in tale tabella.</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tbladupdates.md">tblADUpdates in Lync Server 2013</a></p></td>
<td><p>Include modifiche a Servizi di dominio Active Directory che non sono state ancora elaborate dai successivi passaggi di sincronizzazione di Active Directory ed è una delle tabelle temporanee (insieme alla tabella tblPrincipalMemberDifference) utilizzate nel primo passaggio di sincronizzazione di Active Directory.</p>
<p>Le modifiche apportate a Active Directory sono archiviate e/o elaborate solo per le entità già elencate nella tabella tblPrincipal.</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblprincipalmembers.md">tblPrincipalMembers in Lync Server 2013</a></p></td>
<td><p>Include le appartenenze delle entità.</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tblprincipalmeta.md">tblPrincipalMeta in Lync Server 2013</a></p></td>
<td><p>Include le entità che devono essere aggiornate a partire da Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblskippedaffiliations.md">tblSkippedAffiliations in Lync Server 2013</a></p></td>
<td><p>Include le affiliazioni che non è stato possibile aggiornare per qualche motivo, in genere per errori di accesso di Active Directory.</p>
<p>Questa tabella è esclusivamente per scopi informativi. Il relativo contenuto non viene utilizzato.</p>
<p>Le entità di cui non è stato possibile aggiornare correttamente le affiliazioni sono contenute nella tabella tblPrincipalMeta e dispongono di un'altra possibilità di aggiornamento.</p></td>
</tr>
</tbody>
</table>


## Entità, affiliazioni, nodi, ambiti e ruoli


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tabella</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-tblprincipaltype.md">tblPrincipalType in Lync Server 2013</a></p></td>
<td><p>Include i tipi di entità per classificare il contenuto della tabella tblPrincipal. Questa tabella è statica, viene configurata durante la creazione del database e non è soggetta a modifiche.</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblprincipal.md">tblPrincipal in Lync Server 2013</a></p></td>
<td><p>Include tutte le entità, ovvero utenti, cartelle, gruppi e così via. server Chat persistente gestisce questa tabella come un semplice elenco eterogeneo. Diverse colonne sono basate sul tipo di ogni entità.</p>
<p>La maggior parte di queste entità è costituita da copie memorizzate nella cache di oggetti archiviati in Active Directory. La creazione nella tabella Principal della copia memorizzata nella cache di questi oggetti Active Directory è denominata <em>provisioning</em> .</p>
<p>Alcune entità vengono create in numero maggiore rispetto ad altre e alcuni oggetti di Active Directory vengono completamente ignorati.</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tblprincipalaffiliations.md">tblPrincipalAffiliations in Lync Server 2013</a></p></td>
<td><p>Include affiliazioni di entità che descrivono le appartenenze a gruppi di sicurezza di Active Directory, contenitori di Active Directory e così via.</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblnode.md">tblNode in Lync Server 2013</a></p></td>
<td><p>Include il nodo della categoria, così come viene gestito in Pannello di controllo di Lync Server.</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tblroletype.md">tblRoleType in Lync Server 2013</a></p></td>
<td><p>Include i tipi di ruolo e gli insiemi di autorizzazioni associati. Questa tabella di ricerca è statica.</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblscopeprincipal.md">tblScopePrincipal in Lync Server 2013</a></p></td>
<td><p>Include gli ambiti assegnati ai nodi.</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tblprincipalrole.md">tblPrincipalRole in Lync Server 2013</a></p></td>
<td><p>Include i ruoli assegnati ai nodi.</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblsiopwhitelist.md">tblSiopWhiteList in Lync Server 2013</a></p></td>
<td><p>Include i componenti aggiuntivi registrati che possono essere associati ai nodi.</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tblenumattribute.md">tblEnumAttribute in Lync Server 2013</a></p></td>
<td><p>Include solo gli attributi hardcoded &quot;Visibility&quot; e &quot;Behavior&quot; usati nella tabella tblNode.</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblenumvalue.md">tblEnumValue in Lync Server 2013</a></p></td>
<td><p>Include i valori degli attributi hardcoded &quot;Visibility&quot; e &quot;Behavior&quot; usati nella tabella tblNode.</p></td>
</tr>
</tbody>
</table>


## Inviti, chat e altro supporto client


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tabella</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-tblprincipalinvites.md">tblPrincipalInvites in Lync Server 2013</a></p></td>
<td><p>Include inviti per tutti gli utenti di cui è stato eseguito il provisioning nel sistema per tutti i nodi con Auto Invite abilitato.</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblchat.md">tblChat in Lync Server 2013</a></p></td>
<td><p>Include tutti i messaggi di chat.</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tbllastinviteid.md">tblLastInviteId in Lync Server 2013</a></p></td>
<td><p>Include l'ID dell'ultimo invito generato e usato nella tabella tblPrincipalInvites per ogni utente.</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tbllastchatid.md">tblLastChatId in Lync Server 2013</a></p></td>
<td><p>Include l'ID dell'ultima chat generata e usata nella tabella tblChat per ogni utente.</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tblpreference.md">tblPreference in Lync Server 2013</a></p></td>
<td><p>Include le preferenze client degli utenti (usate solo dai client legacy).</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblfiletoken.md">tblFileToken in Lync Server 2013</a></p></td>
<td><p>Include token temporanei per il trasferimento di file. Ogni volta che un file viene caricato o scaricato, il servizio Chat persistente genera un token usato dal client per accedere all'archivio file del servizio Web.</p></td>
</tr>
</tbody>
</table>


## Supporto server


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tabella</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-tblserveridentity.md">tblServerIdentity in Lync Server 2013</a></p></td>
<td><p>Include i server attivi nel pool di server Chat persistente.</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tbladminlock.md">tblAdminLock in Lync Server 2013</a></p></td>
<td><p>Include il blocco amministratore per l'esecuzione di alcuni comandi dell'amministratore. La voce di revisione di sistema nella tabella tblSystemRevision viene incrementata dopo ogni rilascio del blocco.</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tblsystemrevision.md">tblSystemRevision in Lync Server 2013</a></p></td>
<td><p>Include il numero di revisione usato insieme alla tabella tblAdminLock per garantire la coerenza tra più client.</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblactivepeers.md">tblActivePeers in Lync Server 2013</a></p></td>
<td><p>Include le connessioni peer-to-peer correnti tra i servizi Chat persistente.</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tblconfig.md">tblConfig in Lync Server 2013</a></p></td>
<td><p>Include la configurazione non supportata di server Chat persistente.</p></td>
</tr>
</tbody>
</table>

