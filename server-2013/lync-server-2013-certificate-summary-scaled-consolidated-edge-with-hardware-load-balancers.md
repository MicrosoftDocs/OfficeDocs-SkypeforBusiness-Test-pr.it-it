---
title: 'Lync Server 2013: Riepilogo dei certificati - topologia perimetrale consolidata con scalabilità implementata e servizi di bilanciamento del carico hardware'
TOCTitle: Riepilogo dei certificati - topologia perimetrale consolidata con scalabilità implementata e servizi di bilanciamento del carico hardware
ms:assetid: 894a9f3e-7cba-4915-8fdf-e52f2f25126f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398692(v=OCS.15)
ms:contentKeyID: 49301233
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo dei certificati - topologia perimetrale consolidata con scalabilità implementata e servizi di bilanciamento del carico hardware in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Microsoft Lync Server 2013 utilizza i certificati per l'autenticazione reciproca con altri server e per crittografare i dati da server a server e da server a client. Per i certificati è richiesta la corrispondenza tra i nomi dei record DNS (Domain Name System) associati ai server e il nome soggetto (SN) e il nome alternativo soggetto (SAN) nel certificato. Per il mapping corretto di server, record DNS e voci di certificato, è necessario pianificare con attenzione i nomi di dominio completo (FQDN) previsti per i server, registrati in DNS e le voci SN e SAN nel certificato.

Il certificato assegnato alle interfacce esterne del server perimetrale è richiesto da un'Autorità di certificazione (CA) pubblica. Le CA pubbliche che si sono dimostrate efficienti per la fornitura di certificati per gli scopi di Unified Communications sono elencate nell'articolo seguente: [http://go.microsoft.com/fwlink/p/?linkid=3052\&kbid=929395](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=929395). Quando si richiede il certificato è possibile utilizzare la richiesta generata da Distribuzione guidata di Lync Server oppure creare la richiesta manualmente o tramite la procedura comunicata dalla CA pubblica. In fase di assegnazione, il certificato viene assegnato all'interfaccia del servizio Access Edge, all'interfaccia del servizio Web Conferencing Edge e al servizio di autenticazione audio/video. Questo servizio non deve essere confuso con il servizio A/V Edge che non utilizza un certificato per crittografare i flussi audio e video. L'interfaccia interna del server perimetrale può utilizzare un certificato da una CA interna (dell'organizzazione) o un certificato da una CA pubblica. Il certificato dell'interfaccia interna utilizza solo il nome soggetto e non richiede o utilizza voci SAN.


> [!NOTE]
> Nella tabella seguente viene illustrata una seconda voce SIP (sip.fabrikam.com) nell'elenco dei nomi alternativi soggetto come riferimento. Per ogni dominio SIP presente nell'organizzazione, è necessario che nell'elenco dei nomi alternativi soggetto dei certificati sia incluso un FQDN corrispondente.



## Certificati necessari per Server perimetrale consolidato in scala con bilanciamento del carico hardware


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente</th>
<th>Nome soggetto</th>
<th>Ordine/nomi alternativi soggetto (SAN)</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>server perimetrale consolidato singolo (perimetro esterno)</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>webcon.contoso.com</p>
<p>sip.contoso.com</p>
<p>sip.fabrikam.com</p></td>
<td><p>Il certificato deve provenire da una CA pubblica e includere l'EKU server e l'EKU client se è necessario distribuire la connettività per la messaggistica istantanea pubblica con AOL. Per i server perimetrali con scalabilità implementata, inoltre, la chiave privata del certificato deve essere esportabile ed è necessario copiare il certificato e la chiave privata in ogni server perimetrale. Il certificato viene assegnato alle interfacce perimetrali esterne per:</p>
<ul>
<li><p>servizio Access Edge</p></li>
<li><p>servizio Web Conferencing Edge</p></li>
<li><p>servizio A/V Edge</p></li>
</ul>
<p>I nomi SAN vengono aggiunti automaticamente al certificato in base alle definizioni nel generatore di topologie. È possibile aggiungere voci relative ai nomi SAN in base alle esigenze per ulteriori domini SIP e altre voci che è necessario supportare. Il nome soggetto viene replicato nel nome SAN e deve essere presente per garantire il corretto funzionamento.</p></td>
</tr>
<tr class="even">
<td><p>server perimetrale consolidato singolo (perimetro interno)</p></td>
<td><p>lsedge.contoso.net</p></td>
<td><p>Nessun nome alternativo soggetto necessario</p></td>
<td><p>I certificati possono essere emessi da autorità di certificazione pubbliche o private, e devono contenere l'utilizzo chiavi avanzato (EKU) del server. Il certificato è assegnato alle interfacce interne del server perimetrale.</p></td>
</tr>
</tbody>
</table>


## Riepilogo certificato - connettività per messaggistica istantanea pubblica


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente</th>
<th>Nome soggetto</th>
<th>Ordine/nomi alternativi soggetto (SAN)</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Esterno/ servizio Access Edge</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>sip.contoso.com</p>
<p>webcon.contoso.com</p>
<p>sip.fabrikam.com</p></td>
<td><p>Il certificato deve provenire da una CA pubblica e includere l'EKU server e l'EKU client se è necessario distribuire la connettività per la messaggistica istantanea pubblica con AOL. Il certificato viene assegnato alle interfacce perimetrali esterne per:</p>
<ul>
<li><p>servizio Access Edge</p></li>
<li><p>servizio Web Conferencing Edge</p></li>
<li><p>servizio A/V Edge</p></li>
</ul>
<p>I nomi SAN vengono aggiunti automaticamente al certificato in base alle definizioni nel generatore di topologie. È possibile aggiungere voci relative ai nomi SAN in base alle esigenze per ulteriori domini SIP e altre voci che è necessario supportare. Il nome soggetto viene replicato nel nome SAN e deve essere presente per garantire il corretto funzionamento.</p></td>
</tr>
</tbody>
</table>


## Riepilogo del certificato per il protocollo XMPP


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente</th>
<th>Nome soggetto</th>
<th>Ordine/nomi alternativi soggetto (SAN)</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Assegnare al servizio Access Edge del server perimetrale o del pool di server perimetrali</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>webcon.contoso.com</p>
<p>sip.contoso.com</p>
<p>sip.fabrikam.com</p>
<p>xmpp.contoso.com</p>
<p><strong>*.contoso.com</strong></p></td>
<td><p>Le prime tre voci SAN sono le normali voci SAN per un server perimetrale completo. La voce contoso.com è richiesta per la federazione con il partner XMPP a livello del dominio radice. Questa voce consentirà XMPP per tutti i domini con il suffisso *.contoso.com.</p></td>
</tr>
</tbody>
</table>

