---
title: 'Lync Server 2013: Requisiti di DNS per il pool Front End'
TOCTitle: Requisiti di DNS per il pool Front End
ms:assetid: 02d2aa6b-9e01-437b-a2df-00590280150d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398082(v=OCS.15)
ms:contentKeyID: 49299504
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti di DNS per il pool Front End in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per eseguire correttamente questa procedura, è necessario connettersi al server o al dominio almeno come membro del gruppo Domain Admins o DnsAdmins.

Configurare i record DNS (Domain Name System) necessari prima di pubblicare la topologia in Generatore di topologie. Alcuni dei nomi di dominio completo (FQDN) utilizzati nella configurazione di una distribuzione di Lync Server 2013 inoltre sono FQDN di server logici e non fisici, pertanto prima della pubblicazione è necessario eseguire ulteriori attività di configurazione DNS.


> [!WARNING]
> Lync Server 2013 non supporta domini a etichetta singola. Ad esempio è supportata una foresta con un dominio radice denominato <STRONG>contoso.local</STRONG> ma non è supportato un dominio radice denominato <STRONG>local</STRONG>. Per informazioni dettagliate, vedere l'articolo 300684 della Microsoft Knowledge Base "Informazioni sulla configurazione di Windows per domini con nomi DNS con etichetta singola" all'indirizzo <A class=uri href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=300684">http://go.microsoft.com/fwlink/p/?linkid=3052&amp;kbid=300684</A>.



