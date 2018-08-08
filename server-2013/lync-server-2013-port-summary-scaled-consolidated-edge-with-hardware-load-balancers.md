---
title: "Lync Server 2013: Porte: topol. perim. consolid. c/ scalab. implem., bilanc. carico hw"
TOCTitle: Riepilogo delle porte - topologia perimetrale consolidata con scalabilità implementata e servizi di bilanciamento del carico hardware
ms:assetid: 91213b1e-f875-464b-83e8-fe3a351595a4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398739(v=OCS.15)
ms:contentKeyID: 49301323
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo delle porte - topologia perimetrale consolidata con scalabilità implementata e servizi di bilanciamento del carico hardware in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-04-27_

La caratteristica di server perimetrale di Lync Server 2013 descritta nell'architettura dello scenario è analoga all'implementazione in Lync Server 2010. L'aggiunta più evidente è la voce relativa alla porta **5269 su TCP** per il protocollo XMPP (Extensible Messaging and Presence Protocol). Lync Server 2013 offre, se lo si desidera, la possibilità di distribuire un proxy XMPP nel server perimetrale o nel pool di server perimetrali e il server gateway XMPP nel Front End Server o nel pool Front End.

Oltre a IPv4, il server perimetrale supporta ora IPv6. Per chiarezza, negli scenari si usa solo IPv4.

**Server perimetrale consolidato in scala con bilanciamento del carico hardware**

![Porte e protocolli della rete perimetrale del server perimetrale](images/Gg398739.063f7dd1-16db-4cc7-8708-bca9bc41184d(OCS.15).jpg "Porte e protocolli della rete perimetrale del server perimetrale")

## Informazioni dettagliate relative a porta e protocollo

È consigliabile aprire solo le porte necessarie al supporto della funzionalità per cui si desidera fornire accesso esterno.

Affinché l'accesso remoto funzioni per qualsiasi servizio perimetrale, è necessario che il flusso del traffico SIP possa passare in modo bidirezionale come illustrato nella figura relativa al traffico perimetrale in ingresso e in uscita. In altre parole, i messaggi SIP in arrivo e in uscita nel servizio Access Edge sono coinvolti in messaggistica istantanea, presenza, conferenze Web, contenuti audio/video e federazione.

### Riepilogo firewall per topologia perimetrale consolidata, carico hardware bilanciato: interfaccia esterna - Nodo 1 e Nodo 2 (Esempio)

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
<td><p>Accesso/HTTP/TCP/80</p></td>
<td><p>Indirizzo IP pubblico del servizio Access Edge del server perimetrale</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Revoca certificato/Verifica e recupero CRL</p></td>
</tr>
<tr class="even">
<td><p>Accesso/DNS/TCP/53</p></td>
<td><p>Indirizzo IP pubblico del servizio Access Edge del server perimetrale</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Query DNS su TCP</p></td>
</tr>
<tr class="odd">
<td><p>Accesso/DNS/UDP/53</p></td>
<td><p>Indirizzo IP pubblico del servizio Access Edge del server perimetrale</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Query DNS su UDP</p></td>
</tr>
<tr class="even">
<td><p>A/V/RTP/TCP/50.000-59.999</p></td>
<td><p>Indirizzo IP del  servizio A/V Edge del server perimetrale</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Necessario per la federazione con partner che eseguono Office Communications Server 2007, Office Communications Server 2007 R2, Lync Server 2010 e Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p>A/V/RTP/UDP/50.000-59.999</p></td>
<td><p>Indirizzo IP pubblico del servizio A/V Edge del server perimetrale</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Necessario solo per la federazione con partner che eseguono Office Communications Server 2007.</p></td>
</tr>
<tr class="even">
<td><p>A/V/RTP/TCP/50.000-59.999</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Indirizzo IP pubblico del servizio A/V Edge del server perimetrale</p></td>
<td><p>Necessario solo per la federazione con partner che eseguono Office Communications Server 2007.</p></td>
</tr>
<tr class="odd">
<td><p>A/V/RTP/UDP/50.000-59.999</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Indirizzo IP pubblico del servizio A/V Edge del server perimetrale</p></td>
<td><p>Necessario solo per la federazione con partner che eseguono Office Communications Server 2007.</p></td>
</tr>
<tr class="even">
<td><p>A/V/STUN,MSTURN/UDP/3478</p></td>
<td><p>Indirizzo IP pubblico del servizio A/V Edge del server perimetrale</p></td>
<td><p>Qualsiasi</p></td>
<td><p>La porta 3478 in uscita viene utilizzata per determinare la versione del server perimetrale con cui comunica Lync Server e anche per il traffico multimediale da un server perimetrale a un server perimetrale. Necessaria per la federazione con Lync Server 2010, Windows Live Messenger e Office Communications Server 2007 R2, nonché per la distribuzione di più pool di server perimetrali all'interno di un'azienda.</p></td>
</tr>
<tr class="odd">
<td><p>A/V/STUN,MSTURN/UDP/3478</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Indirizzo IP pubblico del servizio A/V Edge del server perimetrale</p></td>
<td><p>Negoziazione STUN/TURN dei candidati su UDP/3478</p></td>
</tr>
<tr class="even">
<td><p>A/V/STUN,MSTURN/TCP/443</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Indirizzo IP pubblico del servizio A/V Edge del server perimetrale</p></td>
<td><p>Negoziazione STUN/TURN dei candidati su UDP/443</p></td>
</tr>
<tr class="odd">
<td><p>A/V/STUN,MSTURN/TCP/443</p></td>
<td><p>Indirizzo IP pubblico del servizio A/V Edge del server perimetrale</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Negoziazione STUN/TURN dei candidati su UDP/443</p></td>
</tr>
</tbody>
</table>


