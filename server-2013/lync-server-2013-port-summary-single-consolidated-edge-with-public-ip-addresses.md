---
title: "Lync Server 2013: Porte: sing- topolog. perimetr. consolid. c/ indir. IP pubblici"
TOCTitle: Riepilogo delle porte - singola topologia perimetrale consolidata con indirizzi IP pubblici
ms:assetid: 28407acc-8b92-4f78-875c-fd6b4323b602
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204756(v=OCS.15)
ms:contentKeyID: 49299994
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo delle porte - singola topologia perimetrale consolidata con indirizzi IP pubblici in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La funzionalità server perimetrale di Lync Server 2013 descritta in questa architettura di scenario è molto simile a quella implementata in Lync Server 2010. L'aggiunta più significativa è rappresentata dalla voce relativa alla porta **5269 su TCP** per il protocollo XMPP (Extensible Messaging and Presence Protocol). Lync Server 2013 distribuisce facoltativamente un proxy XMPP sul server perimetrale o sul pool di server perimetrali e il server del gateway XMPP sul Front End Server o sul pool Front End. Informazioni sulla pianificazione per il proxy inverso e la federazione sono disponibili nelle sezioni [Scenari per i proxy inversi in Lync Server 2013](lync-server-2013-scenarios-for-reverse-proxy.md) e [Pianificazione per SIP, federazione XMPP e messaggistica istantanea pubblica in Lync Server 2013](lync-server-2013-planning-for-sip-xmpp-federation-and-public-instant-messaging.md), rispettivamente.

Oltre a IPv4, il server perimetrale supporta ora IPv6. Per chiarezza, negli scenari si usa solo IPv4.

**Rete perimetrale aziendale per singolo server perimetrale consolidato con indirizzi IP pubblici**

![Server perimetrale consolidato singolo](images/Gg425891.f8c144c5-e5fb-498a-823e-eb39f26b6847(OCS.15).jpg "Server perimetrale consolidato singolo")

## Informazioni dettagliate relative a porta e protocollo

È consigliabile aprire solo le porte necessarie per supportare le funzionalità per cui si fornisce l'accesso esterno.

Affinché l'accesso remoto funzioni con qualsiasi servizio perimetrale, è necessario consentire il flusso bidirezionale del traffico SIP, come mostrato nella figura relativa al traffico perimetrale in ingresso/in uscita. In altre parole, le funzionalità di messaggistica istantanea (IM), informazioni sulla presenza, Web Conferencing, audio/video (A/V) e federazione comportano l'uso della messaggistica SIP verso e dal servizio Access Edge.

