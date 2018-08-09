---
title: "Lync Server 2013: Porte: pool di Director c/ scalab., bilanciam. carico hw"
TOCTitle: Riepilogo delle porte - pool di server Director con scalabilità implementata, servizio di bilanciamento del carico hardware
ms:assetid: 6ae2f4ac-5b64-4e45-8253-133308f5812d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204983(v=OCS.15)
ms:contentKeyID: 49300880
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo delle porte - pool di server Director con scalabilità implementata, servizio di bilanciamento del carico hardware in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

I requisiti delle porte firewall per un pool di server Director consistono nelle porte utilizzate per stabilire la comunicazione con il Server Director dall'interfaccia interna del server perimetrale o dall'interfaccia rivolta verso l'interno del proxy inverso. Microsoft Lync Server 2013, per impostazione predefinita, suppone che le porte HTTP/TCP 8080 e HTTPS/TCP 4443 siano aperte per il proxy inverso al Server Director, al pool Front End e al Front End Server. Inoltre, deve esserci comunicazione di tipo SIP (Session Initiation Protocol) dall'interfaccia interna dell' server perimetrale al Server Director e al pool Front End e Front End Server. Il protocollo SIP si serve di SIP/MTLS/TCP 5061 dall' server perimetrale al pool Front End e Front End Server. Deve essere inoltre creata una regola che consente la comunicazione SIP/MTLS/TCP 5061 dal Server Director, pool Front End e Front End Server all'interfaccia interna del server perimetrale.

### Porte director e protocollo per le definizioni firewall

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
<td><p>Ricevuta inizialmente dal lato esterno del proxy inverso, la comunicazione è a sua volta inviata al VIP HLB di Server Director e ai servizi web di Front End Server</p></td>
</tr>
<tr class="even">
<td><p>HTTPS/TCP 4443</p></td>
<td><p>Interfaccia interna del proxy inverso</p></td>
<td><p>VIP del bilanciamento del carico hardware del Server Director</p></td>
<td><p>Ricevuta inizialmente dal lato esterno del proxy inverso, la comunicazione è a sua volta inviata al VIP HLB di Server Director e ai servizi web di Front End Server</p></td>
</tr>
<tr class="odd">
<td><p>HTTPS/TCP 444</p></td>
<td><p>Server Director</p></td>
<td><p>Front End Server o pool Front End</p></td>
<td><p>Comunicazioni interne ai server tra VIP HLB di Server Director e Front End Server</p></td>
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
<td><p>VIP del bilanciamento del carico hardware del Server Director</p></td>
<td><p>Comunicazione SIP da server perimetrale a Server Director e Front End Server.</p></td>
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

