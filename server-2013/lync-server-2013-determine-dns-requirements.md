---
title: 'Lync Server 2013: Determinare i requisiti di DNS'
TOCTitle: Determinare i requisiti di DNS
ms:assetid: 95777017-6282-44c0-a685-f246af0501b4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398758(v=OCS.15)
ms:contentKeyID: 49301379
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Determinare i requisiti di DNS per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Utilizzare il diagramma di flusso seguente per determinare i requisiti DNS (Domain Name System). Quando pertinente, vengono segnalate le modifiche introdotte con gli aggiornamenti cumulativi per Lync Server 2013 di febbraio 2013.

> [!IMPORTANT]  
> Microsoft Lync Server 2013 supporta l'uso dell'assegnazione indirizzi IPv6. Per usare gli indirizzi IPv6 è inoltre necessario supportare DNS IPv6 e configurare i record AAAA (noti come “quadrupla A”) dell'host DNS. Nelle distribuzioni in cui si usano indirizzi sia IPv4 sia IPv6, è preferibile configurare e gestire sia i record A per IPv4 sia i record AAAA dell'host per IPv6. Anche se la distribuzione è passata interamente a IPv6, i record dell'host DNS IPv4 potrebbero essere comunque necessari per utenti esterni che usano ancora IPv4.

**Diagramma di flusso Determinazione dei requisiti DNS**

![Diagramma di flusso dei requisiti DNS](images/Gg398758.175782ac-363e-408a-912f-8991bf152970(OCS.15).jpg "Diagramma di flusso dei requisiti DNS")

> [!IMPORTANT]  
> Per impostazione predefinita, il nome di un computer non aggiunto a un dominio è un nome host, non un nome di dominio completo (FQDN). Generatore di topologie usa i nomi di dominio completi, non i nomi host, pertanto è necessario aggiungere un suffisso DNS al nome di ogni computer non aggiunto a un dominio da distribuire come server perimetrale. Quando si assegnano i nomi di dominio completi dei server Lync, dei server perimetrali e dei pool è consigliabile <strong>utilizzare solo i caratteri standard</strong> (inclusi i caratteri A-Z, a-z, 0-9 e i trattini). I caratteri non standard di un nome di dominio completo spesso non sono supportati nel sistema DNS esterno e nelle autorità di certificazione pubbliche (quando il nome di dominio completo deve essere assegnato al nome soggetto nel certificato). Per ulteriori informazioni, vedere <a href="lync-server-2013-configure-dns-host-records.md">Configurare i record host DNS per Lync Server 2013</a>.

## Modalità di individuazione dei servizi da parte dei client Lync

Microsoft Lync 2010, Lync 2013 e Lync Mobile sono simili per quanto riguarda il modo in cui il client individua i servizi in Lync Server 2013 e vi accede. L'eccezione degna di nota è rappresentata dall' app Windows Store Lync che utilizza un diverso processo di individuazione dei servizi. In questa sezione sono descritti in dettaglio due scenari per l'individuazione dei servizi da parte dei client. Il primo scenario si basa sul metodo tradizionale che utilizza una serie di record host SRV e A, mentre il secondo utilizza solo i record del servizio di individuazione automatica. Gli aggiornamenti cumulativi per i client desktop modificano il processo di individuazione DNS da Lync Server 2010. Per tutti i client, il processo di query DNS continua fino a quando non viene completata correttamente una query oppure viene esaurito l'elenco dei record DNS possibili e l'errore finale viene restituito al client.

Per tutti i client **ad eccezione** dell' app Windows Store Lync, durante la ricerca DNS i record SRV sono sottoposti a query e restituiti al client nell'ordine seguente:

1.  lyncdiscoverinternal. *\<dominio\>*    Record A (host) per il servizio di individuazione automatica nei servizi Web interni

2.  lyncdiscover. *\<dominio\>*    Record A (host) per il servizio di individuazione automatica nei servizi Web esterni

3.  \_sipinternaltls.\_tcp. *\<dominio\>*    Record del localizzatore del servizio SRV per le connessioni TLS interne

