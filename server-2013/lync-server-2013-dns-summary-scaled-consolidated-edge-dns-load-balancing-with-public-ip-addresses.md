---
title: "Lync Server 2013: DNS - topolog. perimet. consolid. c/ scalab. implem., bilanciam. carico DNS c/ indir. IP pubblici"
TOCTitle: Riepilogo di DNS - topologia perimetrale consolidata con scalabilità implementata, bilanciamento del carico DNS con indirizzi IP pubblici
ms:assetid: dc8f096a-a0a4-4f71-8930-88ff8fc089d9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205319(v=OCS.15)
ms:contentKeyID: 49302204
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo di DNS - topologia perimetrale consolidata con scalabilità implementata, bilanciamento del carico DNS con indirizzi IP pubblici in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

I requisiti di record DNS per l'accesso remoto a Lync Server 2013 sono piuttosto semplici rispetto a quelli per i certificati e le porte. Molti record inoltre sono facoltativi, a seconda della configurazione dei client che eseguono Lync 2013 e dell'eventuale abilitazione della federazione.

Per i dettagli sui requisiti DNS di Lync 2013, vedere [Determinare i requisiti di DNS per Lync Server 2013](lync-server-2013-determine-dns-requirements.md).

Per informazioni dettagliate sulla configurazione automatica dei client Lync 2013 quando non è configurato DNS split brain, vedere la sezione relativa alla configurazione automatica senza DNS split brain in [Determinare i requisiti di DNS per Lync Server 2013](lync-server-2013-determine-dns-requirements.md).

Nella tabella seguente viene fornito un riepilogo dei record DNS necessari per supportare la topologia perimetrale consolidata singola illustrata nella relativa figura. Si noti che alcuni record DNS sono necessari solo per la configurazione automatica dei client Lync 2013. Se si intende utilizzare oggetti Criteri di gruppo per configurare i client Lync, i record associati non saranno necessari.

## IMPORTANTE: requisiti delle schede di rete del server perimetrale

Per evitare problemi di routing, verificare che siano presenti almeno due schede di rete nei server perimetrali e che il gateway predefinito sia impostato solo nella scheda di rete associata all'interfaccia esterna. Come illustrato nella figura relativa allo scenario di server perimetrali consolidati con scalabilità implementata in [Topologia perimetrale consolidata con scalabilità implementata, bilanciamento del carico DNS con indirizzi IP pubblici in Lync Server 2013](lync-server-2013-scaled-consolidated-edge-dns-load-balancing-with-public-ip-addresses.md), il gateway predefinito ad esempio punterà al firewall esterno.

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
    
    Sono assegnati tre indirizzi IP privati a questa scheda di rete, ad esempio 131.107.155.10 per il servizio Access Edge, 131.107.155.20 per il servizio Web Conferencing Edge e 131.107.155.30 per il servizio A/V Edge.
    
    L'indirizzo IP pubblico del servizio Access Edge è quello primario con il gateway predefinito impostato sul router pubblico (131.107.155.1).
    
    Gli Indirizzi IP privati del servizio Web Conferencing Edge e del servizio A/V Edge sono indirizzi IP aggiuntivi nella sezione **Avanzate** delle proprietà **Protocollo Internet versione 4 (TCP/IPv4)** e **Protocollo Internet versione 6 (TCP/IPv6)** di **Proprietà connessione alla rete locale (LAN)** in Windows Server.
    

    > [!NOTE]
    > È possibile, anche se non consigliabile, utilizzare un singolo indirizzo IP per tutte e tre le interfacce dei servizi perimetrali. Benché in questo modo sia possibile utilizzare meno indirizzi IP, vengono richiesti numeri di porte diversi per ogni servizio. Il numero di porta predefinito è 443/TCP, che garantisce il passaggio del traffico attraverso i firewall più remoti. Modificando i valori delle porte e impostandoli ad esempio su 5061/TCP per il servizio Access Edge, su 444/TCP per il servizio Web Conferencing Edge e su 443/TCP per il servizio A/V Edge, possono verificarsi problemi per gli utenti remoti protetti da un firewall che non consente il traffico sulle porte 5061/TCP e 444/TCP. L'utilizzo di tre indirizzi IP distinti inoltre semplifica la risoluzione dei problemi poiché consente di applicare un filtro in base all'indirizzo IP.



  - **Scheda di rete 2 - Nodo 2 (interfaccia esterna)**
    
    Sono assegnati tre indirizzi IP privati a questa scheda di rete, ad esempio 131.107.155.11 per il servizio Access Edge, 131.107.155.21 per il servizio Web Conferencing Edge e 131.107.155.31 per il servizio A/V Edge.
    
    L'indirizzo IP pubblico del servizio Access Edge è quello primario con il gateway predefinito impostato sul router pubblico (131.107.155.1).
    
    Gli Indirizzi IP privati del servizio Web Conferencing Edge e del servizio A/V Edge sono indirizzi IP aggiuntivi nella sezione **Avanzate** delle proprietà **Protocollo Internet versione 4 (TCP/IPv4)** e **Protocollo Internet versione 6 (TCP/IPv6)** di **Proprietà connessione alla rete locale (LAN)** in Windows Server.

