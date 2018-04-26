---
title: 'Riepilogo porte: SIP, federazione di XMPP e messaggistica istantanea pubblica'
TOCTitle: 'Riepilogo porte: SIP, federazione di XMPP e messaggistica istantanea pubblica'
ms:assetid: ab05bdd6-e9b0-4b1b-9dd9-29ab88e8befe
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ618373(v=OCS.15)
ms:contentKeyID: 49301634
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo porte: SIP, federazione di XMPP e messaggistica istantanea pubblica

 

_**Ultima modifica dell'argomento:** 2015-03-09_

I requisiti di porte, protocolli e firewall per la federazione con Microsoft Lync Server 2013, Lync Server 2010 e Office Communications Server sono simili a quelli per il server perimetrale distribuito. I client avviano la comunicazione con il servizio Access Edge su TLS/SIP/TCP 443. I partner federati invece avvieranno le comunicazioni con il servizio Access Edge su MTLS/SIP/TCP 5061.

Per configurare il firewall per le porte e i protocolli necessari per supportare il servizio di connettività per la messaggistica istantanea pubblica, tenere presente che SIP/MTLS/TCP 5061 è bidirezionale per consentire ai contatti nel provider di servizi di messaggistica istantanea pubblica di contattare i client Lync o per consentire a Lync di contattare i contatti di servizi di messaggistica istantanea pubblica.

Windows Live Messenger può prendere parte alle comunicazioni audio/video con i client Lync. Ciò spiega la configurazione molto simile di porte e protocolli firewall che in genere si imposta nel firewall per supportare i client Lync come utenti esterni.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Oggi più che mai, Lync è un potente strumento per la connessione tra diverse organizzazioni e con utenti di tutto il mondo. La federazione con Windows Live Messenger non richiede ulteriori licenze per utente/dispositivo in aggiunta alla licenza CAL Standard per Lync. La federazione con Skype verrà aggiunta a questo elenco, consentendo agli utenti di Lync di raggiungere centinaia di milioni di persone tramite messaggistica istantanea e comunicazioni vocali.<br />
La federazione con i contatti client di Messenger è ufficialmente terminata il 15 marzo 2013, fatta eccezione per la Cina continentale. Skype diventerà il client federativo per utenti federati che utilizzavano Messenger in precedenza.</td>
</tr>
</tbody>
</table>


Le porte e i protocolli definiti per il proxy XMPP (Extensible Messaging and Presence Protocol) distribuito nel server perimetrale consentono le comunicazioni dal partner federato XMPP al server perimetrale, oltre alle comunicazioni dal server perimetrale al partner federato XMPP. Viene inoltre definita una regola nel firewall esposto all'interno, dal Front End Server o il pool Front End all'server perimetrale o il pool di server perimetrali.

## Riepilogo firewall: federazione SIP


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Ruolo/Protocollo/TCP o UDP/Porta</th>
<th>Indirizzo IP di origine</th>
<th>Indirizzo IP di destinazione</th>
<th>Note</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Access/SIP(MTLS)/TCP/5061</p></td>
<td><p>Indirizzo IP pubblico del servizio Access Edge</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Per la connettività di messaggistica istantanea pubblica e federata con SIP</p></td>
</tr>
</tbody>
</table>


## Riepilogo firewall: connettività per messaggistica istantanea pubblica


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Ruolo/Protocollo/TCP o UDP/Porta</th>
<th>Indirizzo IP di origine</th>
<th>Indirizzo IP di destinazione</th>
<th>Note</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Access/SIP(MTLS)/TCP/5061</p></td>
<td><p>Partner per la connettività per messaggistica istantanea pubblica</p></td>
<td><p>Interfaccia Access server perimetrale</p></td>
<td><p>Per la connettività di messaggistica istantanea pubblica e federata con SIP</p></td>
</tr>
<tr class="even">
<td><p>Access/SIP(MTLS)/TCP/5061</p></td>
<td><p>Interfaccia Access server perimetrale</p></td>
<td><p>Partner per la connettività per messaggistica istantanea pubblica</p></td>
<td><p>Per la connettività di messaggistica istantanea pubblica e federata con SIP</p></td>
</tr>
<tr class="odd">
<td><p>Access/SIP(TLS)/TCP/443</p></td>
<td><p>Client</p></td>
<td><p>Interfaccia Access server perimetrale</p></td>
<td><p>Traffico SIP client-server per l'accesso degli utenti esterni.</p></td>
</tr>
<tr class="even">
<td><p>A/V/RTP/TCP/50.000-59.999</p></td>
<td><p>Interfaccia Access server perimetrale</p></td>
<td><p>Client Live Messenger</p></td>
<td><p>Utilizzato per le sessioni A/V con Windows Live Messenger se è configurata la connettività per messaggistica istantanea pubblica.</p></td>
</tr>
<tr class="odd">
<td><p>A/V/STUN,MSTURN/UDP/3478</p></td>
<td><p>Interfaccia Access server perimetrale</p></td>
<td><p>Client Live Messenger</p></td>
<td><p>Obbligatorio per la connettività per messaggistica istantanea pubblica con Windows Live Messenger.</p></td>
</tr>
<tr class="even">
<td><p>A/V/STUN,MSTURN/UDP/3478</p></td>
<td><p>Client Live Messenger</p></td>
<td><p>Interfaccia Access server perimetrale</p></td>
<td><p>Obbligatorio per la connettività per messaggistica istantanea pubblica con Windows Live Messenger.</p></td>
</tr>
</tbody>
</table>


## Riepilogo firewall: XMPP (Extensible Messaging and Presence Protocol)


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
<td><p>Porta di comunicazione standard da server a server per XMPP. Consente la comunicazione al proxy XMPP di server perimetrale dai partner XMPP federati</p></td>
</tr>
<tr class="even">
<td><p>XMPP/TCP/5269</p></td>
<td><p>Indirizzo IP dell'interfaccia del servizio Access Edge</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Porta di comunicazione standard da server a server per XMPP. Consente la comunicazione dal proxy XMPP di server perimetrale ai partner XMPP federati</p></td>
</tr>
<tr class="odd">
<td><p>XMPP/MTLS/23456</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Indirizzo IP dell'interfaccia interna server perimetrale</p></td>
<td><p>Traffico XMPP interno dal gateway XMPP nel Front End Server o nel pool Front End all'server perimetrale</p></td>
</tr>
</tbody>
</table>


## Vedere anche

#### Concetti

[Scenari per l'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-scenarios-for-external-user-access.md)  
[Determinare i requisiti di porte e firewall A/V esterni per Lync Server 2013](lync-server-2013-determine-external-a-v-firewall-and-port-requirements.md)  

#### Ulteriori risorse

[Gestire i partner federati XMPP per l'organizzazione in Lync Server 2013](lync-server-2013-manage-xmpp-federated-partners-for-your-organization.md)