4.  \_sipinternal.\_tcp. *\<dominio\>*    Record del localizzatore del servizio SRV per le connessioni TCP interne (eseguite solo se TCP è consentito)

5.  \_sip.\_tls. *\<dominio\>*    Record del localizzatore del servizio SRV per le connessioni TLS esterne

6.  sipinternal. *\<dominio\>*    Record A (host) per il pool Front End o il Server Director, risolvibile solo nella rete interna

7.  sip. *\<dominio\>*    Record A (host) per il pool Front End o il Server Director nella rete interna oppure il servizio Access Edge quando il client è esterno

8.  sipexternal. *\<dominio\>*    Record A (host) per il servizio Access Edge quando il client è esterno

Per l' app Windows Store Lync il processo cambia completamente perché vengono utilizzati due record:

1.  lyncdiscoverinternal. *\<dominio\>*    Record A (host) per il servizio di individuazione automatica nei servizi Web interni

2.  lyncdiscover. *\<dominio\>*    Record A (host) per il servizio di individuazione automatica nei servizi Web esterni

Non è previsto il fallback ad altri tipi di record.

La differenza tra i metodi utilizzati per i client più recenti rispetto a quelli meno recenti è che il servizio di individuazione automatica sta diventando il metodo preferito per l'individuazione di tutti i servizi.

Quando viene stabilita una connessione, il servizio di individuazione automatica restituisce gli URL di tutti i servizi Web del pool principale dell'utente, compresi gli URL del servizio Mobility (noto come Mcx dalla directory virtuale creata per il servizio in IIS), di Microsoft Lync Web App e di Web Scheduler. Sia l'URL interno che quello esterno del servizio Mobility, tuttavia, sono associati all'FQDN dei servizi Web esterni. Per questo motivo, sia esso interno o esterno alla rete, un dispositivo mobile si connette al servizio Mobility sempre esternamente, tramite il proxy inverso.

Se sono stati installati gli aggiornamenti cumulativi per Lync Server 2013 di febbraio 2013, il servizio di individuazione automatica restituisce inoltre riferimenti a Internal/UCWA, External/UCWA e UCWA. Queste voci fanno riferimento al componente Web UCWA (Unified Communications Web API). Attualmente viene utilizzata solo la voce UCWA e offre un riferimento a un URL per il componente Web. L'API UCWA è utilizzata dai client Lync 2013 Mobile al posto del servizio Mobility Mcx utilizzato dai client Lync 2010 Mobile.


> [!NOTE]
> Quando si creano i record SRV, è importante ricordare che questi devono puntare a un record A o AAAA (se si usa l'assegnazione indirizzi IPv6) DNS nello stesso dominio in cui viene creato il record DNS SRV. Se ad esempio il record SRV si trova in contoso.com, il record A e AAAA (se si usa l'assegnazione indirizzi IPv6) al quale punta non può trovarsi in fabrikam.com.



> [!tip]  
> La configurazione predefinita prevede l'indirizzamento di tutto il traffico dei client mobili attraverso il sito esterno. È possibile modificare le impostazioni in modo da restituire solo l'URL interno, se preferibile per requisiti specifici. Con questa configurazione, gli utenti possono utilizzare le applicazioni mobili di Lync sui propri dispositivi mobili solo quando si trovano all'interno della rete aziendale. Per supportare questa configurazione, si utilizza il cmdlet <strong>Set-CsMcxConfiguration</strong>.


> [!NOTE]
> Benché le applicazioni mobili possano connettersi anche ad altri servizi di Lync Server 2013, ad esempio il Servizio Rubrica, le richieste Web delle applicazioni mobili vanno al nome di dominio completo Web esterno solo per il servizio per dispositivi mobili. Per le altre richieste di servizio, ad esempio le richieste della Rubrica, questa configurazione non è necessaria.



