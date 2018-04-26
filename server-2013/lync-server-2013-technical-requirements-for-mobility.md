---
title: 'Lync Server 2013: Requisiti tecnici per i dispositivi mobili'
TOCTitle: Requisiti tecnici per i dispositivi mobili
ms:assetid: 831be681-4de0-4e42-b04f-8879ca4dcd23
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690030(v=OCS.15)
ms:contentKeyID: 49301171
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti tecnici per i dispositivi mobili in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-07-24_

    Some information in this topic pertains to Cumulative Updates for Lync Server 2013: February 2013.

Gli utenti di dispositivi mobili hanno a che fare con diversi scenari di applicazioni per dispositivi mobili che richiedono una pianificazione speciale. Un utente potrebbe, ad esempio, iniziare a utilizzare un'applicazione per dispositivi mobili mentre si trova fuori ufficio, connettendosi attraverso la rete 3G, quindi passare alla rete Wi-Fi aziendale quando arriva al lavoro e infine passare di nuovo alla rete 3G all'uscita dell'edificio. È necessario pianificare l'ambiente per supportare tali transizioni di rete e garantire un'esperienza utente coerente. In questa sezione vengono descritti i requisiti dell'infrastruttura necessari per supportare le applicazioni per dispositivi mobili e l'individuazione automatica delle risorse per dispositivi mobili.


> [!NOTE]
> Sebbene le applicazioni per dispositivi mobili siano in grado di connettersi anche ad altri servizi di Lync Server 2013, questo requisito di invio di tutte le richieste Web di applicazioni per dispositivi mobili allo stesso nome di dominio completo (FQDN) Web esterno si applica solo al servizio Mobility di Lync Server 2013. Altri servizi per dispositivi mobili non richiedono questa configurazione.



I requisiti di affinità dei cookie nei servizi di bilanciamento del carico hardware è sostanzialmente ridotta e si sostituisce l'affinità TCP (Transmission Control Protocol) se si utilizza Lync Mobile di Lync Server 2013. È sempre possibile utilizzare l'affinità dei cookie, ma non sarà più richiesta dai servizi Web.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Tutto il traffico dei servizi per dispositivi mobili passa attraverso il proxy inverso, indipendentemente dalla posizione del punto di origine, interna o esterna. Nel caso di un singolo proxy inverso o di una farm di proxy inversi oppure di un dispositivo che fornisce le funzioni di proxy inverso, può verificarsi un problema quando il traffico interno esce attraverso un'interfaccia e tenta immediatamente l'ingresso sulla stessa interfaccia. Ciò causa spesso una violazione delle regole di sicurezza nota come spoofing di pacchetti TCP o semplicemente spoofing. L'<em>hairpinning</em> (ovvero l'uscita e l'ingresso immediato di un pacchetto o di una serie di pacchetti) deve essere consentito per supportare le funzionalità per dispositivi mobili. Uno dei modi per risolvere questo problema consiste nell'utilizzare un proxy inverso separato dal firewall (per motivi di sicurezza, nel firewall dovrebbe essere sempre applicata la regola per la prevenzione dello spoofing). Il fenomeno dell'hairpinning può verificarsi sull'interfaccia esterna del proxy inverso anziché sull'interfaccia esterna del firewall. Lo spoofing viene rilevato nel firewall e la regola può essere evitata nel proxy inverso, consentendo così l'hairpinning necessario per le funzionalità per dispositivi mobili.<br />
Se possibile, utilizzare record host o CNAME DNS (Domain Name System), e non il firewall, per definire il proxy inverso in relazione al comportamento di hairpinning.</td>
</tr>
</tbody>
</table>


Lync Server 2013 supporta i servizi per dispositivi mobili per i client mobili di Lync 2010 Mobile e Lync 2013. Entrambi i client utilizzano il servizio di individuazione automatica di Lync Server 2013 per trovare il punto di ingresso per i dispositivi mobili, ma utilizzano servizi per dispositivi mobili diversi. Lync 2010 Mobile utilizza il servizio Mobility noto come *Mcx* , introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011. I client mobili di Lync 2013 utilizzano l'API Web Unified Communications, o *UCWA* , come provider di servizi per dispositivi mobili.

## Configurazione DNS interna e esterna

I servizi Mobility Mcx (introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011) e UCWA (introdotto negli aggiornamenti cumulativi per Lync Server 2013 di febbraio 2013) utilizzano DNS nello stesso modo.

