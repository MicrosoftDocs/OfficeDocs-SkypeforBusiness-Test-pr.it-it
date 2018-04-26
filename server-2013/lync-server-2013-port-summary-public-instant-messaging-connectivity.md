---
title: Riepilogo delle porte - connettività per messaggistica istantanea pubblica
TOCTitle: Riepilogo delle porte - connettività per messaggistica istantanea pubblica
ms:assetid: f46756ec-1401-4ca2-a4a4-5cd28bcfdc7f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ618376(v=OCS.15)
ms:contentKeyID: 49302476
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo delle porte - connettività per messaggistica istantanea pubblica

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per configurare il firewall per le porte e i protocolli necessari per supportare il servizio di connettività per la messaggistica istantanea pubblica, si tenga presente che SIP/MTLS/TCP 5061 è bidirezionale per consentire ai contatti nel provider di servizi di messaggistica istantanea pubblica di contattare i client Lync o per consentire a Lync di contattare i contatti di servizi di messaggistica istantanea pubblica.

Windows Live Messenger può prendere parte alle comunicazioni audio/video con i client di Lync. Questo avviene grazie alla configurazione molto simile di porte e protocolli firewall che in genere è necessaria nel firewall per supportare i client di Lync come utenti esterni.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Oggi più che mai, Lync è un potente strumento per la connessione tra diverse organizzazioni e con utenti di tutto il mondo. La federazione con Windows Live Messenger non richiede ulteriori licenze per utente/dispositivo in aggiunta alla licenza CAL Standard per Lync. La federazione con Skype verrà aggiunta a questo elenco, consentendo agli utenti di Lync di raggiungere centinaia di milioni di persone tramite messaggistica istantanea e comunicazioni vocali.<br />
La federazione con i contatti client di Messenger avrà ufficialmente termine il 15 marzo 2013, fatta eccezione per la Cina continentale. Skype diventerà il client federativo per utenti federati che utilizzavano Messenger in precedenza.</td>
</tr>
</tbody>
</table>


## Riepilogo firewall - connettività per messaggistica istantanea pubblica


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
<td><p>Access/SIP(MTLS)/TCP/5061</p></td>
<td><p>Partner per la connettività per messaggistica istantanea pubblica</p></td>
<td><p>Interfaccia di server perimetrale Access</p></td>
<td><p>Per connettività di messaggistica istantanea pubblica e federata con SIP</p></td>
</tr>
<tr class="even">
<td><p>Access/SIP(MTLS)/TCP/5061</p></td>
<td><p>Interfaccia di server perimetrale Access</p></td>
<td><p>Partner per la connettività per messaggistica istantanea pubblica</p></td>
<td><p>Per connettività di messaggistica istantanea pubblica e federata con SIP</p></td>
</tr>
<tr class="odd">
<td><p>Access/SIP(TLS)/TCP/443</p></td>
<td><p>Client</p></td>
<td><p>Interfaccia di server perimetrale Access</p></td>
<td><p>Traffico SIP client-server per l'accesso degli utenti esterni.</p></td>
</tr>
<tr class="even">
<td><p>A/V/RTP/TCP/50.000-59.999</p></td>
<td><p>Interfaccia di server perimetrale Access</p></td>
<td><p>Client Live Messenger</p></td>
<td><p>Utilizzato per le sessioni A/V con Windows Live Messenger se è configurata la connettività per messaggistica istantanea pubblica.</p></td>
</tr>
<tr class="odd">
<td><p>A/V/STUN,MSTURN/UDP/3478</p></td>
<td><p>Interfaccia di server perimetrale Access</p></td>
<td><p>Client Live Messenger</p></td>
<td><p>Obbligatorio per la connettività per messaggistica istantanea pubblica con Windows Live Messenger.</p></td>
</tr>
<tr class="even">
<td><p>A/V/STUN,MSTURN/UDP/3478</p></td>
<td><p>Client Live Messenger</p></td>
<td><p>Interfaccia di server perimetrale Access</p></td>
<td><p>Obbligatorio per la connettività per messaggistica istantanea pubblica con Windows Live Messenger.</p></td>
</tr>
</tbody>
</table>


## Vedere anche

#### Concetti

[Scenari per l'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-scenarios-for-external-user-access.md)  
[Determinare i requisiti di porte e firewall A/V esterni per Lync Server 2013](lync-server-2013-determine-external-a-v-firewall-and-port-requirements.md)