### Riepilogo del firewall per un singolo server perimetrale consolidato con indirizzi IP pubblici: interfaccia esterna

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
<td><p>XMPP/TCP/5269</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Servizio proxy XMPP (condivide l'indirizzo IP con il servizio Access Edge)</p></td>
<td><p>Il servizio proxy XMPP accetta traffico dai contatti XMPP nelle federazioni XMPP definite</p></td>
</tr>
<tr class="even">
<td><p>Accesso/HTTP/TCP/80</p></td>
<td><p>Indirizzo IP pubblico del servizio Access Edge del server perimetrale</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Revoca certificato/Verifica e recupero CRL</p></td>
</tr>
<tr class="odd">
<td><p>Accesso/DNS/TCP/53</p></td>
<td><p>Indirizzo IP pubblico del servizio Access Edge del server perimetrale</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Query DNS su TCP</p></td>
</tr>
<tr class="even">
<td><p>Accesso/DNS/UDP/53</p></td>
<td><p>Indirizzo IP pubblico del servizio Access Edge del server perimetrale</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Query DNS su UDP</p></td>
</tr>
<tr class="odd">
<td><p>Access/SIP(TLS)/TCP/443</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Indirizzo IP pubblico del servizio Access Edge del server perimetrale</p></td>
<td><p>Traffico SIP client-server per l'accesso utente esterno</p></td>
</tr>
<tr class="even">
<td><p>Access/SIP(MTLS)/TCP/5061</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Indirizzo IP pubblico del servizio Access Edge del server perimetrale</p></td>
<td><p>Per connettività di messaggistica istantanea pubblica e federata con SIP</p></td>
</tr>
<tr class="odd">
<td><p>Access/SIP(MTLS)/TCP/5061</p></td>
<td><p>Indirizzo IP pubblico del servizio Access Edge del server perimetrale</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Per connettività di messaggistica istantanea pubblica e federata con SIP</p></td>
</tr>
<tr class="even">
<td><p>Conferenza Web/PSOM(TLS)/TCP/443</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Indirizzo IP pubblico di server perimetrale servizio Web Conferencing Edge</p></td>
<td><p>Contenuti multimediali Web Conferencing</p></td>
</tr>
<tr class="odd">
<td><p>A/V/RTP/TCP/50.000-59.999</p></td>
<td><p>Indirizzo IP pubblico del servizio Access Edge del server perimetrale</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Necessario per la federazione con partner che eseguono Office Communications Server 2007, Office Communications Server 2007 R2, Lync Server 2010 e Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p>A/V/RTP/UDP/50.000-59.999</p></td>
<td><p>Indirizzo IP pubblico del servizio A/V Edge del server perimetrale</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Necessario solo per la federazione con partner che eseguono Office Communications Server 2007.</p></td>
</tr>
<tr class="odd">
<td><p>A/V/RTP/TCP/50.000-59.999</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Indirizzo IP pubblico del servizio A/V Edge del server perimetrale</p></td>
<td><p>Necessario solo per la federazione con partner che eseguono Office Communications Server 2007.</p></td>
</tr>
<tr class="even">
<td><p>A/V/RTP/UDP/50.000-59.999</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Indirizzo IP pubblico del servizio A/V Edge del server perimetrale</p></td>
<td><p>Necessario solo per la federazione con partner che eseguono Office Communications Server 2007.</p></td>
</tr>
<tr class="odd">
<td><p>A/V/STUN,MSTURN/UDP/3478</p></td>
<td><p>Indirizzo IP pubblico del servizio A/V Edge del server perimetrale</p></td>
<td><p>Qualsiasi</p></td>
<td><p>La porta 3478 in uscita viene utilizzata per determinare la versione del server perimetrale con cui comunica Lync Server e anche per il traffico multimediale da un server perimetrale a un server perimetrale. Necessaria per la federazione con Lync Server 2010, Windows Live Messenger e Office Communications Server 2007 R2, nonché per la distribuzione di più pool di server perimetrali all'interno di un'azienda.</p></td>
</tr>
<tr class="even">
<td><p>A/V/STUN,MSTURN/UDP/3478</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Indirizzo IP pubblico del servizio A/V Edge del server perimetrale</p></td>
<td><p>Negoziazione STUN/TURN dei candidati su UDP/3478</p></td>
</tr>
<tr class="odd">
<td><p>A/V/STUN,MSTURN/TCP/443</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Indirizzo IP pubblico del servizio A/V Edge del server perimetrale</p></td>
<td><p>Negoziazione STUN/TURN dei candidati su UDP/443</p></td>
</tr>
<tr class="even">
<td><p>A/V/STUN,MSTURN/TCP/443</p></td>
<td><p>Indirizzo IP pubblico del servizio A/V Edge del server perimetrale</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Negoziazione STUN/TURN dei candidati su UDP/443</p></td>
</tr>
</tbody>
</table>


### Riepilogo del firewall per un singolo server perimetrale consolidato con indirizzi IP pubblici: interfaccia interna

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
<th>Indirizzo IP di origine</th>
<th>Indirizzo IP di destinazione</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>XMPP/MTLS/TCP/23456</p></td>
<td><p>Qualsiasi (può essere definito come IP del server Standard Edition, indirizzo IP del server Standard Edition o indirizzo IP del pool che esegue il servizio XMPP Gateway)</p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Traffico XMPP in uscita dal servizio gateway XMPP in esecuzione in Front End Server o in pool Front End</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>SIP/MTLS/TCP/5061</p></td>
<td><p>Qualsiasi (può essere definito come Server Director, indirizzo IP di pool di server Director, Front End Server o indirizzo IP di pool Front End)</p></td>
<td><p>IP del server perimetrale o pool che conserva l'interfaccia interna</p></td>
<td><p>Traffico SIP in uscita (da Server Director, indirizzo IP di pool di server Director, Front End Server o indirizzo IP di pool Front End) all'interfaccia interna di server perimetrale</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>SIP/MTLS/TCP/5061</p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Qualsiasi (può essere definito come indirizzo IP del Server Director, del pool di server Director, del Front End Server o del pool Front End)</p></td>
<td><p>Traffico SIP in ingresso (a Server Director, indirizzo IP di pool di server Director, Front End Server o indirizzo IP di pool Front End) dall'interfaccia interna di server perimetrale</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>PSOM/MTLS/TCP/8057</p></td>
<td><p>Qualsiasi (può essere definito come indirizzo IP di Front End Server oppure ogni indirizzo IP di Front End Server in un pool Front End)</p>
<p></p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Traffico delle conferenze Web da Front End Server oppure ogni Front End Server se si trova in un pool, all'interfaccia interna di server perimetrale</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>SIP/MTLS/TCP/5062</p></td>
<td><p>Qualsiasi (può essere definito come indirizzo IP del Front End Server, indirizzo IP del pool Front End o qualsiasi Survivable Branch Appliance o Survivable Branch Server che utilizza questo server perimetrale)</p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Autenticazione degli utenti A/V (servizio di autenticazione A/V) dal Front End Server o dall'indirizzo IP del pool Front End oppure da qualsiasi Survivable Branch Appliance o Survivable Branch Server che utilizza questo server perimetrale</p></td>
</tr>
<tr class="even">
<td><p>STUN/MSTURN/UDP/3478</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Percorso preferito per trasferimenti multimediali A/V tra utenti interni ed esterni, Survivable Branch Appliance o Survivable Branch Server</p></td>
</tr>
<tr class="odd">
<td><p>STUN/MSTURN/TCP/443</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Percorso di fallback per il trasferimento multimediale A/V tra utenti interni ed esterni, Survivable Branch Appliance o Survivable Branch Server, se non è possibile stabilire la comunicazione UDP, viene utilizzato TCP per il trasferimento file e la condivisione desktop</p></td>
</tr>
<tr class="even">
<td><p>HTTPS/TCP/4443</p></td>
<td><p>Qualsiasi (può essere definito come indirizzo IP di Front End Server o pool che include archivio di gestione centrale)</p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Replica delle modifiche da archivio di gestione centrale a server perimetrale</p></td>
</tr>
<tr class="odd">
<td><p>MTLS/TCP/50001</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Controller del servizio di registrazione centralizzato con i cmdlet di Lync Server Management Shell e del servizio di registrazione centralizzato, riga di comando ClsController (ClsController.exe) oppure comandi dell'agente (ClsAgent.exe) e raccolta log</p></td>
</tr>
<tr class="even">
<td><p>MTLS/TCP/50002</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Controller del servizio di registrazione centralizzato con i cmdlet di Lync Server Management Shell e del servizio di registrazione centralizzato, riga di comando ClsController (ClsController.exe) oppure comandi dell'agente (ClsAgent.exe) e raccolta log</p></td>
</tr>
<tr class="odd">
<td><p>MTLS/TCP/50003</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Controller del servizio di registrazione centralizzato con i cmdlet di Lync Server Management Shell e del servizio di registrazione centralizzato, riga di comando ClsController (ClsController.exe) oppure comandi dell'agente (ClsAgent.exe) e raccolta log</p></td>
</tr>
</tbody>
</table>


## Riepilogo firewall per la federazione


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
<td><p>Indirizzo IP pubblico di servizio Access Edge</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Per connettività di messaggistica istantanea pubblica e federata con SIP</p></td>
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
<td><p>servizio Access Edge del server perimetrale</p></td>
<td><p>Per connettività di messaggistica istantanea pubblica e federata con SIP</p></td>
</tr>
<tr class="even">
<td><p>Access/SIP(MTLS)/TCP/5061</p></td>
<td><p>servizio Access Edge del server perimetrale</p></td>
<td><p>Partner per la connettività per messaggistica istantanea pubblica</p></td>
<td><p>Per connettività di messaggistica istantanea pubblica e federata con SIP</p></td>
</tr>
<tr class="odd">
<td><p>Access/SIP(TLS)/TCP/443</p></td>
<td><p>Client</p></td>
<td><p>servizio Access Edge del server perimetrale</p></td>
<td><p>Traffico SIP client-server per l'accesso utente esterno</p></td>
</tr>
<tr class="even">
<td><p>A/V/RTP/TCP/50.000-59.999</p></td>
<td><p>servizio A/V Edge del server perimetrale</p></td>
<td><p>Client Live Messenger</p></td>
<td><p>Utilizzato per le sessioni A/V con Windows Live Messenger se è configurata la connettività per messaggistica istantanea pubblica.</p></td>
</tr>
<tr class="odd">
<td><p>A/V/STUN,MSTURN/UDP/3478</p></td>
<td><p>servizio A/V Edge del server perimetrale</p></td>
<td><p>Client Live Messenger</p></td>
<td><p>Obbligatorio per la connettività per messaggistica istantanea pubblica con Windows Live Messenger</p></td>
</tr>
<tr class="even">
<td><p>A/V/STUN,MSTURN/UDP/3478</p></td>
<td><p>Client Live Messenger</p></td>
<td><p>servizio A/V Edge del server perimetrale</p></td>
<td><p>Obbligatorio per la connettività per messaggistica istantanea pubblica con Windows Live Messenger</p></td>
</tr>
</tbody>
</table>


## Riepilogo firewall per XMPP (Extensible Messaging and Presence Protocol)


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
<td><p>Indirizzo IP dell'interfaccia di server perimetrale  servizio Access Edge</p></td>
<td><p>Porta di comunicazione standard da server a server per XMPP. Consente la comunicazione al proxy XMPP di server perimetrale dai partner XMPP federati</p></td>
</tr>
<tr class="even">
<td><p>XMPP/TCP/5269</p></td>
<td><p>Indirizzo IP dell'interfaccia di server perimetrale  servizio Access Edge</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Porta di comunicazione standard da server a server per XMPP. Consente la comunicazione dal proxy XMPP di server perimetrale ai partner XMPP federati</p></td>
</tr>
<tr class="odd">
<td><p>XMPP/MTLS/TCP/23456</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Ogni IP dell'interfaccia interna di server perimetrale</p></td>
<td><p>Traffico XMPP interno dal gateway XMPP nel Front End Server o pool Front End all'indirizzo IP di server perimetrale o all'indirizzo IP interno di ogni membro del pool di server perimetrali</p></td>
</tr>
</tbody>
</table>

