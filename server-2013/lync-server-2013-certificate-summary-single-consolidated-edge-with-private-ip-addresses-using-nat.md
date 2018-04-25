---
title: 'Lync Server 2013: Riepilogo dei certificati - singola topologia perimetrale consolidata con indirizzi IP privati tramite NAT'
TOCTitle: Riepilogo dei certificati - singola topologia perimetrale consolidata con indirizzi IP privati tramite NAT
ms:assetid: 6de6680e-5f47-48e6-8e06-4994d710ea6d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398519(v=OCS.15)
ms:contentKeyID: 49300910
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo dei certificati - singola topologia perimetrale consolidata con indirizzi IP privati tramite NAT in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Microsoft Lync Server 2013 utilizza i certificati per l'autenticazione reciproca con altri server e per crittografare i dati da server a server e da server a client. Per i certificati è richiesta la corrispondenza tra i nomi dei record DNS (Domain Name System) associati ai server e il nome soggetto (SN) e il nome alternativo soggetto (SAN) nel certificato. Per il mapping corretto di server, record DNS e voci di certificato, è necessario pianificare con attenzione i nomi di dominio completo (FQDN) previsti per i server, registrati in DNS e le voci SN e SAN nel certificato.

Il certificato assegnato alle interfacce esterne del server perimetrale è richiesto da un'Autorità di certificazione pubblica. Nel seguente articolo sono elencate le Autorità di certificazione pubbliche che hanno fornito certificati corretti per Unified Communications: [http://go.microsoft.com/fwlink/p/?linkid=3052\&kbid=929395](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=929395). Quando si richiede il certificato, è possibile servirsi della richiesta generata dal Distribuzione guidata di Lync Server o creare una richiesta manuale attraverso i cmdlet di Lync Server Management Shell o tramite il processo indicato da un'Autorità di certificazione pubblica. Per informazioni sui cmdlet di Lync Server Management Shell per la gestione dei certificati, vedere [Cmdlet per i certificati e l'autenticazione](lync-server-2013-certificate-and-authentication-cmdlets.md). Quando si assegna un certificato, lo si assegna all'interfaccia del servizio Access Edge, all'interfaccia del servizio Web Conferencing Edge e al servizio di autenticazione A/V. Il servizio di autenticazione A/V è diverso dal servizio A/V Edge, il quale non si serve di un certificato per la crittografia dei flussi audio e video. L'interfaccia interna del server perimetrale può servirsi di un certificato emesso da un'Autorità di certificazione interna all'organizzazione, o pubblica. Il certificato dell'interfaccia interna si serve unicamente del nome soggetto (SN) e non richiede o utilizza voci SAN.


> [!NOTE]
> Nella tabella seguente viene illustrata una seconda voce SIP (sip.fabrikam.com) nell'elenco dei nomi alternativi soggetto come riferimento. Per ogni dominio SIP presente nell'organizzazione, è necessario che nell'elenco dei nomi alternativi soggetto dei certificati sia incluso un FQDN corrispondente.



## Certificati necessari per la perimetrale consolidata singola con indirizzi IP privati che usano NAT


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
<td><p>Singola topologia perimetrale consolidata (perimetro esterno)</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>webcon.contoso.com</p>
<p>sip.contoso.com</p>
<p>sip.fabrikam.com</p></td>
<td><p>Il certificato deve provenire da una CA pubblica e includere l'EKU server e l'EKU client se è necessario distribuire la connettività per la messaggistica istantanea pubblica con AOL. Il certificato viene assegnato alle interfacce perimetrali esterne per:</p>
<ul>
<li><p>Access Edge</p></li>
<li><p>Conferencing Edge</p></li>
<li><p>A/V Edge</p></li>
</ul>
<p>I nomi SAN vengono aggiunti automaticamente al certificato in base alle definizioni nel generatore di topologie. È possibile aggiungere voci relative ai nomi SAN in base alle esigenze per ulteriori domini SIP e altre voci che è necessario supportare. Il nome soggetto viene replicato nel nome SAN e deve essere presente per garantire il corretto funzionamento.</p></td>
</tr>
<tr class="even">
<td><p>Singola topologia perimetrale consolidata (perimetro interno)</p></td>
<td><p>lsedge.contoso.net</p></td>
<td><p>Nessun nome alternativo soggetto necessario</p></td>
<td><p>Il certificato può essere emesso da una CA pubblica o privata e deve contenere l'EKU server. Il certificato viene assegnato all'interfaccia perimetrale interna.</p></td>
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
<td><p>Esterno/Access Edge</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>sip.contoso.com</p>
<p>webcon.contoso.com</p>
<p>sip.fabrikam.com</p></td>
<td><p>Il certificato deve provenire da una CA pubblica e includere l'EKU server e l'EKU client se è necessario distribuire la connettività per la messaggistica istantanea pubblica con AOL. Il certificato viene assegnato alle interfacce perimetrali esterne per:</p>
<ul>
<li><p>Access Edge</p></li>
<li><p>Conferencing Edge</p></li>
<li><p>A/V Edge</p></li>
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