Quando si utilizza l'individuazione automatica, i dispositivi mobili utilizzano il sistema DNS per individuare le risorse. Durante la ricerca DNS viene innanzitutto tentata una connessione al nome di dominio completo (FQDN) associato al record DNS interno, ovvero lyncdiscoverinternal. *\<internal domain name\>*. Se non è possibile stabilire una connessione utilizzando il record DNS interno, viene eseguito un tentativo di connessione tramite il record DNS esterno, ovvero lyncdiscover.*\<sipdomain\>*. Un dispositivo mobile interno alla rete si connette all'URL interno del servizio di individuazione automatica, mentre un dispositivo mobile esterno alla rete si connette all'URL esterno del servizio di individuazione automatica. Le richieste di individuazione automatica esterne passano attraverso il proxy inverso. Il servizio di individuazione automatica di Lync Server 2013 restituisce tutti gli URL dei servizi Web per il pool principale dell'utente, inclusi gli URL dei servizi Mobility (Mcx e UCWA). Sia l'URL interno che quello esterno del servizio Mobility, tuttavia, sono associati al nome FQDN dei servizi Web esterni. Per questo motivo, sia che sia interno o esterno alla rete, un dispositivo mobile si connette al servizio Mobility di Lync Server 2013 esternamente, tramite il proxy inverso.


> [!NOTE]
> È importante tenere presente che una distribuzione può consistere di più spazi dei nomi distinti, per uso interno ed esterno. Il nome di dominio SIP può differire dal nome di dominio della distribuzione interna. Ad esempio, il nome di dominio SIP potrebbe essere <STRONG>contoso.com</STRONG>, mentre quello della distribuzione interna potrebbe essere <STRONG>contoso.net</STRONG>. Gli utenti che accedono a Lync Server utilizzeranno il nome di dominio SIP, ad esempio <STRONG>luca@contoso.com</STRONG>. Per l'indirizzamento ai servizi Web esterni (definiti in Generatore di topologie come <STRONG>Servizi Web esterni</STRONG>), il nome di dominio e il nome di dominio SIP saranno coerenti a quanto definito nel DNS. Per l'indirizzamento ai servizi Web interni (definiti in Generatore di topologie come <STRONG>Servizi Web interni</STRONG>), il nome predefinito dei servizi Web interni sarà il nome FQDN del Front End Server, pool Front End, Server Director o pool di server Director. È possibile sovrascrivere il nome dei servizi Web interni. È necessario utilizzare il nome di dominio interno (e non il nome di dominio SIP) per i servizi Web interni, e definire il record host A (o, per IPv6, AAAA) DNS in modo che corrisponda al nome sovrascritto. Ad esempio, l'FQDN predefinito dei servizi Web interni potrebbe essere <STRONG>pool01.contoso.net</STRONG>. Un FQDN sovrascritto dei servizi Web interni potrebbe essere <STRONG>webpool.contoso.net</STRONG>. Una simile definizione dei servizi Web contribuisce ad assicurarsi che venga rispettata la località interna o esterna dei servizi e non la località dell'utente che li utilizza.<BR>Tuttavia, poiché i servizi Web sono definiti in Generatore di topologie e il nome di questi può essere sostituito, a condizione che siano coerenti il nuovo nome dei servizi Web, il certificato che convalida questo nome e i record DNS che lo definiscono, è possibile utilizzare qualsiasi nome di dominio per definire i servizi Web interni, incluso il nome del dominio SIP. La risoluzione del nome in indirizzo IP è determinata dai record host DNS e da uno spazio dei nomi coerente.<BR>Ai fini di questo argomento e degli esempi in esso contenuti, per l'illustrazione della topologia e delle definizioni DNS viene utilizzato il nome di dominio interno.



Nel diagramma seguente è illustrato il flusso di richieste Web di applicazioni per dispositivi mobili per il servizio Mobility e il servizio di individuazione automatica quando si utilizza una configurazione DNS interna e esterna.

**Flusso del servizio Mobility quando si utilizza l'individuazione automatica**

![Flusso delle richieste per il servizio Mobility](images/Hh690030.cdb96424-96f2-4abf-88d7-1d32d1010ffd(OCS.15).jpg "Flusso delle richieste per il servizio Mobility")


> [!NOTE]
> Il diagramma illustra servizi Web generici. Una directory virtuale denominata Mobility illustra i servizi Mobility Mcx e/o UCWA. Se non sono stati installati gli aggiornamenti cumulativi per Lync Server 2013 di febbraio 2013, è possibile che la directory virtuale Ucwa sia o non sia stata definita nei servizi Web interni ed esterni. Sarà disponibile una directory virtuale Autodiscover e potrebbe esistere una directory virtuale Mcx.<BR>L'individuazione automatica e l'individuazione dei servizi funzionano allo stesso modo, indipendentemente dalla tecnologia per i servizi per dispositivi mobili distribuita.