> [!TIP]  
> La configurazione del server perimetrale con due schede di rete è un'opzione. L'altra consiste nell'utilizzare una scheda di rete per l'interfaccia interna e tre schede di rete per l'interfaccia esterna del server perimetrale. Il vantaggio principale di questa opzione è l'utilizzo di una scheda di rete separata ogni servizio di server perimetrale e la raccolta di dati potenzialmente più concisi per eventuali attività di risoluzione dei problemi.

### Record DNS necessari per topologia perimetrale consolidata con scalabilità implementata e bilanciamento del carico DNS con indirizzi IP pubblici (esempio)

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
<td><p>Interfaccia esterna del servizio Access Edge (Contoso). Ripetere in base alle esigenze per tutti i domini SIP con utenti abilitati per Lync.</p></td>
</tr>
<tr class="even">
<td><p>DNS/A esterno</p></td>
<td><p>webcon.contoso.com</p></td>
<td><p>131.107.155.20 e 131.107.155.21</p></td>
<td><p>Interfaccia esterna del servizio Web Conferencing Edge.</p></td>
</tr>
<tr class="odd">
<td><p>DNS/A esterno</p></td>
<td><p>av.contoso.com</p></td>
<td><p>131.107.155.30 e 131.107.155.31</p></td>
<td><p>Interfaccia esterna del servizio A/V Edge.</p></td>
</tr>
<tr class="even">
<td><p>DNS esterno/SRV/443</p></td>
<td><p>_sip._tls.contoso.com</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>Interfaccia esterna del servizio Access Edge. Necessario per la configurazione automatica dei client Lync 2013 e Lync 2010 per il funzionamento esterno. Ripetere in base alle esigenze per tutti i domini SIP con utenti abilitati per Lync.</p></td>
</tr>
<tr class="odd">
<td><p>DNS esterno/SRV/5061</p></td>
<td><p>_sipfederationtls._tcp.contoso.com</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>Interfaccia esterna del servizio Access Edge. Necessario per l'individuazione DNS automatica dei partner federati. Nota come &quot;dominio SIP consentito&quot;, nonché come federazione avanzata nelle versioni precedenti. Ripetere in base alle esigenze per tutti i domini SIP con utenti abilitati per Lync.</p></td>
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
<td><p>Interfaccia esterna del servizio Access Edge SIP. Necessario per l'individuazione DNS automatica della federazione con altri potenziali partner della federazione. Nota come &quot;dominio SIP consentito&quot;, nonché come federazione avanzata nelle versioni precedenti.</p>

> [!IMPORTANT]  
> Ripetere in base alle esigenze per tutti i domini SIP con utenti abilitati per Lync e per i client Microsoft Lync Mobile che utilizzano il servizio notifica Push o il servizio notifica Push Apple.

</td></tr>
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
<td><p>Interfaccia esterna del servizio Access Edge (Contoso). Ripetere in base alle esigenze per tutti i domini SIP con utenti abilitati per Lync.</p></td>
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
<td><p>Interfaccia esterna XMPP nel servizio Access Edge o nel pool di server perimetrali. Ripetere in base alle esigenze per tutti i domini SIP interni con utenti abilitati per Lync in cui è consentito il contatto con utenti XMPP mediante la configurazione di Criteri di accesso esterno tramite criteri globali, criteri sito in cui è incluso l'utente o criteri utente applicati all'utente abilitato per Lync. È inoltre necessario configurare un dominio XMPP consentito nei criteri Partner federati XMPP. Per ulteriori informazioni, vedere gli argomenti elencati nella sezione <strong>Vedere anche</strong>.</p></td>
</tr>
<tr class="even">
<td><p>DNS/A esterno</p></td>
<td><p>xmpp.contoso.com (esempio)</p></td>
<td><p>Indirizzo IP del servizio Access Edge nel server perimetrale o nel pool di server perimetrali che ospita il proxy XMPP</p></td>
<td><p>Punta al servizio Access Edge o al pool di server perimetrali che ospita il servizio proxy XMPP. Il record SRV creato punterà a questo record host (A o AAAA).</p></td>
</tr>
</tbody>
</table>