I dispositivi mobili supportano l'individuazione manuale dei servizi. In questo caso è necessario che ogni utente configuri le impostazioni dei dispositivi mobili con gli URI interni ed esterni completi del servizio di individuazione automatica, compresi percorso e protocollo, come illustrato di seguito:

  - https:// *\<FQDNPoolEst\>* /Autodiscover/autodiscoverservice.svc/Root per l'accesso esterno

  - https:// *\<FQDNPoolInt\>* /AutoDiscover/AutoDiscover.svc/Root per l'accesso interno

L'individuazione automatica è consigliabile rispetto all'individuazione manuale. L'utilizzo di impostazioni manuali, tuttavia, può essere utile per la risoluzione dei problemi di connettività dei dispositivi mobili.

## Configurazione di DNS split-brain con Lync Server

Il termine DNS split-brain ha varie definizioni, ad esempio DNS suddiviso o DNS split-horizon. Questo termine descrive semplicemente una configurazione in cui esistono due zone DNS con lo stesso spazio dei nomi, di cui una tuttavia serve solo richieste interne e l'altra solo richieste esterne. Tuttavia, molti record DNS SRV e A contenuti nel DNS interno non saranno contenuti nel DNS esterno e viceversa. Nei casi in cui lo stesso record DNS è presente sia nel DNS esterno che nel DNS esterno, ad esempio www.contoso.com, l'indirizzo IP restituito sarà diverso in base al punto in cui viene eseguita la query (interno o esterno).

> [!IMPORTANT]  
> Attualmente, il sistema DNS split-brain non è supportato per le funzionalità per dispositivi mobili e più nello specifico per i record DNS LyncDiscover e LyncDiscoverInternal. LyncDiscover deve essere definito su un server DNS esterno e LyncDiscoverInternal su un server DNS interno.

Ai fini di questo argomento, verrà usato il termine DNS split-brain.