Per supportare gli utenti mobili sia all'interno che all'esterno della rete aziendale, i nomi FQDN Web interni ed esterni devono soddisfare alcuni requisiti. È inoltre necessario che vengano soddisfatti altri requisiti, a seconda delle caratteristiche che si sceglie di implementare:

  - Nuovi record DNS CNAME o A (host AAAA, se IPv6), per l'individuazione automatica.

  - Nuova regola del firewall, se si desidera supportare le notifiche push tramite la rete Wi-Fi.

  - Nomi alternativi soggetto nei certificati server interni e nei certificati proxy inverso, per l'individuazione automatica.

  - Modifiche alla configurazione del servizio di bilanciamento del carico hardware di Front End Server per l'affinità dell'origine.

La topologia deve soddisfare i requisiti seguenti per supportare il servizio Mobility e quello di individuazione automatica:

  - Il nome FQDN Web interno di pool Front End deve essere diverso dal nome FQDN Web esterno di pool Front End.

  - Il nome FQDN Web interno deve essere risolto solo all'interno della rete aziendale ed essere accessibile solo da tale posizione.

  - Il nome FQDN Web esterno deve essere risolto solo in Internet ed essere accessibile solo da tale posizione.

  - Per un utente che si trova all'interno della rete aziendale, l'URL del servizio per dispositivi mobili deve essere indirizzato al nome FQDN Web esterno. Questo requisito riguarda il servizio per dispositivi mobili e si applica solo a questo URL.

  - Per un utente che si trova fuori dalla rete aziendale, la richiesta deve essere indirizzata al nome FQDN Web esterno del pool Front End o del Server Director.

Se l'individuazione automatica è supportata, è necessario creare i record DNS seguenti per ogni dominio SIP:

  - Un record DNS interno per supportare gli utenti mobili che si connettono dall'interno della rete dell'organizzazione.

  - Un record DNS esterno, o pubblico, per supportare gli utenti mobili che si connettono da Internet.

L'URL interno di individuazione automatica non deve essere raggiungibile dall'esterno della rete. L'URL esterno di individuazione automatica non deve essere raggiungibile dall'interno della rete. Se tuttavia non è possibile soddisfare questo requisito per l'URL esterno, ciò non avrà probabilmente effetto sulle funzionalità dei client mobili, in quanto viene sempre eseguito prima un tentativo di utilizzare l'URL interno.

