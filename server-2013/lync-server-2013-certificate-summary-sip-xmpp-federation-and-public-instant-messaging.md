---
title: Riepilogo dei certificati - SIP, federazione di XMPP e messaggistica istantanea pubblica
TOCTitle: Riepilogo dei certificati - SIP, federazione di XMPP e messaggistica istantanea pubblica
ms:assetid: 933d6351-cfa6-4432-b3ed-1aff3ac92065
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ618372(v=OCS.15)
ms:contentKeyID: 49301343
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo dei certificati - SIP, federazione di XMPP e messaggistica istantanea pubblica

 

_**Ultima modifica dell'argomento:** 2015-03-09_

I certificati necessari per la federazione con Microsoft Lync Server 2013, Lync Server 2010 e Office Communications Server vengono in genere configurati dall'utente che li richiede e assegna al server perimetrale.

Tra i requisiti dei certificati per consentire e stabilire le comunicazioni con partner XMPP (Extensible Messaging and Presence Protocol) è prevista l'aggiunta di voci per i domini XMPP. Il record incluso nel certificato come nome alternativo del soggetto (SAN) corrisponderà al dominio che può partecipare alle comunicazioni XMPP. Il dominio può essere a livello della radice (ad esempio, contoso.com) se si desidera abilitare XMPP per l'intero dominio oppure può corrispondere a domini figlio selezionati (ad esempio, corp.contoso.com, finance.contoso.com) se si desidera abilitare XMPP per un sottoinsieme di utenti.

Per configurare i certificati per la connettività per la messaggistica istantanea pubblica, osservare che non ci sono differenze rispetto ad altri tipi di federazione SIP o certificati del server perimetrale standard, con l'unica eccezione che America Online (AOL) richiede che il certificato o i certificati (in presenza di un pool di server perimetrali) contengano anche l'EKU del client, ovvero un'integrazione al certificato che fa parte del certificato pubblico esterno assegnato al server perimetrale.

Per accertarsi di soddisfare correttamente i requisiti dei certificati per la distribuzione di server perimetrale, leggere gli argomenti indicati nella sezione **Vedere anche**.



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
<th>Nomi alternativo soggetto</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Esterno/Access Edge</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>sip.contoso.com</p>
<p>webcon.contoso.com</p>
<p>contoso.com</p>

> [!NOTE]
> Per supportare lo spazio dei nomi XMPP di contoso.com


<p>sip.fabrikam.com</p>

> [!NOTE]
> Per supportare lo spazio dei nomi SIP di fabrikam.com


<p>fabrikam.com</p>

> [!NOTE]
> Per supportare lo spazio dei nomi XMPP di fabrikam.com


</td>
<td><p>Il certificato deve essere stato emesso da un'autorità di certificazione pubblica e deve includere l'EKU del server e del client se si intende distribuire la connettività per la messaggistica istantanea pubblica con AOL. Il certificato viene assegnato alle interfacce del server perimetrale esterno per:</p>
<ul>
<li><p>servizio Access Edge</p></li>
<li><p>servizio Web Conferencing Edge</p></li>
<li><p>servizio A/V Edge</p></li>
</ul>

> [!NOTE]
> Dal punto di vista tecnico, un certificato non viene assegnato a A/V Edge. L'autenticazione e le comunicazioni sicure vengono gestite tramite il servizio di autenticazione Media Relay esterno (MRAS). MRAS utilizza il certificato assegnato all'interfaccia interna del server perimetrale.


<p>I nomi SAN vengono aggiunti automaticamente al certificato in base alle definizioni nel generatore di topologie. È possibile aggiungere voci relative ai nomi SAN in base alle esigenze per ulteriori domini SIP e altre voci che è necessario supportare. Il nome soggetto viene replicato nel nome SAN e deve essere presente per garantire il corretto funzionamento.</p></td>
</tr>
</tbody>
</table>


## Vedere anche

#### Attività

[Esempio di configurazione XMPP in Lync Server 2013 - federazione di XMPP con Google Talk](lync-server-2013-example-xmpp-configuration-–-xmpp-federation-with-google-talk.md)  

#### Concetti

[Pianificare i certificati dei server perimetrali in Lync Server 2013](lync-server-2013-plan-for-edge-server-certificates.md)  
[Riepilogo dei certificati - singola topologia perimetrale consolidata con indirizzi IP privati tramite NAT in Lync Server 2013](lync-server-2013-certificate-summary-single-consolidated-edge-with-private-ip-addresses-using-nat.md)  
[Riepilogo dei certificati - singola topologia perimetrale consolidata con indirizzi IP pubblici in Lync Server 2013](lync-server-2013-certificate-summary-single-consolidated-edge-with-public-ip-addresses.md)  
[Riepilogo dei certificati - topologia perimetrale consolidata con scalabilità implementata, bilanciamento del carico DNS con indirizzi IP privati tramite NAT in Lync Server 2013](lync-server-2013-certificate-summary-scaled-consolidated-edge-dns-load-balancing-with-private-ip-addresses-using-nat.md)  
[Riepilogo dei certificati - topologia perimetrale consolidata con scalabilità implementata, bilanciamento del carico DNS con indirizzi IP pubblici in Lync Server 2013](lync-server-2013-certificate-summary-scaled-consolidated-edge-dns-load-balancing-with-public-ip-addresses.md)  
[Riepilogo dei certificati - topologia perimetrale consolidata con scalabilità implementata e servizi di bilanciamento del carico hardware in Lync Server 2013](lync-server-2013-certificate-summary-scaled-consolidated-edge-with-hardware-load-balancers.md)

