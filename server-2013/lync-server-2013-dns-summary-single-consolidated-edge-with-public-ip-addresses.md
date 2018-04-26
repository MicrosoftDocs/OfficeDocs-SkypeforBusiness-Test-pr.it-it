---
title: 'Lync Server 2013: Riepilogo di DNS - singola topologia perimetrale consolidata con indirizzi IP pubblici'
TOCTitle: Riepilogo di DNS - singola topologia perimetrale consolidata con indirizzi IP pubblici
ms:assetid: 7b83eae4-aa1a-4cc6-8077-42176d56cab5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205025(v=OCS.15)
ms:contentKeyID: 49301088
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo di DNS - singola topologia perimetrale consolidata con indirizzi IP pubblici in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

I requisiti di record DNS per l'accesso remoto a Lync Server 2013 sono piuttosto semplici rispetto a quelli per i certificati e le porte. Molti record inoltre sono facoltativi, a seconda della configurazione dei client che eseguono Lync 2013 e dell'eventuale abilitazione della federazione.

Per i dettagli sui requisiti DNS di Lync 2013, vedere [Determinare i requisiti di DNS per Lync Server 2013](lync-server-2013-determine-dns-requirements.md).

Per informazioni dettagliate sulla configurazione automatica dei client che eseguono Lync 2013 nel caso in cui manchi una configurazione DNS di tipo split brain, vedere "Configurazione automatica senza DNS di tipo split brain" in [Determinare i requisiti di DNS per Lync Server 2013](lync-server-2013-determine-dns-requirements.md).

Nella tabella seguente viene presentato un riepilogo dei record DNS necessari per supportare la topologia perimetrale consolidata singola illustrata nella figura corrispondente. Si noti che alcuni record DNS sono necessari solo per la configurazione automatica dei client Lync 2013 e Lync 2010. Se si intende configurare i client Lync utilizzando oggetti Criteri di gruppo, i record di configurazione automatica associati non sono necessari.

## IMPORTANTE: requisiti delle schede di rete del server perimetrale

Per evitare problemi di routing, verificare che nel server server perimetrali siano presenti almeno due schede di rete e che il gateway predefinito sia impostato solo nella scheda di rete associata all'interfaccia esterna. Ad esempio, come illustrato nella figura Topologia perimetrale singola con indirizzi IP pubblici in [Singola topologia perimetrale consolidata con indirizzi IP pubblici in Lync Server 2013](lync-server-2013-single-consolidated-edge-with-public-ip-addresses.md), il gateway predefinito deve fare riferimento al router esterno del perimetro Internet o al firewall che fornisce indirizzi IP pubblici. La relazione di rete per le interfacce di server perimetrale è una relazione di routing, e non una relazione NAT.

È possibile configurare due schede di rete all'interno del server perimetrale come segue:

  - **Scheda di rete 1 (interfaccia interna)**
    
    Interfaccia interna con indirizzo 172.25.33.10 assegnato.
    
    Nessun gateway predefinito definito.
    
    Verificare che esista una route dalla rete in cui si trova l'interfaccia interna del server perimetrale alle reti in cui sono presenti server che eseguono Lync Server 2013 o Lync Server 2013 (ad esempio, da 172.25.33.0 a 192.168.10.0).

  - **Scheda di rete 2 (interfaccia esterna)**
    
    A questa scheda di rete sono assegnati tre indirizzi IP pubblici, ad esempio 131.107.155.10 per Access Edge, 131.107.155.20 per Web Conferencing Edge, 131.107.155.30 per AV Edge.
    

    > [!NOTE]
    > È possibile, ma non consigliabile, utilizzare un solo indirizzo IP per tutte e tre le interfacce dei servizi Edge. Sebbene questa scelta consenta di risparmiare indirizzi IP, richiede numeri di porta diversi per ogni servizio. Il numero di porta predefinito è 443/TCP e garantisce che la maggior parte dei firewall remoti consenta il traffico. L'impostazione dei valori di porta ad esempio su 5061/TCP per Access Edge, 444/TCP per Web Conferencing Edge e 443/TCP per AV Edge può causare problemi per gli utenti remoti se un firewall da cui sono protetti non consente il traffico su 5061/TCP e 444/TCP. L'utilizzo di tre indirizzi IP distinti inoltre facilita la risoluzione dei problemi perché i dati possono essere filtrati in base all'indirizzo IP.

    
    L'indirizzo IP pubblico di Access Edge è quello primario, con il gateway predefinito impostato sul router pubblico (131.107.155.1).
    
    Gli indirizzi IP pubblici di Web conferencing e A/V Edge sono indirizzi IP aggiuntivi nella sezione **Avanzate** delle proprietà di **Internet Protocol Version 4 (TCP/IPv4)** e **Internet Protocol Version 6 (TCP/IPv6)** delle **Proprietà LAN** in Windows Server.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>La configurazione del server perimetrale con due schede di rete è un'opzione. L'altra consiste nell'utilizzare una scheda di rete per l'interfaccia interna e tre schede di rete per l'interfaccia esterna del server perimetrale. Il vantaggio principale di questa opzione è l'utilizzo di una scheda di rete separata ogni servizio di server perimetrale e la raccolta di dati potenzialmente più concisi per eventuali attività di risoluzione dei problemi.</td>
</tr>
</tbody>
</table>


### Record DNS necessari per la topologia perimetrale singola con indirizzi IP pubblici (esempio)

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
<td><p>131.107.155.10</p></td>
<td><p>Interfaccia esterna Access Edge (Contoso). Ripetere secondo le necessità per tutti i domini SIP con utenti abilitati per Lync.</p></td>
</tr>
<tr class="even">
<td><p>DNS/A esterno</p></td>
<td><p>webcon.contoso.com</p></td>
<td><p>131.107.155.20</p></td>
<td><p>Interfaccia esterna Web Conferencing Edge Server</p></td>
</tr>
<tr class="odd">
<td><p>DNS/A esterno</p></td>
<td><p>av.contoso.com</p></td>
<td><p>131.107.155.30</p></td>
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
<td><p>Interfaccia esterna Access Edge SIP. Necessario per l'individuazione DNS automatica di partner federati, condizione nota come &quot;dominio SIP consentito&quot;, nonché come federazione avanzata nelle versioni precedenti. Ripetere secondo le necessità per tutti i domini SIP con utenti abilitati per Lync.</p></td>
</tr>
<tr class="even">
<td><p>DNS interno/A</p></td>
<td><p>lsedge.contoso.net</p></td>
<td><p>172.25.33.10</p></td>
<td><p>Interfaccia interna del server perimetrale consolidato.</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>I record elencati nella tabella precedente sono visualizzati con estensione <em>net</em> o <em>com</em>, per evidenziare la zona in cui devono trovarsi se non si utilizza il DNS di tipo split brain. Se si utilizza il DNS di tipo split brain, tutti i record devono trovarsi nella stessa zona, con l'unica distinzione tra versione interna ed esterna. Per informazioni dettagliate, vedere “DNS di tipo split brain” in <a href="lync-server-2013-determine-dns-requirements.md">Determinare i requisiti di DNS per Lync Server 2013</a>.</td>
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
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Questo record SRV è necessario per il fornitore di servizi di accesso a terze parti per notifiche Push e dispositivi mobili.</td>
</tr>
</tbody>
</table>

</div></td>
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

