---
title: "Lync Server 2013: Scenari per l'accesso degli utenti esterni"
TOCTitle: Scenari per l'accesso degli utenti esterni
ms:assetid: 25697446-b045-4d12-9b1c-47f694b4f224
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425727(v=OCS.15)
ms:contentKeyID: 49299951
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Scenari per l'accesso degli utenti esterni in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per garantire l'accesso utente esterno per  Lync Server 2013, è necessario distribuire almeno un server perimetrale e un proxy inverso nella rete perimetrale. Se si desidera, è possibile distribuire un Server Director o un pool di server Director nella rete interna.

Se si necessita di una capacità maggiore di quella offerta da un singolo server perimetrale o si desidera usufruire della disponibilità elevata per la distribuzione server perimetrale, è possibile configurare il bilanciamento del carico e distribuire più server perimetrali in un pool con bilanciamento del carico. Se nell'organizzazione sono presenti più data center, possono sussistere distribuzioni di server perimetrale o pool di server perimetrali in più posizioni. Solo una delle distribuzioni di server perimetrale tuttavia può essere designata come route di federazione.

In questa sezione vengono definiti scenari per le distribuzioni di server perimetrale e le sezioni di pianificazione vengono associate ai possibili scenari. Ad esempio se la distribuzione richiede disponibilità elevata, federazione con contatti XMPP (Extensible Messaging and Presence Protocol) e mobilità Lync, è opportuno selezionare le voci corrispondenti nella tabella seguente che potrebbero soddisfare i requisiti e utilizzare le sezioni di pianificazione per definire la distribuzione, come illustrato nel diagramma di flusso seguente.

**Processo di selezione degli scenari di distribuzione di server perimetrali**

![Esempio di diagramma di flusso della distribuzione](images/Gg425727.007100b5-6923-4909-bfd7-897d8867205f(OCS.15).jpg "Esempio di diagramma di flusso della distribuzione")

Attraverso questo processo è possibile pianificare e documentare la configurazione di tutte le funzionalità potenziali che si intende distribuire agli utenti. È tuttavia possibile aggiungere servizi di federazione e Mobility dopo la distribuzione del server perimetrale e confermare la correttezza dell'operazione prima di aggiungere altre funzionalità. Il processo di aggiunta di funzionalità a una distribuzione di server perimetrale esistente è trattato nella sezione Distribuzione. Per informazioni sulla distribuzione, vedere [Distribuzione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-deploying-external-user-access.md). Se si include la pianificazione per queste funzionalità durante il processo di pianificazione iniziale, è possibile preparare i requisiti di DNS, firewall e certificati per le funzionalità aggiunte, per acquisire i certificati e configurare i requisiti di DNS e porte/protocolli in anticipo.

> [!TIP]  
> Se si intende pianificare l'installazione di server perimetrali e proxy inverso e aggiungere funzionalità successivamente (ad esempio federazione e Mobility), determinare quali certificati saranno necessari per tutti i servizi dopo la distribuzione. La pianificazione e l'acquisizione dei certificati per tutte le funzionalità in anticipo, che vengano o meno distribuite inizialmente, evita di dover ordinare nuovi certificati per soddisfare i requisiti di federazione (nei server perimetrali) o del proxy inverso (per i servizi Mobility).


> [!NOTE]
> Tutti i servizi perimetrali vengono eseguiti in ogni server perimetrale. Non è possibile dividere i servizi tra due server perimetrali diversi. Se si distribuisce un pool di server perimetrali per la scalabilità, tutti i servizi perimetrali vengono distribuiti in ogni server perimetrale del pool. La federazione XMPP, la federazione Office Communications Server e Lync Server, la connettività per messaggistica istantanea pubblica e mobilità client sono servizi aggiuntivi che è possibile distribuire dopo avere distribuito prima il server perimetrale o il pool di server perimetrali. I servizi Mobility sono una funzionalità che utilizza il proxy inverso. L'installazione di servizi Mobility non aggiunge funzionalità al server perimetrali, ma richiede la riconfigurazione del proxy inverso. Nella colonna <STRONG>Obiettivo dell'installazione</STRONG> in cui sono elencate queste funzionalità vengono fornite linee guida di pianificazione nella colonna associata in <STRONG>Sezione o sezioni per la pianificazione del server perimetrale</STRONG> per la pianificazione concorrente di queste funzionalità da distribuire dopo l'installazione e la configurazione dei server perimetrali.



