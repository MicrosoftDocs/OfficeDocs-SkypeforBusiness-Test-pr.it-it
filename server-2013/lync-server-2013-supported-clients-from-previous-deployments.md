---
title: 'Lync Server 2013: Client supportati dalle distribuzioni precedenti'
TOCTitle: Client supportati dalle distribuzioni precedenti
ms:assetid: 69d427f8-57a5-4244-b2ed-f2eb7600285e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398499(v=OCS.15)
ms:contentKeyID: 49300866
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Client supportati dalle distribuzioni precedenti in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In uno scenario di coesistenza i client di Lync Server 2013 possono interagire con i client di versioni precedenti di Lync Server e Office Communications Server. Diversamente dalle versioni precedenti, Lync Server 2010 supporta i nuovi client di Lync 2013 e ciò consente alle organizzazioni che eseguono l'aggiornamento da Lync Server 2010 di distribuire i nuovi client in modo indipendente dagli aggiornamenti di Lync Server.

## Combinazioni supportate di client e server

Nella tabella seguente sono indicate le combinazioni supportate di versioni client e server. Lync Server 2013 supporta due versioni client precedenti e Lync Server 2010 supporta il nuovo client Lync 2013.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Client</th>
<th>Lync Server 2013</th>
<th>Lync Server 2010</th>
<th>Office Communications Server 2007 R2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lync 2013</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Non supportato</p></td>
</tr>
<tr class="even">
<td><p>Lync Web App 2013</p></td>
<td><p>Supportato</p></td>
<td><p>Non supportato</p></td>
<td><p>Non supportato</p></td>
</tr>
<tr class="odd">
<td><p>Lync 2010</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Non supportato</p></td>
</tr>
<tr class="even">
<td><p>Lync 2010 Attendant</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Non supportato</p></td>
</tr>
<tr class="odd">
<td><p>Lync 2010, Group Chat</p></td>
<td><p>Non applicabile</p></td>
<td><p>Supportato1</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p>Lync Web App 2010</p></td>
<td><p>Non supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Non supportato</p></td>
</tr>
<tr class="odd">
<td><p>Lync 2010 Attendee</p></td>
<td><p>Non supportato2</p></td>
<td><p>Supportato</p></td>
<td><p>Non supportato</p></td>
</tr>
<tr class="even">
<td><p>Office Communicator 2007 R2</p></td>
<td><p>Interoperativo3</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Office Communications Server 2007 R2 Attendant</p></td>
<td><p>Non supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
</tr>
<tr class="even">
<td><p>Office Communicator 2007</p></td>
<td><p>Non supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
</tr>
<tr class="odd">
<td><p>Office Live Meeting 2007</p></td>
<td><p>Non supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Supportato</p></td>
</tr>
</tbody>
</table>


1In Microsoft Lync Server 2010 la funzionalità Group Chat è disponibile con Group Chat Server, un'applicazione attendibile di terze parti per Lync Server 2010. I client di Lync 2013 non sono compatibili con Lync Server 2010, Group Chat.

2Lync Web App 2013 offre ora funzionalità complete di partecipazione alle riunioni, inclusi audio e video del computer e può sostituire Lync 2010 Attendee.

3Le funzionalità di presenza e messaggistica istantanea di Office Communicator 2007 R2 sono compatibili con Lync Server 2013, mentre le funzionalità di conferenza non lo sono. Durante la migrazione da Office Communications Server 2007 R2, Office Communicator 2007 R2 è utile per l'interoperabilità di presenza e messaggistica istantanea, ma gli utenti devono utilizzare Lync Web App 2013 per partecipare alle riunioni Lync Server 2013.


> [!NOTE]
> Per informazioni dettagliate sulle capacità di coesistenza e interazione dei client di Lync Server 2013 con i client di versioni precedenti di Lync Server e Office Communications Server, vedere <A href="lync-server-2013-client-interoperability-in-lync-2013.md">Interoperabilità dei client in Lync 2013</A> nella documentazione relativa alla pianificazione.