I record DNS possono essere di tipo CNAME o A (l'host, se IPv6, è AAAA).


> [!NOTE]
> I client dei dispositivi mobili non supportano certificati SSL (Secure Sockets Layer) multipli da domini diversi. Di conseguenza, il reindirizzamento CNAME a domini diversi non è supportato in HTTPS. Ad esempio, un record CNAME DNS per lyncdiscover.contoso.com che esegue il reindirizzamento a un indirizzo director.contoso.net non è supportato in HTTPS. In una topologia di questo tipo, un client di dispositivo portatile deve utilizzare il protocollo HTTP per la prima richiesta, in modo che il reindirizzamento CNAME venga risolto in HTTP. Per le richieste successive viene quindi utilizzato HTTPS. Per supportare questo scenario, è necessario configurare il proxy inverso con una regola di pubblicazione Web per la porta 80 (HTTP). Per ulteriori informazioni, vedere la sezione relativa alla creazione di una regola di pubblicazione Web per la porta 80, in <A href="lync-server-2013-configuring-the-reverse-proxy-for-mobility.md">Configurazione del proxy inverso per i dispositivi mobili in Lync Server 2013</A>.<BR>Il reindirizzamento CNAME allo stesso dominio è supportato su HTTPS. In questo caso, il certificato del dominio di destinazione copre il dominio di origine.



Per informazioni dettagliate sui record DNS necessari per lo scenario, vedere [Riepilogo DNS - Individuazione automatica in Lync Server 2013](lync-server-2013-dns-summary-autodiscover.md).

## Requisiti relativi a porte e firewall

Se si supportano le notifiche push e si desidera che i dispositivi mobili Apple possano ricevere le notifiche push tramite la rete Wi-Fi, è necessario anche aprire la porta 5223 nella rete Wi-Fi aziendale. La porta 5223 è una porta TCP in uscita utilizzata dal servizio di notifica Push Apple. Questa connessione può essere avviata dal dispositivo mobile. Per informazioni dettagliate, vedere [http://support.apple.com/kb/TS1629](http://support.apple.com/kb/ts1629?viewlocale=it_it).


> [!WARNING]
> Le notifiche push non sono necessarie per un dispositivo Apple che utilizza il client mobile Lync 2013.



Se un utente è ospitato in un Survivable Branch Appliance (SBA), sono necessarie le seguenti porte:

  - UcwaSipExternalListeningPort richiede la porta 5088

  - UcwaSipPrimaryListeningPort richiede la porta 5089

Per ulteriori dettagli e istruzioni sui requisiti di porte e protocolli per l'individuazione automatica, vedere [Riepilogo porte - Individuazione automatica in Lync Server 2013](lync-server-2013-port-summary-autodiscover.md).

## Requisiti relativi ai certificati

Se si supporta l'individuazione automatica per i client mobili Lync è necessario modificare gli elenchi dei nomi alternativi soggetto dei certificati per supportare le connessioni sicure dai client mobili. È necessario richiedere e assegnare nuovi certificati, aggiungendo le voci dei nomi alternativi soggetto descritte in questa sezione per ogni Front End Server e Server Director in cui viene eseguito il servizio di individuazione automatica. L'approccio consigliato prevede inoltre la modifica anche degli elenchi dei nomi alternativi soggetto dei certificati per i proxy inversi. È necessario aggiungere voci di nomi alternativi soggetto per ogni dominio SIP dell'organizzazione.

La riemissione di certificati utilizzando un'Autorità di certificazione interna è in genere un processo semplice, ma l'aggiunta di più voci di nomi alternativi soggetto ai certificati pubblici utilizzati dal proxy inverso può essere un'operazione dispendiosa. Se sono presenti molti domini SIP, e pertanto l'aggiunta di nomi alternativi soggetto è molto dispendiosa, è possibile configurare il proxy inverso per effettuare la richiesta iniziale al servizio di individuazione automatica tramite la porta 80 utilizzando il protocollo HTTP, anziché la porta 443 utilizzando il protocollo HTTPS (configurazione predefinita). La richiesta viene quindi reindirizzata alla porta 8080 nel Server Director o nel pool Front End. Quando si pubblica la richiesta iniziale al servizio di individuazione automatica nella porta 80, non è necessario modificare i certificati per il proxy inverso, in quanto per la richiesta viene utilizzato HTTP anziché HTTPS. Questo approccio è supportato ma non consigliato.

## Requisiti relativi a IIS (Internet Information Services)

Per i dispositivi mobili è consigliabile utilizzare IIS 7.5, IIS 8.0 o IIS 8.5. Tramite il programma di installazione del servizio Mobility vengono impostati alcuni flag ASP.NET per migliorare le prestazioni. IIS 7.5 viene installato per impostazione predefinita in Windows Server 2008 R2, IIS 8.0 viene installato in Windows Server 2012 e IIS 8.5 viene installato in Windows Server 2012 R2. Le impostazioni ASP.NET vengono modificate automaticamente dal programma di installazione del servizio Mobility.

## Requisiti relativi al servizio di bilanciamento del carico hardware

Nel servizio di bilanciamento del carico hardware che supporta il pool Front End, gli indirizzi IP virtuali (VIP, Virtual IP) esterni dei servizi Web per il traffico dei servizi Web devono essere configurati per l'origine. L'affinità dell'origine è utile per assicurarsi che più connessioni da un unico client vengano inviate a un server per mantenere lo stato di sessione. Per informazioni dettagliate sui requisiti di affinità, vedere [Requisiti per il bilanciamento del carico per Lync Server 2013](lync-server-2013-load-balancing-requirements.md).

Se si prevede di supportare i client mobili Lync solo nella rete Wi-Fi interna, è necessario configurare gli indirizzi IP virtuali dei servizi Web interni per l'indirizzo di origine, come descritto per gli indirizzi IP virtuali dei servizi Web esterni. In questo caso, utilizzare la persistenza dell'indirizzo di origine (o TCP) per gli indirizzi IP virtuali dei servizi Web interni nel servizio di bilanciamento del carico hardware. Per informazioni dettagliate, vedere [Requisiti per il bilanciamento del carico per Lync Server 2013](lync-server-2013-load-balancing-requirements.md).

## Requisiti relativi al proxy inverso

Se si supporta l'individuazione automatica per i client mobili Lync è necessario aggiornare la regola corrente di pubblicazione Web come indicato di seguito:

  - Se si decide di aggiornare gli elenchi dei nomi alternativi soggetto nei certificati del proxy inverso e di utilizzare HTTPS per la richiesta iniziale al servizio di individuazione automatica, è necessario aggiornare la regola di pubblicazione Web per lyncdiscover.*\<sipdomain\>*. Solitamente questa è associata alla regola di pubblicazione per l'URL esterno dei servizi Web nel pool Front End.

  - Se si decide di utilizzare HTTP per la richiesta iniziale al servizio di individuazione automatica in modo che non sia necessario aggiornare l'elenco di nomi alternativi soggetto nei certificati del proxy inverso, è necessario creare una nuova regola di pubblicazione Web per la porta HTTP/TCP 80, se tale regola non esiste già. Se, invece, una regola per la porta HTTP/TCP 80 esiste già, è possibile aggiornarla per includere la voce lyncdiscover.*\<sipdomain\>*.

