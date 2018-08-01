---
title: 'Lync Server 2013: Riepilogo di DNS - topologia perimetrale consolidata con scalabilità implementata, bilanciamento del carico DNS con indirizzi IP privati tramite NAT'
TOCTitle: Riepilogo di DNS - topologia perimetrale consolidata con scalabilità implementata, bilanciamento del carico DNS con indirizzi IP privati tramite NAT
ms:assetid: 11bc7b84-91cf-48f9-ad0e-06ad30b46a2e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398201(v=OCS.15)
ms:contentKeyID: 49299731
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo di DNS - topologia perimetrale consolidata con scalabilità implementata, bilanciamento del carico DNS con indirizzi IP privati tramite NAT in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

I requisiti di record DNS per l'accesso remoto a Lync Server 2013 sono piuttosto semplici rispetto a quelli per i certificati e le porte. Molti record inoltre sono facoltativi, a seconda della configurazione dei client che eseguono Lync 2013 e dell'eventuale abilitazione della federazione.

Per i dettagli sui requisiti DNS di Lync 2013, vedere [Determinare i requisiti di DNS per Lync Server 2013](lync-server-2013-determine-dns-requirements.md).

Per informazioni dettagliate sulla configurazione automatica dei client Lync 2013 quando non è configurato DNS split brain, vedere la sezione relativa alla configurazione automatica senza DNS split brain in [Determinare i requisiti di DNS per Lync Server 2013](lync-server-2013-determine-dns-requirements.md).

Nella tabella seguente viene fornito un riepilogo dei record DNS necessari per supportare la topologia perimetrale consolidata singola illustrata nella relativa figura. Si noti che alcuni record DNS sono necessari solo per la configurazione automatica dei client Lync 2013. Se si intende utilizzare oggetti Criteri di gruppo per configurare i client Lync, i record associati non saranno necessari.

## IMPORTANTE: requisiti delle schede di rete del server perimetrale

Per evitare problemi di routing, verificare che siano presenti almeno due schede di rete nei server perimetrali e che il gateway predefinito sia impostato solo nella scheda di rete associata all'interfaccia esterna. Come illustrato nella figura relativa allo scenario di server perimetrali consolidati con scalabilità implementata in [Topologia perimetrale consolidata con scalabilità implementata, bilanciamento del carico DNS con indirizzi IP privati tramite NAT in Lync Server 2013](lync-server-2013-scaled-consolidated-edge-dns-load-balancing-with-private-ip-addresses-using-nat.md), ad esempio, il gateway predefinito punterà al firewall esterno.