> [!important]  
> Il nome specificato deve essere uguale al nome computer configurato nel server. Per impostazione predefinita, il nome di un computer non aggiunto a un dominio è un nome breve e non un FQDN. Generatore di topologie usa gli FQDN e non i nomi brevi. <strong>Usare solo i caratteri standard</strong> (A-Z, a-z, 0-9 e i trattini) quando si assegnano gli FQDN dei server che eseguono Lync Server, server perimetrali e pool. Non usare i caratteri Unicode o i caratteri di sottolineatura. I caratteri non standard di un FQDN spesso non sono supportati dalle autorità di certificazione (CA) pubbliche e DNS esterne (quando l'FQDN deve essere assegnato al nome soggetto nel certificato).

Prima di iniziare a utilizzare la topologia dopo che è stata distribuita, verificare che siano stati creati i record DNS e Active Directory seguenti, in base alle proprie esigenze per funzionalità specifiche:

  - Ogni ruolo del server che esisterà nella topologia deve essere pubblicato come oggetto di Active Directory (tale operazione verrà eseguita aggiungendo il computer al dominio).

  - Deve esistere un record A DNS per ogni server.

  - Deve esistere un record SRV DNS per ogni dominio SIP se si intende utilizzare l'accesso automatico per i client nel formato \_sipinternal\_tcp. *\<dominio SIP\>* . Se si userà la configurazione manuale per i client, questo record non è necessario.

  - Deve esistere un record A DNS per ogni URL semplice configurato. Vi sono in genere quattro URL semplici: meet, dialin, lwa e scheduler. Vi è inoltre l'URL semplice admin che è un URL speciale per l'accesso al Pannello di controllo di Lync Server 2013.

  - Il computer basato su SQL Server deve essere aggiunto al dominio e raggiungibile dal computer da cui Generatore di topologie esegue la pubblicazione.

La tabella seguente è basata sulle architetture di riferimento presentate nella sezione di pianificazione. Per informazioni dettagliate, vedere [Scenari per l'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-scenarios-for-external-user-access.md) nella documentazione relativa alla pianificazione.

### Record DNS necessari per il pool Front End

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Posizione</th>
<th>Tipo</th>
<th>FQDN</th>
<th>Corrisponde a/Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DNS interno</p></td>
<td><p>A</p></td>
<td><p>pool01.contoso.net</p></td>
<td><p>Pool01 (bilanciamento del carico DNS). Richiede un record A DNS per l'indirizzo IP di ogni Front End Server all'interno del pool con mapping al FQDN del pool.</p></td>
</tr>
<tr class="even">
<td><p>DNS interno</p></td>
<td><p>A</p></td>
<td><p>pool01.contoso.net</p></td>
<td><p>Pool01 (IP virtuale (VIP) del dispositivo di bilanciamento del carico hardware).</p></td>
</tr>
<tr class="odd">
<td><p>DNS interno</p></td>
<td><p>A</p></td>
<td><p>fe01.contoso.net</p>
<p>fe02.contoso.net</p>
<p>fe03.contoso.net</p>
<p>…</p></td>
<td><p>Pool01 Front End Server (NODO 1).</p>
<p>Pool01 Front End Server (NODO 2).</p>
<p>Pool01 Front End Server (NODO 3).</p>
<p>…</p></td>
</tr>
<tr class="even">
<td><p>DNS interno</p></td>
<td><p>A</p></td>
<td><p>fe02.contoso.net</p></td>
<td><p>Pool01 Front End Server (NODO 2).</p></td>
</tr>
<tr class="odd">
<td><p>DNS interno</p></td>
<td><p>A</p></td>
<td><p>lsweb.contoso.net</p></td>
<td><p>Pool01 (VIP) per traffico Web da client a server.</p></td>
</tr>
<tr class="even">
<td><p>DNS interno</p></td>
<td><p>A</p></td>
<td><p>sqlbe.contoso.net</p></td>
<td><p>Pool01 server back-end che esegue SQL Server 2008 R2.</p></td>
</tr>
<tr class="odd">
<td><p>DNS interno</p></td>
<td><p>A</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>Necessario per Lync Phone Edition, l'accesso automatico dei client senza record SRV DNS e per la corrispondenza esatta dei domini. Non necessario in tutti i casi.</p></td>
</tr>
<tr class="even">
<td><p>DNS interno</p></td>
<td><p>A</p></td>
<td><p>sip.fabrikam.com</p></td>
<td><p>Presuppone un secondo dominio SIP. Necessario per Lync Phone Edition, l'accesso automatico dei client senza record SRV DNS e per la corrispondenza esatta dei domini. Non necessario in tutti i casi.</p></td>
</tr>
<tr class="odd">
<td><p>DNS interno</p></td>
<td><p>A</p></td>
<td><p>dialin.contoso.com</p></td>
<td><p>URL semplice per le conferenze telefoniche con accesso esterno pubblicate internamente. Il Front End Server (o il Server Director, se installato) risponde alle query dell'URL semplice.</p></td>
</tr>
<tr class="even">
<td><p>DNS interno</p></td>
<td><p>A</p></td>
<td><p>meet.contoso.com</p></td>
<td><p>URL semplice per le conferenze pubblicate internamente. Il Front End Server (o il Server Director, se installato) risponde alle query dell'URL semplice.</p></td>
</tr>
<tr class="odd">
<td><p>DNS interno</p></td>
<td><p>A</p></td>
<td><p>admin.contoso.com</p>
<p>admin</p></td>
<td><p>Record facoltativo, URL semplice per il Pannello di controllo di Lync Server 2013 pubblicato internamente. Il Front End Server (o il Server Director, se installato) risponde alle query dell'URL semplice. È consigliato solo il nome post (non il nome di dominio).</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> VIP = indirizzo IP virtuale per il dispositivo di bilanciamento del carico hardware



## Record SRV DNS per il pool Front End


<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Posizione</th>
<th>Tipo</th>
<th>FQDN</th>
<th>FQDN di destinazione</th>
<th>Porta</th>
<th>Corrisponde a/Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DNS interno</p></td>
<td><p>SRV</p></td>
<td><p>_sipinternaltls._tcp.contoso.com</p></td>
<td><p>pool01.contoso.com</p></td>
<td><p>5061</p></td>
<td><p>Necessario per la configurazione automatica dei client Lync 2013, per il funzionamento interno.</p></td>
</tr>
<tr class="even">
<td><p>DNS interno</p></td>
<td><p>SRV</p></td>
<td><p>_sipinternaltls._tcp.fabrikam.com</p></td>
<td><p>pool01.fabrikam.com</p></td>
<td><p>5061</p></td>
<td><p>Necessario per la configurazione automatica dei client Lync 2013, per il funzionamento interno.</p></td>
</tr>
<tr class="odd">
<td><p>DNS interno</p></td>
<td><p>SRV</p></td>
<td><p>_ntp._udp.contoso.com</p></td>
<td><p>dc01.contoso.com</p></td>
<td><p>123</p></td>
<td><p>Origine NTP (Network Time Protocol) necessaria per i dispositivi che eseguono Lync Phone Edition. Internamente deve puntare al controller di dominio. Se quest'ultimo non è definito, tenterà di usare il server NTP time.windows.com.</p></td>
</tr>
</tbody>
</table>

