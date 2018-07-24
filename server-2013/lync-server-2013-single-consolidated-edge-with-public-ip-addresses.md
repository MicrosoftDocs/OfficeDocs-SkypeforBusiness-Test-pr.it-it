---
title: 'Lync Server 2013: Singola topologia perimetrale consolidata con indirizzi IP pubblici'
TOCTitle: Singola topologia perimetrale consolidata con indirizzi IP pubblici
ms:assetid: a92d1179-6a1f-4efe-908a-f8dfc5024f30
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205148(v=OCS.15)
ms:contentKeyID: 49301606
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Singola topologia perimetrale consolidata con indirizzi IP pubblici in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-08_

Se nell'organizzazione è necessario il supporto di meno di 15.000 connessioni client al servizio Access Edge, 1.000 connessioni client attive al servizio Web Conferencing di Lync Server e 500 sessioni A/V Edge contemporanee e se non è importante garantire la disponibilità elevata del server perimetrale, questa topologia offre come vantaggi costi hardware inferiori e una distribuzione più semplice. Se si desidera una maggiore capacità o disponibilità, è consigliabile distribuire una topologia di server perimetrale consolidata con scalabilità implementata.

  -   
    [Topologia perimetrale consolidata con scalabilità implementata, bilanciamento del carico DNS con indirizzi IP privati tramite NAT in Lync Server 2013](lync-server-2013-scaled-consolidated-edge-dns-load-balancing-with-private-ip-addresses-using-nat.md)

  -   
    [Topologia perimetrale consolidata con scalabilità implementata, bilanciamento del carico DNS con indirizzi IP pubblici in Lync Server 2013](lync-server-2013-scaled-consolidated-edge-dns-load-balancing-with-public-ip-addresses.md)

  -   
    [Topologia perimetrale consolidata con scalabilità implementata e servizi di bilanciamento del carico hardware in Lync Server 2013](lync-server-2013-scaled-consolidated-edge-with-hardware-load-balancers.md)

> [!important]  
> Quando viene utilizzato l'indirizzo IP pubblico nel server perimetrale, il gateway predefinito nel server perimetrale non è più il firewall o il router locale, ma il router o il firewall del perimetro pubblico, che sarà un indirizzo pubblico. Il proxy inverso continua a utilizzare il router o il firewall associato alla rete perimetrale più esterna. La differenza tra il proxy inverso e il server perimetrale con gli indirizzi IP pubblici è costituita dal fatto che il proxy inverso utilizza ancora la conversione NAT mentre il server perimetrale utilizza una relazione di route.

La figura non mostra i Director, ovvero un ruolo server facoltativo distribuito nella rete interna tra il server perimetrali e il pool Front End o il server. Per informazioni dettagliate sulla topologia per i Director, vedere [Componenti richiesti per il server Director in Lync Server 2013](lync-server-2013-components-required-for-the-director.md). Nella figura è rappresentato un singolo proxy inverso.


> [!NOTE]
> La figura è disponibile a titolo orientativo e per fornire un esempio di indirizzamento IP, ma non intende rappresentare i flussi di comunicazione effettivi con il corretto traffico in arrivo e in uscita. La figura rappresenta un quadro di alto livello del traffico possibile. I dettagli del flusso di traffico in arrivo (verso le porte di attesa) e in uscita (verso i server o i client di destinazione) sono rappresentati nel diagramma di riepilogo delle porte in ogni scenario. La porta TCP 443, ad esempio, è in effetti solo per il traffico in arrivo (destinato al server perimetrale o al proxy inverso) e rappresenta esclusivamente un flusso bidirezionale dalla prospettiva del protocollo (TCP). La figura illustra inoltre la variazione del tipo di traffico in presenza di NAT (Network Address Translation), ovvero l'indirizzo di destinazione diventa in arrivo e quello di origine in uscita. Il firewall esterno ed interno e le interfacce del server di esempio sono illustrati solo a scopo di riferimento. Sono infine visualizzati il gateway predefinito e le relazioni di route, nei casi appropriati. Si noti inoltre che il diagramma utilizza la zona DNS <EM>.com</EM> per rappresentare la zona DNS esterna sia per il proxy inverso che per i server perimetrali, e la zona DNS <EM>.net</EM> fa riferimento alla zona DNS interna.