È possibile configurare due schede di rete in ogni server perimetrale, come illustrato di seguito:

  - **Scheda di rete 1 - Nodo 1 (interfaccia interna)**
    
    Interfaccia interna con indirizzo 172.25.33.10 assegnato.
    
    Nessun gateway predefinito definito.
    
    Verificare che esista una route dalla rete in cui si trova l'interfaccia interna del server perimetrale alle reti in cui sono presenti server che eseguono Lync Server 2013 o Lync Server 2013 (ad esempio, da 172.25.33.0 a 192.168.10.0).

  - **Scheda di rete 1 - Nodo 2 (interfaccia interna)**
    
    Interfaccia interna con indirizzo 172.25.33.11 assegnato.
    
    Nessun gateway predefinito definito.
    
    Verificare che esista una route dalla rete in cui si trova l'interfaccia interna del server perimetrale alle reti in cui sono presenti server che eseguono Lync Server 2013 o Lync Server 2013 (ad esempio, da 172.25.33.0 a 192.168.10.0).

  - **Scheda di rete 2 - Nodo 1 (interfaccia esterna)**
    
    A questa scheda di rete sono assegnati tre indirizzi IP privati, ad esempio 10.45.16.10 per Access Edge, 10.45.16.20 per Web Conferencing Edge e 10.45.16.30 per A/V Edge.
    

    > [!NOTE]
    > È possibile, ma non consigliabile, utilizzare un solo indirizzo IP per tutte e tre le interfacce dei servizi Edge. Sebbene questa scelta consenta di risparmiare indirizzi IP, richiede numeri di porta diversi per ogni servizio. Il numero di porta predefinito è 443/TCP e garantisce che la maggior parte dei firewall remoti consenta il traffico. L'impostazione dei valori di porta ad esempio su 5061/TCP per Access Edge, 444/TCP per Web Conferencing Edge e 443/TCP per AV Edge può causare problemi per gli utenti remoti se un firewall da cui sono protetti non consente il traffico su 5061/TCP e 444/TCP. L'utilizzo di tre indirizzi IP distinti inoltre facilita la risoluzione dei problemi perché i dati possono essere filtrati in base all'indirizzo IP.

    
    L'indirizzo IP pubblico di Access Edge è primario, con gateway predefinito impostato sul router integrato (10.45.16.1).
    
    Gli indirizzi IP privati di Web Conferencing Edge e A/V Edge sono indirizzi IP aggiuntivi nella sezione **Avanzate** delle proprietà di **Protocollo Internet versione 4 (TCP/IPv4)** e **Protocollo Internet versione 6 (TCP/IPv6)** delle proprietà di **Connessione alla rete locale (LAN)** in Windows Server.

  - **Scheda di rete 2 - Nodo 2 (interfaccia esterna)**
    
    A questa scheda di rete sono assegnati tre indirizzi IP privati, ad esempio 10.45.16.11 per Access Edge, 10.45.16.21 per Web Conferencing Edge e 10.45.16.31 per A/V Edge.
    
    L'indirizzo IP pubblico di Access Edge è primario, con gateway predefinito impostato sul router integrato (10.45.16.1).
    
    Gli indirizzi IP privati di Web Conferencing Edge e A/V Edge sono indirizzi IP aggiuntivi nella sezione **Avanzate** delle proprietà di **Protocollo Internet versione 4 (TCP/IPv4)** e **Protocollo Internet versione 6 (TCP/IPv6)** delle proprietà di **Connessione alla rete locale (LAN)** in Windows Server.

> [!tip]  
> La configurazione del server perimetrale con due schede di rete è un'opzione. L'altra consiste nell'utilizzare una scheda di rete per l'interfaccia interna e tre schede di rete per l'interfaccia esterna del server perimetrale. Il vantaggio principale di questa opzione è l'utilizzo di una scheda di rete separata ogni servizio di server perimetrale e la raccolta di dati potenzialmente più concisi per eventuali attività di risoluzione dei problemi.

### Record DNS necessari per server perimetrale consolidato in scala, servizio di bilanciamento del carico DNS con indirizzi IP privati tramite NAT (esempio)

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Posizione/TIPO/Porta</th>
<th>FQDN/Record DNS</th>
<th>Indirizzo IP/FQDN</th>
<th>Corrisponde a/Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DNS/A esterno</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>131.107.155.10 e 131.107.155.11</p></td>
<td><p>Interfaccia esterna Access Edge (Contoso). Ripetere secondo le necessità per tutti i domini SIP con utenti abilitati per Lync.</p></td>
</tr>
<tr class="even">
<td><p>DNS/A esterno</p></td>
<td><p>webcon.contoso.com</p></td>
<td><p>131.107.155.20 e 131.107.155.21</p></td>
<td><p>Interfaccia esterna Web Conferencing Edge Server</p></td>
</tr>
<tr class="odd">
<td><p>DNS/A esterno</p></td>
<td><p>av.contoso.com</p></td>
<td><p>131.107.155.30 e 131.107.155.31</p></td>
<td><p>Interfaccia esterna A/V Edge Server</p></td>
</tr>
<tr class="even">
<td><p>DNS esterno/SRV/443</p></td>
<td><p>_sip._tls.contoso.com</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>Interfaccia esterna Access Edge. Necessario per la configurazione automatica dei client Lync 2013 e Lync 2010 per il funzionamento esterno. Ripetere secondo le necessità per tutti i domini SIP con utenti abilitati per Lync.</p></td>
</tr>
<tr class="odd">
<td><p>DNS esterno/SRV/5061</p></td>
<td><p>_sipfederationtls._tcp.contoso.com</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>Interfaccia esterna Access Edge SIP. Necessario per l'individuazione DNS automatica di partner federati, nota come dominio SIP consentito, nonché come federazione avanzata nelle versioni precedenti. Ripetere per tutti i domini SIP con utenti abilitati per Lync, se necessario.</p></td>
</tr>
<tr class="even">
<td><p>DNS interno/A</p></td>
<td><p>lsedge.contoso.net</p></td>
<td><p>172.25.33.10 e 172.25.33.11</p></td>
<td><p>Interfaccia interna del server perimetrale consolidato.</p></td>
</tr>
</tbody>
</table>


