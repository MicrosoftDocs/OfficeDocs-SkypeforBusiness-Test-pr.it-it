---
title: Requisiti di DNS per pool Front End
TOCTitle: Requisiti di DNS per pool Front End
ms:assetid: ba28919c-fbbe-4c54-8bf9-2b0cd3fa39c7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412910(v=OCS.15)
ms:contentKeyID: 49301797
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti di DNS per pool Front End

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questa sezione vengono descritti i record DNS (Domain Name System) necessari per la distribuzione di pool Front End.

## Record DNS per i pool Front End

Nella tabella seguente sono indicati i requisiti DNS per la distribuzione di un pool Front End di Lync Server 2013.

### Requisiti di DNS per un pool Front End

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Scenario di distribuzione</th>
<th>Requisito DNS</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Pool Front End con più Front End Server e un dispositivo di bilanciamento del carico hardware (indipendentemente dal fatto che nel pool sia implementato anche il bilanciamento del carico DNS)</p></td>
<td><p>Quando si utilizzano sia il bilanciamento del carico DNS che un dispositivo di bilanciamento del carico hardware, è necessario ospitare record (A). Creare un record A interno che risolva il nome di dominio completo (FQDN) del pool Front End per il bilanciamento del carico DNS. Creare un record (A) host interno per i servizi Web interni per l'indirizzo IP virtuale (VIP) del dispositivo di bilanciamento del carico. È necessario utilizzare i servizi Web interni definiti nel Generatore di topologie.</p>
<p>Se, ad esempio, si utilizzano sia il bilanciamento del carico DNS che il bilanciamento del carico hardware, si disporrà di un record A per ogni Front End Server in un pool per il bilanciamento del carico DNS e di un record A per i servizi Web interni che fanno riferimento all'indirizzo IP virtuale del dispositivo di bilanciamento del carico hardware:</p>
<ul>
<li><p>Bilanciamento del carico DNS:   Pool01.contoso.net   Indirizzo IP del pool   10.10.10.5</p>

> [!WARNING]
> Ogni Front End Server disporrà inoltre di un record A distinto:


<ol>
<li><p>FE01.contoso.net    10.10.10.1</p></li>
<li><p>FE02.contoso.net    10.10.10.2</p></li>
<li><p>FE03.contoso.net    10.10.10.3</p></li>
<li><p>FE04.contoso.net    10.10.10.4</p></li>
</ol></li>
<li><p>Bilanciamento del carico hardware:   WebInternal.contoso.net   Indirizzo IP VIP bilanciamento carico hardware   192.168.10.5</p></li>
</ul>
<p>Tutto il traffico, tranne quello HTTP/HTTPS, utilizzerà il record Pool01.contoso.net. Il traffico HTTP/HTTPS utilizzerà l'indirizzo dei servizi Web interni definito 192.168.10.5</p></td>
</tr>
<tr class="even">
<td><p>Pool Front End con bilanciamento del carico DNS</p></td>
<td><p>Un set di record A interni che risolvono l'FQDN del pool nell'indirizzo IP di ogni server nel pool. Deve esistere un solo record A per ogni server nel pool.</p></td>
</tr>
<tr class="odd">
<td><p>Pool Front End con bilanciamento del carico DNS</p></td>
<td><p>Un set di record A interni che risolvono l'FQDN di ogni server nell'indirizzo IP di tale server. Per informazioni dettagliate, vedere <a href="lync-server-2013-dns-load-balancing.md">Bilanciamento del carico DNS in Lync Server 2013</a> nella documentazione relativa alla pianificazione.</p></td>
</tr>
<tr class="even">
<td><p>Pool Front End con un solo Front End Server e un database back-end dedicato, ma senza servizio di bilanciamento del carico</p></td>
<td><p>Un record A interno che risolve l'FQDN del pool Front End nell'indirizzo IP del singolo server Enterprise Edition Front End Server.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Accesso client automatico</p></td>
<td><p>Per ogni dominio SIP supportato, un record SRV per _sipinternaltls._tcp.&lt;dominio&gt; sulla porta 5061 corrispondente all'FQDN del pool Front End che esegue l'autenticazione e il reindirizzamento delle richieste di accesso dei client. Per informazioni dettagliate, vedere <a href="lync-server-2013-dns-requirements-for-automatic-client-sign-in.md">Requisiti DNS per l'accesso automatico dei client in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>Individuazione del servizio Web Aggiornamento dispositivi tramite dispositivi per comunicazioni unificate</p></td>
<td><p>Un record A interno con il nome ucupdates-r2.&lt;dominio SIP&gt; risolto nel'indirizzo IP del pool Front End che ospita il servizio Web Aggiornamento dispositivi. Se viene acceso un dispositivo per comunicazioni unificate, ma un utente non ha mai eseguito l'accesso al dispositivo, il record A consente al dispositivo di individuare il pool Front End che ospita il servizio Web Aggiornamento dispositivi e ottenere gli aggiornamenti. In caso contrario, i dispositivi ottengono queste informazioni tramite il provisioning di tipo in-band la prima volta che un utente esegue l'accesso.</p>

> [!IMPORTANT]
> Se è disponibile una distribuzione esistente del servizio Web Aggiornamento dispositivi in Lync Server 2010, è già stato creato un record A interno con il nome ucupdates.<em>&lt;dominio SIP&gt;</em>. Per Microsoft Office Communications Server 2007 R2 è necessario creare un record A DNS aggiuntivo con il nome ucupdates-r2.<em>&lt;dominio SIP&gt;</em>.

</td>
</tr>
<tr class="odd">
<td><p>Un proxy inverso per il supporto del traffico HTTP</p></td>
<td><p>Un record A esterno che risolve il nome di dominio completo (FQDN) della Web farm esterna nell'indirizzo IP esterno del proxy inverso. Per informazioni dettagliate, vedere <a href="lync-server-2013-determine-dns-requirements.md">Determinare i requisiti di DNS per Lync Server 2013</a> nella documentazione relativa alla pianificazione.</p></td>
</tr>
</tbody>
</table>


Nella tabella seguente viene illustrato un esempio dei record DNS necessari per il nome di dominio completo (FQDN) della Web farm interna.

### Record DNS di esempio per il nome di dominio completo (FQDN) della Web farm interna

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN Web farm interna</th>
<th>FQDN pool</th>
<th>Record A DNS</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>webcon.contoso.com</p></td>
<td><p>ee-pool.contoso.com</p></td>
<td><p>Record A DNS per ee-pool.contoso.com che viene risolto nell'indirizzo VIP del servizio di bilanciamento del carico utilizzato dai Front End Server.</p>
<p>Record A DNS per webcon.contoso.com che viene risolto nell'indirizzo VIP del servizio di bilanciamento del carico utilizzato dai Front End Server.</p></td>
</tr>
<tr class="even">
<td><p>ee-pool.contoso.com</p></td>
<td><p>ee-pool.contoso.com</p></td>
<td><p>Record A DNS per ee-pool.contoso.com che viene risolto nell'indirizzo IP virtuale (VIP) del servizio di bilanciamento del carico utilizzato dai server Enterprise Edition Front End Server nel pool Front End.</p>
<p>Si noti che se si utilizza il bilanciamento del carico DNS nel pool, il pool Front End e la Web farm interna non potranno avere lo stesso FQDN.</p></td>
</tr>
</tbody>
</table>