### Riepilogo firewall per topologia perimetrale consolidata, carico hardware bilanciato: interfaccia interna - Nodo 1 e Nodo 2

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
<td><p>XMPP/MTLS/TCP/23456</p></td>
<td><p>Qualsiasi (può essere definito come indirizzo del Front End Server o indirizzo IP virtuale del pool Front End che esegue il servizio gateway XMPP)</p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Traffico XMPP in uscita dal servizio gateway XMPP in esecuzione in Front End Server o in pool Front End</p></td>
</tr>
<tr class="even">
<td><p>HTTPS/TCP/4443</p></td>
<td><p>Qualsiasi (definibile come IP del server Front End Server o pool contenente archivio di gestione centrale)</p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Replica delle modifiche da archivio di gestione centrale a server perimetrale</p></td>
</tr>
<tr class="odd">
<td><p>PSOM/MTLS/TCP/8057</p></td>
<td><p>Qualsiasi (definibile come IP del Server Director, IP del Front End Server o IP virtuale del pool)</p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Traffico di conferenze Web da distribuzione interna a interfaccia server perimetrale interna</p></td>
</tr>
<tr class="even">
<td><p>STUN/MSTURN/UDP/3478</p></td>
<td><p>Qualsiasi (definibile come IP del Server Director, IP del Front End Server o IP virtuale del pool)</p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Percorso preferito per trasferimenti multimediali A/V tra utenti interni ed esterni, Survivable Branch Appliance o Survivable Branch Server</p></td>
</tr>
<tr class="odd">
<td><p>STUN/MSTURN/TCP/443</p></td>
<td><p>Qualsiasi (definibile come IP del Server Director, IP del Front End Server o IP virtuale del pool)</p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Percorso di fallback per il trasferimento multimediale A/V tra utenti interni ed esterni, Survivable Branch Appliance o Survivable Branch Server, se non è possibile stabilire la comunicazione UDP, viene utilizzato TCP per il trasferimento file e la condivisione desktop</p></td>
</tr>
<tr class="even">
<td><p>MTLS/TCP/50001</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Controller del servizio di registrazione centralizzato con i cmdlet di Lync Server Management Shell e del servizio di registrazione centralizzato, riga di comando ClsController (ClsController.exe) oppure comandi dell'agente (ClsAgent.exe) e raccolta log</p></td>
</tr>
<tr class="odd">
<td><p>MTLS/TCP/50002</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Controller del servizio di registrazione centralizzato con i cmdlet di Lync Server Management Shell e del servizio di registrazione centralizzato, riga di comando ClsController (ClsController.exe) oppure comandi dell'agente (ClsAgent.exe) e raccolta log</p></td>
</tr>
<tr class="even">
<td><p>MTLS/TCP/50003</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Interfaccia interna server perimetrale</p></td>
<td><p>Controller del servizio di registrazione centralizzato con i cmdlet di Lync Server Management Shell e del servizio di registrazione centralizzato, riga di comando ClsController (ClsController.exe) oppure comandi dell'agente (ClsAgent.exe) e raccolta log</p></td>
</tr>
</tbody>
</table>


