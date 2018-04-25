---
title: 'Lync Server 2013: Requisiti relativi a IIS (Internet Information Services)'
TOCTitle: Requisiti relativi a IIS (Internet Information Services)
ms:assetid: 4f57a605-a8a9-4c5a-9a18-05ecb3d9ab6b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398321(v=OCS.15)
ms:contentKeyID: 49300539
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti relativi a IIS (Internet Information Services) in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Diversi componenti di Lync Server 2013 richiedono Internet Information Services (IIS). In questo argomento vengono descritte le funzionalità IIS specifiche necessarie per supportare Lync Server. Negli argomenti di questa sezione vengono illustrati i requisiti di componenti specifici per IIS.

Quando il ruolo Server Web (IIS) è abilitato in Windows Server 2008, per impostazione predefinita vengono installati vari servizi ruolo. Nella tabella seguente vengono descritti i servizi ruolo aggiuntivi che devono essere installati quando si abilita il ruolo Server Web (IIS) in Windows Server 2008.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Servizio ruolo</th>
<th>Funzionalità</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Funzionalità HTTP comuni</p></td>
<td><p>Reindirizzamento HTTP</p></td>
</tr>
<tr class="even">
<td><p>Sviluppo applicazioni</p></td>
<td><p>ASP.NET</p></td>
</tr>
<tr class="odd">
<td><p>Sviluppo applicazioni</p></td>
<td><p>Estendibilità .NET</p></td>
</tr>
<tr class="even">
<td><p>Sviluppo applicazioni</p></td>
<td><p>Estensioni ISAPI</p></td>
</tr>
<tr class="odd">
<td><p>Sviluppo applicazioni</p></td>
<td><p>Filtri ISAPI</p></td>
</tr>
<tr class="even">
<td><p>Integrità e diagnostica</p></td>
<td><p>Strumenti di registrazione</p></td>
</tr>
<tr class="odd">
<td><p>Integrità e diagnostica</p></td>
<td><p>Funzionalità di traccia</p></td>
</tr>
<tr class="even">
<td><p>Sicurezza</p></td>
<td><p>Autenticazione di base</p></td>
</tr>
<tr class="odd">
<td><p>Sicurezza</p></td>
<td><p>Autenticazione di Windows</p></td>
</tr>
<tr class="even">
<td><p>Strumenti di gestione</p></td>
<td><p>Strumenti e script di gestione IIS</p></td>
</tr>
<tr class="odd">
<td><p>Strumenti di gestione</p></td>
<td><p>Compatibilità di gestione con IIS 6</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg398321.security(OCS.15).gif" title="security" alt="security" />SicurezzaNota:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Se si utilizza IIS 7.0 in un sistema operativo Windows Server 2008, il programma di installazione di Lync Server disabilita l'autenticazione in modalità kernel in IIS.</td>
</tr>
</tbody>
</table>


## Argomenti della sezione

  - [Requisiti di IIS per pool Front End e server Standard Edition in Lync Server 2013](lync-server-2013-iis-requirements-for-front-end-pools-and-standard-edition-servers.md)

