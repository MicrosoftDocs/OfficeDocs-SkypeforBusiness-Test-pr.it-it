---
title: "Lync Server 2013: Elenco tabelle di conformità del server Chat persistente"
TOCTitle: Elenco delle tabelle di conformità del server Chat persistente
ms:assetid: 8563446e-90cc-47cc-8a8e-4883decfe195
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ215878(v=OCS.15)
ms:contentKeyID: 49301203
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Elenco delle tabelle di conformità del server Chat persistente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Lo schema del database di conformità di Chat persistente è costituito dalle tabelle riportate di seguito.

## Elenco delle tabelle di conformità di server Chat persistente


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
<td><p><a href="lync-server-2013-tblcompliancedata.md">tblComplianceData in Lync Server 2013</a></p></td>
<td><p>Include gli eventi di conformità ancora non elaborati da tutti gli adattatori configurati.</p>
<p>Questa tabella include eventi correlati alle Chat persistente, ad esempio messaggi di chat e download di file. Gli eventi dei partecipanti vengono registrati dalla tabella ComplianceParticipant.</p>
<p>I server che hanno elaborato gli eventi in questa tabella sono elencati nella tabella ComplianceFanout.</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblcompliancefanout.md">tblComplianceFanout in Lync Server 2013</a></p></td>
<td><p>Include i server che hanno elaborato un evento di conformità. È strettamente associata alla tabella ComplianceData.</p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-tblcomplianceparticipant.md">tblComplianceParticipant in Lync Server 2013</a></p></td>
<td><p>Include i partecipanti correnti per servizio chat e per server. È gestita in base a eventi di conformità delle parti e di partecipazione ricevuti dal servizio Chat persistente.</p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-tblcompliancestate.md">tblComplianceState in Lync Server 2013</a></p></td>
<td><p>Contiene informazioni relative allo stato di conformità a livello di pool.</p></td>
</tr>
</tbody>
</table>