I servizi di bilanciamento del carico hardware presentano specifici requisiti se vengono distribuiti per offrire disponibilità e bilanciamento del carico per Lync Server. Questi requisiti sono definiti nella figura e nelle tabelle seguenti. I fornitori di terze parti possono usare termini diversi per i requisiti definiti qui. È necessario mappare i requisiti di Lync Server alle caratteristiche e alle opzioni di configurazione indicate dal fornitore del servizio di bilanciamento del carico hardware.

Quando si configurano servizi di bilanciamento del carico hardware, tenere presenti i requisiti seguenti:

  - Nel servizio di bilanciamento del carico hardware è possibile configurare SNAT (Source Network Address Translation) per servizio Access Edge e servizio Web Conferencing Edge

  - Non è possibile configurare SNAT in servizio A/V Edge: il servizio A/V Edge deve rispondere con l'indirizzo del server reale e non con l'IP virtuale del servizio di bilanciamento del carico hardware affinché l'attraversamento di UDP su NAT (STUN) o l'attraversamento mediante NAT di inoltro (TURN) o la federazione TURN (FTURN) funzioni correttamente

  - Vengono utilizzati indirizzi IP pubblici in ogni interfaccia server e per gli indirizzi IP virtuali del servizio di bilanciamento del carico hardware e i requisiti degli indirizzi IP pubblici sono N+1, dove esiste un indirizzo IP pubblico per ogni interfaccia server reale e uno per ogni indirizzo IP virtuale del servizio di bilanciamento del carico hardware. Nei casi in cui sono presenti 2 server perimetrali nel pool, ciò produce 9 indirizzi IP pubblici di cui 3 usati per gli indirizzi IP virtuali del servizio di bilanciamento del carico hardware e uno per ogni interfaccia di server perimetrale (per un totale di sei server)

  - Per servizio Access Edge e servizio Web Conferencing Edge, (e con NAT sul servizio di bilanciamento del carico hardware) il client contatta l'indirizzo VIP, il quale modifica l'indirizzo IP di origine del client impostandolo sul proprio indirizzo IP. L'interfaccia server invia l'indirizzo restituito all'indirizzo VIP, il quale cambia l'indirizzo di origine dall'indirizzo IP dell'interfaccia server e invia il pacchetto al client

  - Per il servizio A/V Edge, l'indirizzo VIP NON deve cambiare l'indirizzo IP di origine e l'indirizzo del server reale viene restituito direttamente al client. Non è possibile configurare NAT sul servizio di bilanciamento del carico hardware per il traffico A/V

  - Per i contenuti A/V, il firewall esterno deve mantenere l'indirizzo IP pubblico del server reale per tutti i pacchetti

  - Una volta stabilita, la connessione tra il client e servizio A/V Edge avviene al server reale e non al servizio di bilanciamento del carico hardware

  - La topologia perimetrale interna deve essere instradata ai server e client interni e le route persistenti sono impostate per tutte le reti interne che ospitano server o client

  - L'indirizzo VIP del servizio Access Edge del servizio di bilanciamento del carico hardware agisce come gateway predefinito per ogni interfaccia di server perimetrale

![Dettagli su porte e protocolli del server perimetrale](images/Gg398739.1c193b80-98ab-4d59-a854-dbfdb5e209e2(OCS.15).jpg "Dettagli su porte e protocolli del server perimetrale")

