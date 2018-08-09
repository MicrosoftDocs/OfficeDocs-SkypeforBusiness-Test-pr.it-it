---
title: "Lync Server 2013: Riepilogo porte - bilanciam. carico DNS e carico hardware"
TOCTitle: Riepilogo delle porte - bilanciamento del carico DNS e bilanciamento del carico hardware
ms:assetid: b07c37e4-820e-46ee-a678-1da95d1b87af
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205179(v=OCS.15)
ms:contentKeyID: 49301686
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo delle porte - bilanciamento del carico DNS e bilanciamento del carico hardware in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

I requisiti delle porte di firewall per un singolo Server Director riguardano le porte utilizzate per stabilire la comunicazione con il Server Director dall'interfaccia interna o dalla rete rivolta verso l'interno del proxy inverso. Per impostazione predefinita, Microsoft Lync Server 2013 prevede che le porte HTTP/TCP 8080 e HTTPS/TCP 4443 siano aperte dal proxy inverso al Server Director, nonché al pool Front End e al Front End Server. Deve inoltre esservi comunicazione SIP (Session Initiation Protocol) dall'interfaccia interna del server perimetrale al Server Director e al pool Front End e al Front End Server. Il protocollo SIP utilizza SIP/MTLS/TCP 5061 dal server perimetrale al pool Front End e al Front End Server. Deve inoltre essere creata una regola che consenta la comunicazione SIP/MTLS/TCP 5061 dal Server Director, dal pool Front End e dal Front End Server all'interfaccia interna del server perimetrale.

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
<td><p>VIP del bilanciamento del carico hardware del Server Director</p></td>
<td><p>Ricevuta inizialmente dal lato esterno del proxy inverso, la comunicazione viene inviata al VIP del bilanciamento del carico hardware del Server Director e ai servizi Web del Front End Server.</p></td>
</tr>
<tr class="even">
<td><p>HTTPS/TCP 4443</p></td>
<td><p>Interfaccia interna del proxy inverso</p></td>
<td><p>VIP del bilanciamento del carico hardware del Server Director</p></td>
<td><p>Ricevuta inizialmente dal lato esterno del proxy inverso, la comunicazione viene inviata al VIP del bilanciamento del carico hardware del Server Director e ai servizi Web del Front End Server.</p></td>
</tr>
<tr class="odd">
<td><p>HTTPS/TCP 444</p></td>
<td><p>Server Director</p></td>
<td><p>pool Front End o Front End Server</p></td>
<td><p>Comunicazione tra server tra il VIP del bilanciamento del carico hardware del Server Director e il Front End Server o i Front End Server.</p></td>
</tr>
<tr class="even">
<td><p>HTTP/TCP 80</p></td>
<td><p>Client interni</p></td>
<td><p>VIP del bilanciamento del carico hardware del Server Director</p></td>
<td><p>Il Server Director fornisce i servizi Web ai client sia interni che esterni.</p></td>
</tr>
<tr class="odd">
<td><p>HTTPS/TCP 443</p></td>
<td><p>Client interni</p></td>
<td><p>VIP del bilanciamento del carico hardware del Server Director</p></td>
<td><p>Il Server Director fornisce i servizi Web ai client sia interni che esterni.</p></td>
</tr>
<tr class="even">
<td><p>SIP/MTLS/TCP 5061</p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Server Director</p></td>
<td><p>Comunicazione SIP dal server perimetrale al Server Director e ai Front End Server.</p></td>
</tr>
<tr class="odd">
<td><p>MTLS/TCP/50001</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Server Director</p></td>
<td><p>Raccolta log e comandi del controller (ClsController.exe) o dell'agente (ClsAgent.exe) del servizio di registrazione centralizzato</p></td>
</tr>
<tr class="even">
<td><p>MTLS/TCP/50002</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Server Director</p></td>
<td><p>Raccolta log e comandi del controller (ClsController.exe) o dell'agente (ClsAgent.exe) del servizio di registrazione centralizzato</p></td>
</tr>
<tr class="odd">
<td><p>MTLS/TCP/50003</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Server Director</p></td>
<td><p>Raccolta log e comandi del controller (ClsController.exe) o dell'agente (ClsAgent.exe) del servizio di registrazione centralizzato</p></td>
</tr>
</tbody>
</table>