Se si sta configurando un DNS split-brain, le zone interna ed esterna seguenti contengono un riepilogo dei tipi di record DNS necessari in ogni zona. Per informazioni dettagliate, vedere [Scenari per l'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-scenarios-for-external-user-access.md).

**DNS interno:**

  - Contiene una zona DNS denominata contoso.com per cui è autorevole

  - La zona contoso.com interna contiene:
    
      - Record SRV e A e AAAA (se si usa l'assegnazione indirizzi IPv6) DNS per la configurazione automatica del client Lync Server 2013 (facoltativo)
    
      - Record DNS A e AAAA (se si usa l'assegnazione indirizzi IPv6) o CNAME per l'individuazione automatica dei servizi Web di Lync Server 2013 (facoltativo)
    
      - Record A e AAAA (se si usa l'assegnazione indirizzi IPv6) DNS per il nome del pool Front End, il server Director o il nome del pool di server Director e tutti i server interni che eseguono Lync Server 2013 nella rete aziendale
    
      - Record A e AAAA (se si usa l'assegnazione indirizzi IPv6) DNS per l'interfaccia perimetrale interna di ogni istanza di Lync Server 2013, server perimetrale nella rete perimetrale
    
      - Record A e AAAA (se si usa l'assegnazione indirizzi IPv6) DNS per l'interfaccia interna di ogni server proxy inverso nella rete perimetrale (facoltativo per la gestione del proxy inverso)
    
      - Tutte le interfacce perimetrali interne di server perimetrale di Lync Server 2013 nella rete perimetrale usano la zona DNS interna per risolvere le query in contoso.com
    
      - Tutti i server che eseguono Lync Server 2013 e i client che eseguono Lync 2013 nella rete aziendale puntano ai server DNS interni per la risoluzione di query in contoso.com oppure usano file HOSTS su ogni server perimetrale ed elencano i record A e AAAA (se si usa l'assegnazione indirizzi IPv6) per il successivo server hop, in particolare il server Director o il VIP del server Director, il VIP del pool Front End o il server Standard Edition

**DNS esterno:**

  - Contiene una zona DNS denominata contoso.com per cui è autorevole

  - La zona contoso.com esterna contiene:
    
      - Record SRV e A e AAAA (se si usa l'assegnazione indirizzi IPv6) per la configurazione automatica del client Lync Server 2013 (facoltativo)
    
      - Record DNS A e AAAA (se si usa l'assegnazione indirizzi IPv6) o CNAME per l'individuazione automatica dei servizi Web di Lync Server 2013 per l'uso in mobilità.
    
      - Record SRV e A e AAAA (se si usa l'assegnazione indirizzi IPv6) DNS per l'interfaccia perimetrale esterna di ogni istanza di Lync Server 2013, server perimetrale o indirizzo IP virtuale del dispositivo di bilanciamento del carico (VIP) nella rete perimetrale
    
      - Record DNS A e AAAA (se si usa l'assegnazione indirizzi IPv6) per l'interfaccia esterna del server proxy inverso o VIP per un pool di server proxy inversi nella rete perimetrale

## Configurazione automatica senza DNS split-brain

Se si usa DNS split-brain, un utente di Lync Server 2013 che accede internamente può utilizzare la caratteristica di configurazione automatica se la zona DNS interna contiene un record SRV \_sipinternaltls.\_tcp per ogni dominio SIP in uso. Se non si utilizza DNS split-brain, tuttavia, la configurazione interna automatica dei client che eseguono Lync non funzionerà, a meno che non si implementi una delle soluzioni alternative descritte più avanti in questa sezione. Il motivo è che Lync Server 2013 richiede che l'URI SIP dell'utente corrisponda al dominio del pool Front End designato per la configurazione automatica, come nelle versioni precedenti di Communicator.

Se ad esempio sono in uso due domini SIP, saranno necessari i record del servizio DNS (SRV) seguenti:

  - A scopo di confronto, se un utente esegue l'accesso come bob@contoso.com, il record DNS SRV seguente non funzionerà per la configurazione automatica, in quanto il dominio SIP dell'utente (contoso.com) corrisponde al dominio del pool Front End di configurazione automatica:
    
     \_sipinternaltls.\_tcp.contoso.com. 86400 IN SRV 0 0 5061 pool01.contoso.com

  - Se un utente esegue l'accesso come alice@fabrikam.com, il record DNS SRV seguente funzionerà per la configurazione automatica nel secondo dominio SIP.
    
     \_sipinternaltls.\_tcp.fabrikam.com. 86400 IN SRV 0 0 5061 pool01.fabrikam.com

A scopo di confronto, se un utente esegue l'accesso come tim@litwareinc.com, il record DNS SRV seguente non funzionerà per la configurazione automatica, in quanto il dominio SIP del client (litwareinc.com) non corrisponde al dominio in cui si trova il pool (fabrikam.com):

 \_sipinternaltls.\_tcp.litwareinc.com. 86400 IN SRV 0 0 5061 pool01.fabrikam.com

Se è necessaria la configurazione automatica per i client che eseguono Lync, selezionare una delle opzioni seguenti:

  - **Oggetti Criteri di gruppo**   Utilizzare gli oggetti Criteri di gruppo (GPO) per popolare il server con i valori corretti.
    

    > [!NOTE]
    > Questa opzione non abilita la configurazione automatica, ma automatizza il processo di configurazione manuale, dunque se si utilizza questo approccio i record SRV associati alla configurazione automatica non sono necessari.



  - **Zona interna corrispondente**   Creare nel DNS interno una zona corrispondente al DNS esterno (ad esempio, contoso.com) e creare record A e AAAA (se si usa l'assegnazione indirizzi IPv6) DNS corrispondenti al pool Lync Server 2013 usato per la configurazione automatica. Se ad esempio un utente è ospitato in pool01.contoso.net, ma accede a Lync come bob@contoso.com, creare una zona DNS interna denominata contoso.com e al suo interno creare un record A e AAAA (se si usa l'assegnazione indirizzi IPv6) DNS per pool01.contoso.com.

  - **Zona interna dedicata**   Se la creazione di un'intera zona nel DNS interno non rappresenta una scelta appropriata, è possibile creare zone dedicate che corrispondono ai record SRV necessari per la configurazione automatica e quindi popolarle utilizzando dnscmd.exe. Dnscmd.exe è necessario perché l'interfaccia utente DNS non supporta la creazione di zone dedicate. Ad esempio, se il dominio SIP è contoso.com ed è presente un pool Front End denominato pool01 che contiene due Front End Server, nel DNS interno saranno necessarie le zone dedicate e i record A seguenti:
    
        dnscmd . /zoneadd _sipinternaltls._tcp.contoso.com. /dsprimary
        dnscmd . /recordadd _sipinternaltls._tcp.contoso.com. @ SRV 0 0 5061 pool01.contoso.com.
        dnscmd . /zoneadd pool01.contoso.com. /dsprimary
        dnscmd . /recordadd pool01.contoso.com. @ A 192.168.10.90
        dnscmd . /recordadd pool01.contoso.com. @ AAAA <IPv6 address>
        dnscmd . /recordadd pool01.contoso.com. @ A 192.168.10.91 
        dnscmd . /recordadd pool01.contoso.com. @ AAAA <IPv6 address>
    
    Se l'ambiente contiene un secondo dominio SIP, ad esempio fabrikam.com, nel DNS interno saranno necessarie le zone dedicate e i record A seguenti:
    
        dnscmd . /zoneadd _sipinternaltls._tcp.fabrikam.com. /dsprimary
        dnscmd . /recordadd _sipinternaltls._tcp.fabrikam.com. @ SRV 0 0 5061 pool01.fabrikam.com.
        dnscmd . /zoneadd pool01.fabrikam.com. /dsprimary
        dnscmd . /recordadd pool01.fabrikam.com. @ A 192.168.10.90
        dnscmd . /recordadd pool01.contoso.com. @ AAAA <IPv6 address>
        dnscmd . /recordadd pool01.fabrikam.com. @ A 192.168.10.91
        dnscmd . /recordadd pool01.contoso.com. @ AAAA <IPv6 address>


> [!NOTE]
> Il nome di dominio completo del pool Front End appare due volte, ma con due indirizzi IP diversi. Questo avviene perché viene utilizzato il bilanciamento del carico DNS, ma se fosse utilizzato il bilanciamento del carico hardware sarebbe presente una sola voce per il pool Front End. Inoltre, i valori FQDN del pool Front End sono diversi tra l'esempio contoso.com e l'esempio fabrikam.com, ma gli indirizzi IP restano invariati. Questo avviene perché gli utenti che accedono da entrambi i domini SIP utilizzano lo stesso pool Front End per la configurazione automatica.



Per informazioni dettagliate, vedere l'articolo del blog DMTF relativo alla configurazione automatica di Communicator e DNS split-brain all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=200707](http://go.microsoft.com/fwlink/p/?linkid=200707).


> [!NOTE]
> Il contenuto di ogni blog e i relativi URL sono soggetti a modifiche senza preavviso.



## Configurazione del DNS (Domain Name System) per il ripristino di emergenza

Per configurare il DNS affinché reindirizzi il traffico Web di Lync Server 2013 ai siti di ripristino di emergenza e failover, è necessario usare un provider DNS che supporti GeoDNS. È possibile impostare i record DNS per il Web in modo che supportino il ripristino di emergenza, così che le funzionalità che usano i servizi Web continuino a funzionare anche in caso di disconnessione di un intero pool Front End. La funzionalità di ripristino di emergenza supporta gli URL semplici di Autodiscover (URL Lyncdiscover), Meet e Dial-In.

I record aggiuntivi dell'host DNS (A e AAAA se si usa IPv6) per la risoluzione interna ed esterna di servizi Web vengono definiti e configurati nel provider GeoDNS. Nei dettagli seguenti si presuppongo pool accoppiati, in località geografiche diverse e il supporto di GeoDNS da parte del provider con DNS round-robin o configurazione idonea all'uso di Pool1 come principale e Pool2 per il failover in caso di perdita di comunicazione o malfunzionamento hardware.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Record GeoDNS (esempio)</th>
<th>Record del pool (esempio)</th>
<th>Record CNAME (esempio)</th>
<th>Impostazioni DNS (selezionare un'opzione)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Meet-int.geolb.contoso.com</p></td>
<td><p>Pool1InternalWebFQDN.contoso.com</p>
<p>Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>Meet.contoso.com alias to Pool1InternalWebFQDN.contoso.com</p>
<p>Meet.contoso.com alias to Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>Round-robin tra pool</p>
<p>Utilizza il principale e connessione al secondario in caso di problemi</p></td>
</tr>
<tr class="even">
<td><p>Meet-ext.geolb.contoso.com</p></td>
<td><p>Pool1ExternalWebFQDN.contoso.com</p>
<p>Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>Alias Meet.contoso.com per Pool1ExternalWebFQDN.contoso.com</p>
<p>Alias Meet.contoso.com per Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>Round-robin tra pool</p>
<p>Utilizza il principale e connessione al secondario in caso di problemi</p></td>
</tr>
<tr class="odd">
<td><p>Dialin-int.geolb.contoso.com</p></td>
<td><p>Pool1InternalWebFQDN.contoso.com</p>
<p>Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>Alias Dialin.contoso.com per Pool1InternalWebFQDN.contoso.com</p>
<p>Alias Dialin.contoso.com per Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>Round-robin tra pool</p>
<p>Utilizza il principale e connessione al secondario in caso di problemi</p></td>
</tr>
<tr class="even">
<td><p>Dialin-ext.geolb.contoso.com</p></td>
<td><p>Pool1ExternalWebFQDN.contoso.com</p>
<p>Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>Alias Dialin.contoso.com per Pool1ExternalWebFQDN.contoso.com</p>
<p>Alias Dialin.contoso.com per Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>Round-robin tra pool</p>
<p>Utilizza il principale e connessione al secondario in caso di problemi</p></td>
</tr>
<tr class="odd">
<td><p>Lyncdiscoverint-int.geolb.contoso.com</p></td>
<td><p>Pool1InternalWebFQDN.contoso.com</p>
<p>Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>Alias Lyncdiscoverinternal.contoso.com per Pool1InternalWebFQDN.contoso.com</p>
<p>Alias Lyncdiscoverinternal.contoso.com per Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>Round-robin tra pool</p>
<p>Utilizza il principale e connessione al secondario in caso di problemi</p></td>
</tr>
<tr class="even">
<td><p>Lyncdiscover-ext.geolb.contoso.com</p></td>
<td><p>Pool1ExternalWebFQDN.contoso.com</p>
<p>Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>Lyncdiscover.contoso.com alias to Pool1ExternalWebFQDN.contoso.com</p>
<p>Alias Lyncdiscover.contoso.com per Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>Round-robin tra pool</p>
<p>Utilizza il principale e connessione al secondario in caso di problemi</p></td>
</tr>
<tr class="odd">
<td><p>Scheduler-int.geolb.contoso.com</p></td>
<td><p>Pool1InternalWebFQDN.contoso.com</p>
<p>Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>Alias Scheduler.contoso.com per Pool1InternalWebFQDN.contoso.com</p>
<p>Alias Scheduler.contoso.com per Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>Round-robin tra pool</p>
<p>Utilizza il principale e connessione al secondario in caso di problemi</p></td>
</tr>
<tr class="even">
<td><p>Scheduler-ext.geolb.contoso.com</p></td>
<td><p>Pool1ExternalWebFQDN.contoso.com</p>
<p>Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>Alias Scheduler.contoso.com per Pool1ExternalWebFQDN.contoso.com</p>
<p>Alias Scheduler.contoso.com per Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>Round-robin tra pool</p>
<p>Utilizza il principale e connessione al secondario in caso di problemi</p></td>
</tr>
</tbody>
</table>


## Bilanciamento del carico DNS

Il bilanciamento del carico DNS viene in genere implementato a livello di applicazione. L'applicazione, ad esempio un client che esegue Lync, tenta di connettersi a un server in un pool connettendosi a uno degli indirizzi IP restituiti dalla query sui record A e AAAA (se si usa l'assegnazione indirizzi IPv6) DNS per l'FQDN del pool.

Se ad esempio sono presenti tre Front End Server in un pool denominato pool01.contoso.com, accadrà quanto segue:

  - I client con Lync eseguono una query DNS per pool01.contoso.com. La query restituisce tre indirizzi IP che vengono memorizzati nella cache come segue, non necessariamente nell'ordine indicato:
    
    pool01.contoso.com      192.168.10.90
    
    pool01.contoso.com      192.168.10.91
    
    pool01.contoso.com      192.168.10.92

  - Il client tenta di stabilire una connessione TCP (Transmission Control Protocol) a uno degli indirizzi IP. Se la connessione ha esito negativo, il client tenta con l'indirizzo IP successivo nella cache.

  - Se la connessione TCP ha esito positivo, il client negozia TLS per connettersi al registrar principale su pool01.contoso.com.

  - Se il client tenta con tutte le voci memorizzate nella cache senza che sia possibile stabilire una connessione, l'utente riceve una notifica indicante che al momento non sono disponibili server che eseguono Lync Server 2013.


> [!NOTE]
> Il bilanciamento del carico basato su DNS è diverso dal DNS Round robin (DNS RR), che in genere fa riferimento al bilanciamento del carico con l'utilizzo di DNS per fornire un ordine diverso degli indirizzi IP corrispondenti ai server in un pool. Normalmente DNS RR abilita solo la distribuzione del carico, ma non il failover. Se ad esempio la connessione all'unico indirizzo IP fornito dalla query A e AAAA (se si usa l'assegnazione indirizzi IPv6) DNS non riesce, la connessione ha esito negativo. Il DNS Round robin è pertanto meno affidabile del bilanciamento del carico basato su DNS. È possibile utilizzare il DNS Round robin in combinazione con il bilanciamento del carico DNS.



Il bilanciamento del carico DNS viene utilizzato per:

  - Bilanciare il carico SIP tra server nei server perimetrali

  - Bilanciare il carico delle applicazioni dei servizi per applicazioni per comunicazioni unificate, ad esempio Operatore automatico conferenza, Response Group e Parcheggio di chiamata

  - Impedire nuove connessioni alle applicazioni dei servizi per applicazioni per comunicazioni unificate (noto anche come "svuotamento")

  - Bilanciare il carico di tutto il traffico client-server tra client e server perimetrali

Non è possibile utilizzare il bilanciamento del carico DNS per:

  - Traffico Web client-server ai server Director o Front End

Bilanciamento del carico DNS e traffico federato:

Se una query DNS SRV restituisce più record DNS, il servizio Access Edge Server seleziona sempre il record DNS SRV con la minore priorità numerica e il massimo peso numerico. Il documento IETF (Internet Engineering Task Force) "A DNS RR for specifying the location of services (DNS SRV)" <http://www.ietf.org/rfc/rfc2782.txt> specifica che se sono definiti più record SRV DNS, la priorità deve essere utilizzata prima del peso. Si supponga, ad esempio, che il record A SRV DNS abbia un peso 20 e una priorità 40 e che il record B SRV DNS abbia un peso 10 e una priorità 50. In questo caso verrebbe selezionato il record A SRV DNS con priorità 40. Per la selezione dei record SRV DNS si applicano le regole seguenti:

  - La priorità viene considerata per prima. Un client DEVE tentare di contattare l'host di destinazione definito dal record SRV DNS con la priorità minore raggiungibile. I tentativi per le destinazioni con la stessa priorità DEVONO essere eseguiti nell'ordine specificato dal campo del peso.

  - Il campo del peso specifica un peso relativo per le voci con la stessa priorità. Ai pesi maggiori DEVE essere assegnata una probabilità proporzionalmente maggiore di essere selezionati. Gli amministratori DNS DEVONO utilizzare il peso 0 quando non esiste alcuna selezione del server da eseguire. In presenza di record che contengono pesi maggiori di 0, i record con peso 0 dovrebbero avere una probabilità molto limitata di essere selezionati.

Se vengono restituiti più record DNS SRV con priorità e peso uguali, l'Access Edge Server selezionerà sempre il record SRV ricevuto per primo dal server DNS.