## Record necessari per la federazione


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Posizione/TIPO/Porta</th>
<th>FQDN</th>
<th>Indirizzo IP/Record host FQDN</th>
<th>Corrisponde a/Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DNS esterno/SRV/5061</p></td>
<td><p>_sipfederationtls._tcp.contoso.com</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>Interfaccia esterna Access Edge SIP. Necessario per l'individuazione DNS automatica della federazione con altri potenziali partner, condizione nota come &quot;domini SIP consentiti&quot;, nonché come federazione avanzata nelle versioni precedenti. Ripetere secondo le necessità per tutti i domini SIP con utenti abilitati per Lync.</p>

> [!IMPORTANT]  
> Questo record SRV è necessario per il fornitore di servizi di accesso a terze parti per notifiche Push e dispositivi mobili.

</td>
</tr>
</tbody>
</table>


## Riepilogo DNS - Connettività per messaggistica istantanea pubblica


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Posizione/TIPO/Porta</th>
<th>FQDN/Record DNS</th>
<th>Indirizzo IP/FQDN</th>
<th>Corrisponde a/Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DNS/A esterno</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>Interfaccia del servizio Access Edge</p></td>
<td><p>Interfaccia esterna Access Edge (Contoso). Ripetere secondo le necessità per tutti i domini SIP con utenti abilitati per Lync.</p></td>
</tr>
</tbody>
</table>


## Riepilogo DNS per il protocollo XMPP


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Posizione/TIPO/Porta</th>
<th>FQDN</th>
<th>Indirizzo IP/Record host FQDN</th>
<th>Corrisponde a/Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DNS esterno/SRV/5269</p></td>
<td><p>_xmpp-server._tcp.contoso.com</p></td>
<td><p>xmpp.contoso.com</p></td>
<td><p>Interfaccia esterna del proxy XMPP nel servizio Access Edge o nel pool di server perimetrali. Ripetere secondo le necessità per tutti i domini SIP interni con utenti abilitati per Lync in cui il contatto con i contatti XMPP è consentito mediante la configurazione dei criteri di accesso esterno tramite criteri globali, criteri del sito in cui si trova l'utente o criteri utente applicati all'utente abilitato per Lync. Nei criteri Partner federati XMPP deve inoltre essere configurato un dominio XMPP consentito. Per ulteriori informazioni, vedere gli argomenti nella sezione <strong>Vedere anche</strong>.</p></td>
</tr>
<tr class="even">
<td><p>DNS/A esterno</p></td>
<td><p>xmpp.contoso.com (esempio)</p></td>
<td><p>Indirizzo IP del servizio Access Edge nel server perimetrale o nel pool di server perimetrali che ospita il proxy XMPP</p></td>
<td><p>Punta al servizio Access Edge o al pool di server perimetrali che ospita il servizio proxy XMPP. Il record SRV creato punterà a questo record host (A o AAAA).</p></td>
</tr>
</tbody>
</table>

