---
title: Riepilogo DNS - Individuazione automatica in Lync Server 2013
TOCTitle: Riepilogo DNS - Individuazione automatica in Lync Server 2013
ms:assetid: b336a2ae-0e58-4b74-b606-aedbbd411587
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945644(v=OCS.15)
ms:contentKeyID: 52062294
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo DNS - Individuazione automatica in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

L'individuazione automatica è un servizio flessibile perché accetta la comunicazione tramite HTTP o HTTPS. A questo scopo, è necessario configurare correttamente il DNS (Domain Name System) e i certificati utilizzati dai server che ospitano il servizio di individuazione automatica. I requisiti dei certificati sono illustrati in [Riepilogo certificato - Individuazione automatica](lync-server-2013-certificate-summary-autodiscover.md).

> [!IMPORTANT]  
> La logica di ricerca DNS per i client Lync Server utilizza un ordine di risoluzione specifico. È consigliabile includere sempre nel DNS sia lyncdiscoverinternal.&lt;dominio&gt; che lyncdiscover.&lt;dominio&gt;. Se si esclude il record lyncdiscoverinternal.&lt;dominio&gt;, i client interni non saranno in grado di connettersi ai servizi desiderati o riceveranno una risposta errata di individuazione automatica.

### Record DNS interni

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di record</th>
<th>Nome host</th>
<th>Viene risolto in</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CNAME</p></td>
<td><p>Lyncdiscoverinternal.<em>&lt;nome dominio interno&gt;</em></p></td>
<td><p>FQDN dei servizi Web interni per il pool di server Director, se presente, o per il pool Front End se non si dispone di un Server Director.</p></td>
</tr>
<tr class="even">
<td><p>A (l'host, se IPv6, è AAAA)</p></td>
<td><p>lyncdiscoverinternal.<em>&lt;nome dominio interno&gt;</em></p></td>
<td><p>Indirizzo IP dei servizi Web interni (indirizzo IP virtuale, o VIP, se si utilizza il servizio di bilanciamento del carico) del pool di server Director, se disponibile, oppure del pool Front End, se non si dispone di un Server Director.</p></td>
</tr>
</tbody>
</table>


È necessario creare uno dei record DNS esterni seguenti:

### Record DNS esterni

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di record</th>
<th>Nome host</th>
<th>Viene risolto in</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CNAME</p></td>
<td><p>lyncdiscover. <em>&lt;dominiosip&gt;</em></p></td>
<td><p>FQDN dei servizi Web esterni per il pool di server Director, se disponibile, oppure del pool Front End, se non si dispone di un Server Director.</p></td>
</tr>
<tr class="even">
<td><p>A (l'host, se IPv6, è AAAA)</p></td>
<td><p>lyncdiscover. <em>&lt;dominiosip&gt;</em></p></td>
<td><p>Indirizzo IP esterno o pubblico del proxy inverso.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Il traffico esterno attraversa il proxy inverso.




> [!NOTE]
> I client dei dispositivi mobili non supportano certificati SSL (Secure Sockets Layer) multipli da domini diversi. Di conseguenza, il reindirizzamento CNAME a domini diversi non è supportato in HTTPS. Ad esempio, un record CNAME DNS per lyncdiscover.contoso.com che esegue il reindirizzamento a un indirizzo director.contoso.net non è supportato in HTTPS. In una topologia di questo tipo, un client di dispositivo mobile deve utilizzare il protocollo HTTP per la prima richiesta, in modo che il reindirizzamento CNAME venga risolto in HTTP. Per le richieste successive viene quindi utilizzato HTTPS. Per supportare questo scenario, è necessario configurare il proxy inverso con una regola di pubblicazione Web per la porta 80 (HTTP). Per ulteriori informazioni, vedere la sezione relativa alla creazione di una regola di pubblicazione Web per la porta 80, in <A href="lync-server-2013-configuring-the-reverse-proxy-for-mobility.md">Configurazione del proxy inverso per i dispositivi mobili in Lync Server 2013</A>. Il reindirizzamento CNAME allo stesso dominio è supportato in HTTPS. In questo caso, il certificato del dominio di destinazione copre il dominio di origine.



## Vedere anche

#### Attività

[Configurazione del proxy inverso per i dispositivi mobili in Lync Server 2013](lync-server-2013-configuring-the-reverse-proxy-for-mobility.md)  

#### Concetti

[Riepilogo certificato - Individuazione automatica](lync-server-2013-certificate-summary-autodiscover.md)

