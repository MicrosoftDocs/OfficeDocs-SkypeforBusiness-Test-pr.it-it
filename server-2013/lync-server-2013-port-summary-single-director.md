---
title: 'Lync Server 2013: Riepilogo delle porte - singolo server Director'
TOCTitle: Riepilogo delle porte - singolo server Director
ms:assetid: 079c1414-723f-4499-b7d4-a0d7121c1626
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204648(v=OCS.15)
ms:contentKeyID: 49299584
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo delle porte - singolo server Director in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

I requisiti delle porte firewall per un Server Director singolo sono rappresentati dalle porte utilizzate per stabilire la comunicazione con il Director dall'interfaccia interna o dalla rete rivolta verso l'interno del proxy inverso. Per impostazione predefinita, in Microsoft Lync Server 2013 è prevista l'apertura delle porte HTTP/TCP 8080 e HTTPS/TCP 4443 dal proxy inverso al Server Director, nonché al pool Front End e al Front End Server. Deve inoltre esistere comunicazione SIP (Session Initiation Protocol) dall'interfaccia interna del server perimetrale al Server Director, al pool Front End e al Front End Server. Il protocollo SIP usa SIP/MTLS/TCP 5061 dal server perimetrale al pool Front End e al Front End Server. È inoltre necessario creare una regola che consenta la comunicazione SIP/MTLS/TCP 5061 dal Server Director, il pool Front End e il Front End Server all'interfaccia interna del server perimetrale.

### Porte e protocolli di un singolo Server Director per le definizioni di firewall

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Ruolo/protocollo/TCP o UDP/porta</th>
<th>Indirizzo IP di origine</th>
<th>Indirizzo IP di destinazione</th>
<th>Note</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HTTP/TCP 8080</p></td>
<td><p>Interfaccia interna del proxy inverso</p></td>
<td><p>Server Director</p></td>
<td><p>Inizialmente ricevuta dal lato esterno del proxy inverso, la comunicazione viene inviata ai servizi Web del Server Director e del Front End Server</p></td>
</tr>
<tr class="even">
<td><p>HTTPS/TCP 4443</p></td>
<td><p>Interfaccia interna del proxy inverso</p></td>
<td><p>Server Director</p></td>
<td><p>Inizialmente ricevuta dal lato esterno del proxy inverso, la comunicazione viene inviata ai servizi Web del Server Director e del Front End Server</p></td>
</tr>
<tr class="odd">
<td><p>HTTPS/TCP 444</p></td>
<td><p>Server Director</p></td>
<td><p>Front End Server o pool Front End</p></td>
<td><p>Comunicazioni interne tra Server Director e Front End Server</p></td>
</tr>
<tr class="even">
<td><p>HTTP/TCP 80</p></td>
<td><p>Client interni</p></td>
<td><p>Servizi Web Server Director</p></td>
<td><p>Il Server Director fornisce servizi Web ai client interni ed esterni.</p></td>
</tr>
<tr class="odd">
<td><p>HTTPS/TCP 443</p></td>
<td><p>Client interni</p></td>
<td><p>Servizi Web Server Director</p></td>
<td><p>Il Server Director fornisce servizi Web ai client interni ed esterni.</p></td>
</tr>
<tr class="even">
<td><p>SIP/MTLS/TCP 5061</p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Server Director</p></td>
<td><p>Comunicazione SIP dal server perimetrale al Server Director e al Front End Server.</p></td>
</tr>
<tr class="odd">
<td><p>MTLS/TCP/50001</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Comandi e raccolta log del controller (ClsController.exe) o dell'agente (ClasAgent.exe) del servizio di registrazione centralizzato</p></td>
</tr>
<tr class="even">
<td><p>MTLS/TCP/50002</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Comandi e raccolta log del controller (ClsController.exe) o dell'agente (ClasAgent.exe) del servizio di registrazione centralizzato</p></td>
</tr>
<tr class="odd">
<td><p>MTLS/TCP/50003</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Comandi e raccolta log del controller (ClsController.exe) o dell'agente (ClasAgent.exe) del servizio di registrazione centralizzato</p></td>
</tr>
</tbody>
</table>