## Identificazione e associazione degli obiettivi di pianificazione


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Obiettivo dell'installazione</th>
<th>Documentazione relativa alla pianificazione del server perimetrale</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Si è deciso che un solo server sia sufficiente per i servizi perimetrali nell'infrastruttura. Si intende inoltre utilizzare indirizzi IP privati per le interfacce esterne dei server perimetrali con NAT su Internet.</p>
<p>Utilizzare questa sezione di pianificazione se si distribuisce un solo server perimetrale nel perimetro. Si distribuirà un server perimetrale con indirizzi IP privati al server perimetrale e si utilizzerà NAT per fornire indirizzi IP pubblici per gli utenti esterni in Internet.</p></td>
<td><p><a href="lync-server-2013-single-consolidated-edge-with-private-ip-addresses-and-nat.md">Singola topologia perimetrale consolidata con indirizzi IP privati e NAT in Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p>Si è deciso che un solo server sia sufficiente per i servizi perimetrali nell'infrastruttura. Si intende inoltre utilizzare indirizzi IP pubblici per le interfacce esterne dei server perimetrali su Internet.</p>
<p>Utilizzare questa sezione di pianificazione se si distribuisce un solo server perimetrale nel perimetro. Si distribuirà un server perimetrale con indirizzi IP pubblici assegnati al server perimetrale. Anziché NAT, in questo scenario si utilizzerà il routing. L'indirizzo IP pubblico effettivo del server perimetrale è reso disponibile per le connessioni utente esterne.</p></td>
<td><p><a href="lync-server-2013-single-consolidated-edge-with-public-ip-addresses.md">Singola topologia perimetrale consolidata con indirizzi IP pubblici in Lync Server 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>Si è deciso che l'elevata disponibilità dei servizi perimetrali è importante per gli utenti e si distribuiranno due o più server perimetrali nel pool. Si intende inoltre utilizzare indirizzi IP privati per le interfacce esterne dei server perimetrali con NAT su Internet.</p>
<p>Utilizzare questa sezione di pianificazione se si distribuisce un pool di server perimetrali nel perimetro. Si distribuiranno i server perimetrali con indirizzi IP privati assegnati al server perimetrale, utilizzando il bilanciamento del carico DNS per distribuire la comunicazione nel pool. Si utilizzerà NAT per fornire indirizzi IP pubblici per gli utenti esterni in Internet.</p></td>
<td><p><a href="lync-server-2013-scaled-consolidated-edge-dns-load-balancing-with-private-ip-addresses-using-nat.md">Topologia perimetrale consolidata con scalabilità implementata, bilanciamento del carico DNS con indirizzi IP privati tramite NAT in Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p>Si è deciso che l'elevata disponibilità dei servizi perimetrali è importante per gli utenti e si distribuiranno due o più server perimetrali nel pool. Si intende inoltre utilizzare indirizzi IP pubblici per le interfacce esterne dei server perimetrale su Internet.</p>
<p>Utilizzare questa sezione di pianificazione se si distribuisce un pool di server perimetrali nel perimetro. Si distribuiranno i server perimetrali con indirizzi IP pubblici assegnati al server perimetrale, utilizzando il bilanciamento del carico DNS per distribuire la comunicazione nel pool. Anziché NAT, si utilizzerà il routing per fornire indirizzi IP pubblici per gli utenti esterni in Internet.</p></td>
<td><p><a href="lync-server-2013-scaled-consolidated-edge-dns-load-balancing-with-public-ip-addresses.md">Topologia perimetrale consolidata con scalabilità implementata, bilanciamento del carico DNS con indirizzi IP pubblici in Lync Server 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>Si è deciso che l'elevata disponibilità dei servizi perimetrali è importante per gli utenti e si distribuiranno due o più server perimetrali nel pool tramite un servizio di bilanciamento del carico hardware.</p>
<p>Utilizzare questa sezione di pianificazione se si distribuisce un pool di server perimetrali nel perimetro. Si distribuiranno i server perimetrali con indirizzi IP pubblici assegnati al server perimetrale, utilizzando servizi di bilanciamento del carico hardware per distribuire la comunicazione nel pool. Anziché NAT, si utilizzerà il routing per fornire indirizzi IP pubblici per gli utenti esterni in Internet.</p></td>
<td><p><a href="lync-server-2013-scaled-consolidated-edge-with-hardware-load-balancers.md">Topologia perimetrale consolidata con scalabilità implementata e servizi di bilanciamento del carico hardware in Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p>Gli scenari di federazione consentono di pianificare la funzionalità per estendere i tipi di partner con cui possono comunicare gli utenti.</p><ul><li><p>Federazione Lync Server</p></li><li><p>Federazione Office Communications Server</p></li><li><p>Connettività per messaggistica istantanea pubblica</p></li><li><p>Federazione XMPP</p></li></ul></td>
<td><p>Pianificazione per gli scenari di federazione</p><ul><li><p><a href="lync-server-2013-planning-for-lync-server-and-office-communications-server-federation.md">Pianificazione della federazione di Lync Server e Office Communications Server</a></p></li><li><p><a href="lync-server-2013-planning-for-public-instant-messaging-connectivity.md">Pianificazione della connettività per messaggistica istantanea pubblica</a></p></li><li><p><a href="lync-server-2013-planning-for-extensible-messaging-and-presence-protocol-xmpp-federation.md">Pianificazione per la federazione di XMPP (Extensible Messaging and Presence Protocol) in Lync Server 2013</a></p></li></ul></td>
</tr>
<tr class="odd">
<td><p>I servizi Mobility vengono offerti tramite il proxy inverso. I servizi che abilitano la mobilità per gli utenti esterni sono distribuiti nel Front End Server o nel pool Front End. Per abilitare i servizi Mobility per gli utenti esterni, creare regole di pubblicazione o modificare quelle esistenti nel proxy inverso.</p></td>
<td><p><a href="lync-server-2013-planning-for-mobility.md">Pianificazione della versione per dispositivi mobili in Lync Server 2013</a></p></td>
</tr>
</tbody>
</table>


> [!TIP]  
> Nelle sezioni Scenari di seguito sono illustrate architetture di riferimento, esempi di DNS, definizioni di porte/protocolli e requisiti di certificati. Sono inoltre inclusi diagrammi per esigenze relative a DNS, definizioni di porte/protocolli e certificati. I diagrammi offrono un modello da compilare e distribuire ad altri team (ad esempio il team di rete, il team di infrastruttura di chiave pubblica e il team di distribuzione server dell'organizzazione). I diagrammi hanno l'obiettivo di migliorare le comunicazioni e garantire che gli elementi di configurazione obbligatori del server perimetrale vengano illustrati in modo efficiente ai responsabili della configurazione. Si consiglia di utilizzare i diagrammi e le architetture di riferimento associate per pianificare la distribuzione.