### Impostazioni delle porte esterne necessarie per la topologia perimetrale consolidata, carico hardware bilanciato: IP virtuali interfaccia esterna

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
<td><p>XMPP/TCP/5269</p></td>
<td><p>Servizio proxy XMPP (condivide l'indirizzo IP con il servizio Access Edge)</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Il servizio proxy XMPP invia il traffico ai contatti XMPP in federazioni XMPP definite</p></td>
</tr>
<tr class="odd">
<td><p>Access/SIP(TLS)/TCP/443</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Indirizzo VIP pubblico del servizio Access Edge</p></td>
<td><p>Traffico SIP client-server per l'accesso utente esterno</p></td>
</tr>
<tr class="even">
<td><p>Access/SIP(MTLS)/TCP/5061</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Indirizzo VIP pubblico del servizio Access Edge</p></td>
<td><p>Segnalazione SIP, connettività IM federata e pubblica con SIP</p></td>
</tr>
<tr class="odd">
<td><p>Access/SIP(MTLS)/TCP/5061</p></td>
<td><p>Indirizzo VIP pubblico del servizio Access Edge</p></td>
<td><p>Partner federato</p></td>
<td><p>Segnalazione SIP, connettività IM federata e pubblica con SIP</p></td>
</tr>
<tr class="even">
<td><p>Conferenza Web/PSOM(TLS)/TCP/443</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Indirizzo VIP pubblico del servizio Web Conferencing Edge del server perimetrale</p></td>
<td><p>Contenuti multimediali Web Conferencing</p></td>
</tr>
<tr class="odd">
<td><p>A/V/STUN,MSTURN/UDP/3478</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Indirizzo VIP pubblico del servizio A/V Edge del server perimetrale</p></td>
<td><p>Negoziazione STUN/TURN dei candidati su UDP/3478</p></td>
</tr>
<tr class="even">
<td><p>A/V/STUN,MSTURN/TCP/443</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Indirizzo VIP pubblico del servizio A/V Edge del server perimetrale</p></td>
<td><p>Negoziazione STUN/TURN dei candidati su UDP/443</p></td>
</tr>
</tbody>
</table>


### Riepilogo firewall per topologia perimetrale consolidata, carico hardware bilanciato: IP virtuali interfaccia interna

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
<td><p>Qualsiasi (può essere definito come Server Director, indirizzo IP virtuale del pool di server Director, Front End Server o indirizzo IP virtuale del pool Front End)</p></td>
<td><p>Interfaccia VIP interna di server perimetrale</p></td>
<td><p>Traffico SIP in uscita (dal Server Director, indirizzo IP virtuale del pool di server Director, Front End Server o indirizzo IP virtuale del pool Front End) verso l'indirizzo VIP della topologia perimetrale interna</p></td>
</tr>
<tr class="even">
<td><p>Access/SIP(MTLS)/TCP/5061</p></td>
<td><p>Interfaccia VIP interna di server perimetrale</p></td>
<td><p>Qualsiasi (può essere definito come Server Director, indirizzo IP virtuale del pool di server Director, Front End Server o indirizzo IP virtuale del pool Front End)</p></td>
<td><p>Traffico SIP in ingresso (verso Server Director, indirizzo IP virtuale del pool di server Director, Front End Server o indirizzo IP virtuale del pool Front End) dall'interfaccia interna del server perimetrale</p></td>
</tr>
<tr class="odd">
<td><p>SIP/MTLS/TCP/5062</p></td>
<td><p>Qualsiasi (può essere definito come indirizzo IP del Front End Server, indirizzo IP del pool Front End o qualsiasi Survivable Branch Appliance o Survivable Branch Server che utilizza questo server perimetrale)</p></td>
<td><p>Interfaccia VIP interna di server perimetrale</p></td>
<td><p>Autenticazione degli utenti A/V (servizio di autenticazione A/V) dal Front End Server o dall'indirizzo IP del pool Front End oppure da qualsiasi Survivable Branch Appliance o Survivable Branch Server che utilizza questo server perimetrale</p></td>
</tr>
<tr class="even">
<td><p>STUN/MSTURN/UDP/3478</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Interfaccia VIP interna di server perimetrale</p></td>
<td><p>Percorso preferito per trasferimenti multimediali A/V tra utenti interni ed esterni</p></td>
</tr>
<tr class="odd">
<td><p>STUN/MSTURN/TCP/443</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Interfaccia VIP interna di server perimetrale</p></td>
<td><p>Percorso di fallback per trasferimenti multimediali A/V tra utenti interni ed esterni se non è possibile stabilire la comunicazione UDP, TCP è usato per il trasferimento di file e la condivisione del desktop</p></td>
</tr>
<tr class="even">
<td><p>STUN/MSTURN/TCP/443</p></td>
<td><p>Interfaccia VIP interna di server perimetrale</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Percorso di fallback per trasferimenti multimediali A/V tra utenti interni ed esterni se non è possibile stabilire la comunicazione UDP, TCP è usato per il trasferimento di file e la condivisione del desktop</p></td>
</tr>
</tbody>
</table>

