---
title: "Lync Server 2013: DNS: topol. perim. consolid. c/ scalab. impl. e bilanc. carico hw"
TOCTitle: Riepilogo di DNS - topologia perimetrale consolidata con scalabilità implementata e servizi di bilanciamento del carico hardware
ms:assetid: 8453297c-da1d-4b9e-a37e-6721458c6feb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398670(v=OCS.15)
ms:contentKeyID: 49301185
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo di DNS - topologia perimetrale consolidata con scalabilità implementata e servizi di bilanciamento del carico hardware in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

I requisiti di record DNS per l'accesso remoto a Lync Server 2013 sono piuttosto semplici rispetto a quelli per i certificati e le porte. Molti record inoltre sono facoltativi, a seconda della configurazione dei client che eseguono Lync 2013 e dell'eventuale abilitazione della federazione.

Per i dettagli sui requisiti DNS di Lync 2013, vedere [Determinare i requisiti di DNS per Lync Server 2013](lync-server-2013-determine-dns-requirements.md).

Per informazioni dettagliate sulla configurazione automatica dei client Lync 2013 quando non è configurato DNS split brain, vedere la sezione relativa alla configurazione automatica senza DNS split brain in [Determinare i requisiti di DNS per Lync Server 2013](lync-server-2013-determine-dns-requirements.md).

Nella tabella seguente è incluso un riepilogo dei record DNS necessari per supportare la topologia perimetrale consolidata con scalabilità implementata (bilanciamento del carico hardware) illustrata in Reference Architecture 3: Scaled Consolidated Edge (Hardware Load Balanced). Si noti che determinati record DNS sono necessari solo per la configurazione automatica per i client Lync. Se si prevede di utilizzare oggetti Criteri di gruppo per configurare i client Lync, i record associati non sono necessari.

## IMPORTANTE: requisiti delle schede di rete del server perimetrale

Per evitare problemi di routing, verificare che siano presenti almeno due schede di rete nei server perimetrali e che il gateway predefinito sia impostato solo nella scheda di rete associata all'interfaccia esterna. Come illustrato nella figura relativa allo scenario di server perimetrali consolidati con scalabilità implementata in [Topologia perimetrale consolidata con scalabilità implementata e servizi di bilanciamento del carico hardware in Lync Server 2013](lync-server-2013-scaled-consolidated-edge-with-hardware-load-balancers.md), ad esempio, il gateway predefinito punterà al firewall esterno.

È possibile configurare due schede di rete in ogni server perimetrali, come illustrato di seguito:

  - **Scheda di rete 1 (interfaccia interna)**
    
    Interfaccia interna con indirizzo 172.25.33.10 assegnato.
    
    Nessun gateway predefinito.
    
    Verificare che sia presente una route dalla rete che contiene l'interfaccia interna del server perimetrale a qualsiasi rete che contiene client o server Lync Server che eseguono Lync Server (ad esempio, da 172.25.33.0 a 192.168.10.0).

  - **Scheda di rete 2 (interfaccia esterna)**
    
    A questa scheda di rete sono assegnati tre indirizzi IP pubblici, ad esempio 131.107.155.10 per servizio Access Edge, 131.107.155.20 per servizio Web Conferencing Edge, 131.107.155.30 per servizio A/V Edge.
    

    > [!NOTE]
    > Gli indirizzi IP assegnati alle interfacce di rete esterne effettive del server perimetrale potrebbero dipendere dal servizio di bilanciamento del carico hardware scelto. Per informazioni sui requisiti effettivi a livello di indirizzi IP, fare riferimento alla documentazione del servizio di bilanciamento del carico hardware.<BR>È possibile, anche se non consigliabile, utilizzare un singolo indirizzo IP per tutte e tre le interfacce dei servizi perimetrali. Benché in questo modo sia possibile utilizzare meno indirizzi IP, vengono richiesti numeri di porte diversi per ogni servizio. Il numero di porta predefinito è 443/TCP, che garantisce il passaggio del traffico attraverso i firewall più remoti. Modificando i valori delle porte e impostandoli ad esempio su 5061/TCP per il servizio Access Edge, su 444/TCP per il servizio Web Conferencing Edge e su 443/TCP per il servizio A/V Edge, possono verificarsi problemi per gli utenti remoti protetti da un firewall che non consente il traffico sulle porte 5061/TCP e 444/TCP. L'utilizzo di tre indirizzi IP distinti inoltre semplifica la risoluzione dei problemi poiché consente di applicare un filtro in base all'indirizzo IP.

    
    L'indirizzo IP di servizio Access Edge è quello primario, con il gateway predefinito impostato sul router integrato (131.107.155.1).
    
    Gli indirizzi IP di servizio Web Conferencing Edge e servizio A/V Edge sono secondari.

> [!TIP]  
> La configurazione del server perimetrale con due schede di rete è un'opzione. L'altra consiste nell'utilizzare una scheda di rete per l'interfaccia interna e tre schede di rete per l'interfaccia esterna del server perimetrale. Il vantaggio principale di questa opzione è l'utilizzo di una scheda di rete separata ogni servizio di server perimetrale e la raccolta di dati potenzialmente più concisi per eventuali attività di risoluzione dei problemi.

### Record DNS necessari per la topologia perimetrale consolidata e bilanciamento del carico hardware (esempio)

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
<td><p>Interfaccia esterna di servizio Access Edge (Contoso). Ripetere secondo necessità per tutti i domini SIP con utenti abilitati per Lync</p></td>
</tr>
<tr class="even">
<td><p>DNS/A esterno</p></td>
<td><p>webcon.contoso.com</p></td>
<td><p>131.107.155.20</p></td>
<td><p>Interfaccia esterna del servizio Web Conferencing Edge.</p></td>
</tr>
<tr class="odd">
<td><p>DNS/A esterno</p></td>
<td><p>av.contoso.com</p></td>
<td><p>131.107.155.30</p></td>
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
<td><p>Interfaccia esterna SIP di servizio Access Edge Necessario per l'individuazione DNS automatica di partner federati, nota come dominio SIP consentito, nonché come federazione avanzata nelle versioni precedenti. Ripetere secondo necessità per tutti i domini SIP con utenti abilitati per client Lync e Microsoft Lync Mobile che utilizzano servizio notifica Push o servizio notifica Push Apple</p></td>
</tr>
<tr class="even">
<td><p>DNS interno/A</p></td>
<td><p>lsedge.contoso.net</p></td>
<td><p>172.25.33.10</p></td>
<td><p>Interfaccia interna del server perimetrale consolidato.</p></td>
</tr>
</tbody>
</table>

