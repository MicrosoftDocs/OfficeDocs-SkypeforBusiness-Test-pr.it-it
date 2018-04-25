---
title: Riepilogo delle porte - federazione di XMPP (Extensible Messaging and Presence Protocol)
TOCTitle: Riepilogo delle porte - federazione di XMPP (Extensible Messaging and Presence Protocol)
ms:assetid: 62e98fab-7add-4983-a3fa-dbe74e1c3849
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ618371(v=OCS.15)
ms:contentKeyID: 49300774
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo delle porte - federazione di XMPP (Extensible Messaging and Presence Protocol)

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Le porte e i protocolli definiti per il proxy XMPP (Extensible Messaging and Presence Protocol) distribuito nel server perimetrale consentono le comunicazioni dal partner federato XMPP al server perimetrale e consentono inoltre le comunicazioni dal server perimetrale al partner federato XMPP. Viene inoltre definita una regola nel firewall esposto all'interno, dal Front End Server o il pool Front End al server perimetrale o il pool di server perimetrali.

## Riepilogo delle impostazioni del firewall per il protocollo XMPP


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Protocollo/TCP o UDP/porta</th>
<th>Origine (indirizzo IP)</th>
<th>Destinazione (indirizzo IP)</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>XMPP/TCP/5269</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Indirizzo IP dell'interfaccia del servizio Access Edge</p></td>
<td><p>Porta di comunicazione server-server standard per XMPP. Consente le comunicazioni al proxy XMPP del server perimetrale dai partner XMPP federati</p></td>
</tr>
<tr class="even">
<td><p>XMPP/TCP/5269</p></td>
<td><p>Indirizzo IP dell'interfaccia del servizio Access Edge</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Porta di comunicazione server-server standard per XMPP. Consente le comunicazioni dal proxy XMPP del server perimetrale ai partner XMPP federati</p></td>
</tr>
<tr class="odd">
<td><p>XMPP/MTLS/23456</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Indirizzo IP dell'interfaccia interna del server perimetrale</p></td>
<td><p>Traffico XMPP interno dal gateway XMPP nel Front End Server o nel pool Front End al server perimetrale</p></td>
</tr>
</tbody>
</table>


## Vedere anche

#### Attività

[Esempio di configurazione XMPP in Lync Server 2013 - federazione di XMPP con Google Talk](lync-server-2013-example-xmpp-configuration-–-xmpp-federation-with-google-talk.md)  

#### Ulteriori risorse

[Gestire i partner federati XMPP per l'organizzazione in Lync Server 2013](lync-server-2013-manage-xmpp-federated-partners-for-your-organization.md)