Una novità di Microsoft Lync Server 2013 è il supporto dell'indirizzamento IPv6. In modo molto simile all'indirizzamento IPv4, gli indirizzi IPv6 devono essere assegnati in modo che gli indirizzi facciano parte dello spazio di indirizzi IPv6 assegnato. Gli indirizzi indicati in questo argomento sono solo a titolo di esempio. È necessario acquisire indirizzi IPv6 adatti alla distribuzione e specificare l'ambito corretto per ottenere l'interoperabilità con i meccanismi di indirizzamento interno ed esterno. Windows Server offre una funzionalità importante per il funzionamento transitorio di IPv6 e per la comunicazione tra IPv4 e IPv6 nota come *dual stack* . Dual stack è uno stack di rete separato e distinto per IPv4 e IPv6 che consente l'assegnazione simultanea di indirizzi IPv4 e IPv6, oltre a consentire al server di comunicare con altri host e client in base agli specifici requisiti.

I tipi di indirizzo tipici che verranno utilizzati per l'indirizzamento IPv6 sono gli indirizzi globali IPv6 (simili agli indirizzi pubblici IPv4), gli indirizzi locali univoci IPv6 (simili agli intervalli di indirizzi privati IPv4) e gli indirizzi locali rispetto al collegamento IPv6 (simili agli indirizzi IP privati automatici in Windows Server per IPv4)

Esistono tecnologie di conversione degli indirizzi di rete (NAT) per IPv6 che supportano conversioni NAT da IPv6 a IPv4 (comunemente nota come NAT64) e NAT da IPv6 a IPv6 (comunemente nota come NAT66). L'esistenza delle tecnologie NAT significa che i cinque scenari presentati per i server perimetrali di Lync Server sono ancora validi.


> [!WARNING]
> IPv6 è un argomento complesso che richiede una pianificazione accurata in collaborazione con il team responsabile della rete e il provider Internet, per assicurarsi che gli indirizzi assegnati a livello del server Windows e a livello di Lync Server 2013 funzionino come previsto. Per ulteriori risorse sull'indirizzamento e la pianificazione di IPv6, vedere i collegamenti alla fine di questo argomento.



**Topologia perimetrale consolidata singola con indirizzi IP pubblici**

![Scenario per singolo server perimetrale consolidato](images/JJ205148.2db9f9e1-75aa-4de0-ab3f-c6effddb4f4d(OCS.15).jpg "Scenario per singolo server perimetrale consolidato")

> [!important]  
> Se si utilizza il servizio Controllo di ammissione di chiamata, è ancora necessario assegnare indirizzi IPv4 all'interfaccia interna del server perimetrale. Il servizio Controllo di ammissione di chiamata utilizza indirizzi IPv4 e deve averli a disposizione per il corretto funzionamento.

## Argomenti della sezione

  - [Riepilogo dei certificati - singola topologia perimetrale consolidata con indirizzi IP pubblici in Lync Server 2013](lync-server-2013-certificate-summary-single-consolidated-edge-with-public-ip-addresses.md)

  - [Riepilogo delle porte - singola topologia perimetrale consolidata con indirizzi IP pubblici in Lync Server 2013](lync-server-2013-port-summary-single-consolidated-edge-with-public-ip-addresses.md)

  - [Riepilogo di DNS - singola topologia perimetrale consolidata con indirizzi IP pubblici in Lync Server 2013](lync-server-2013-dns-summary-single-consolidated-edge-with-public-ip-addresses.md)

## Vedere anche

#### Ulteriori risorse

[Architettura dell'indirizzamento IP versione 6](http://tools.ietf.org/html/rfc4291)  
[Formato degli indirizzi unicast globali IPv6](http://tools.ietf.org/html/rfc3587)  
[Indirizzi unicast IPv6 locali univoci](http://tools.ietf.org/html/rfc4193)

