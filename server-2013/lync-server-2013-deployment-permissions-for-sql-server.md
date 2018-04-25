---
title: 'Lync Server 2013: Autorizzazioni di distribuzione per SQL Server'
TOCTitle: Autorizzazioni di distribuzione per SQL Server
ms:assetid: 56ea0c02-bcf5-4d45-aa13-570531c29074
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398375(v=OCS.15)
ms:contentKeyID: 49300585
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Autorizzazioni di distribuzione per SQL Server in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Microsoft SQL Server 2012 ha requisiti specifici quando si installa e distribuisce Lync Server 2013. Poiché Windows e SQL Server presentano una diversa definizione dei rispettivi sistemi di sicurezza, l'accesso come amministratori nel dominio Active Directory non implica la concessione delle autorizzazioni per SQL Server. È inoltre necessario essere membri dell'entità sysadmin nel server basato su SQL Server che si sta configurando.

## Autorizzazioni necessarie per l'installazione dei database e di Lync Server

Le opzioni seguenti descrivono in dettaglio tre associazioni di autorizzazioni e appartenenze a gruppi per l'installazione dei file di Lync Server 2013 e dei database di SQL Server. Scegliere lo scenario più adatto ai requisiti specifici dell'organizzazione.

### Associazioni di autorizzazioni e appartenenze ai gruppi

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Ruolo di SQL Server o Lync Server 2013</th>
<th>Autorizzazioni e appartenenze ai gruppi di SQL Server tipiche del ruolo</th>
<th>Autorizzazioni e appartenenze ai gruppi di Lync Server 2013 tipiche del ruolo</th>
<th>Risultati delle autorizzazioni</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Amministratore di Lync Server 2013</p></td>
<td><p>Deve appartenere al gruppo di sicurezza sysadmins di SQL Server ed essere membro del gruppo Administrators locale di SQL Server</p></td>
<td><p>Deve essere un membro del gruppo RTCUniversalServerAdmins</p></td>
<td><p>L'amministratore di Lync Server 2013 deve disporre delle autorizzazioni appropriate per installare sia Lync Server 2013 che i database di SQL Server.</p></td>
</tr>
<tr class="even">
<td><p>Amministratore di SQL Server</p></td>
<td><p>Membro del gruppo sysadmins di SQL Server (o equivalente) e membro del gruppo Administrators locale di SQL Server</p></td>
<td><p>Deve essere un membro del gruppo RTCUniversalServerReadOnly</p></td>
<td><p>L'amministratore di SQL Server deve disporre delle autorizzazioni appropriate per installare sia Lync Server 2013 che i database di SQL Server.</p></td>
</tr>
<tr class="odd">
<td><p>Entrambi gli amministratori condividono responsabilità per l'installazione</p></td>
<td><p>L'amministratore di SQL Server è membro del gruppo sysadmins (o equivalente) e membro del gruppo Administrarors locale di SQL Server</p></td>
<td><p>L'amministratore di Lync Server 2013 è membro di RTCUniversalServerAdmins</p></td>
<td><p>L'amministratore di Lync Server 2013 può installare Lync Server 2013, ma non i database. L'amministratore di SQL Server utilizza i cmdlet Lync Server Management Shell e Windows PowerShell forniti dall'amministratore di Lync Server 2013 per installare i database. Lo strumento Lync Server 2013 Management Shell utilizzato dall'amministratore di SQL Server è installato nel Front End Server. Ciò evita la necessità di installare gli strumenti di amministrazione di Lync Server 2013 nel server basato su SQL Server.</p></td>
</tr>
</tbody>
</table>

