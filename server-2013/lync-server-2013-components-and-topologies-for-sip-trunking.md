---
title: 'Lync Server 2013: Componenti e topologie per il trunking SIP'
TOCTitle: Componenti e topologie per il trunking SIP
ms:assetid: 8ed9a9d0-517e-4f36-a131-22cdafa257fa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398720(v=OCS.15)
ms:contentKeyID: 49301291
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Componenti e topologie per il trunking SIP in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

Nella figura seguente viene illustrata la topologia di trunking SIP in Lync Server.

**Topologia di trunking SIP**

![Topologia basata sul trunking SIP](images/Gg398720.669fb55d-7c81-4e21-9421-fabc43d6e064(OCS.15).jpg "Topologia basata sul trunking SIP")

Come illustrato nella figura, una rete privata virtuale (VPN, Virtual Private Network) IP viene utilizzata per la connettività tra l'azienda e il provider di servizi PSTN. Lo scopo di questa rete privata è quello di fornire connettività IP, migliorare la protezione e, facoltativamente, ottenere garanzie relative alla qualità del servizio. Data la natura delle VPN, non è necessario utilizzare TLS per il traffico di segnalazione SIP o SRTP per il traffico multimediale. Le connessioni tra l'azienda e il provider di servizi sono pertanto normali connessioni TCP per SIP e RTP (tramite UDP) per i contenuti multimediali potenzialmente inviati tramite una rete VPN IP. Accertarsi che le porte di tutti i firewall tra i router VPN siano aperte per consentire ai router VPN di comunicare e che gli indirizzi IP nei perimetri esterni dei router VPN consentano l'esecuzione del routing pubblicamente.

> [!IMPORTANT]  
> Rivolgersi al proprio provider di servizi per determinare se offra supporto per la disponibilità elevata, failover compreso. In caso affermativo sarà necessario determinare le procedure per configurarla, ad esempio se sia necessario configurare un solo indirizzo IP e un trunk SIP in ogni Mediation Server, oppure se sia necessario configurare più trunk SIP per ogni Mediation Server<br />Se sono presenti più siti centrali, chiedere al provider di servizi se offra anche la capacità di abilitare connessioni da e verso un altro sito centrale.


> [!NOTE]
> Per il trunking SIP è consigliabile distribuire Mediation Server autonomi. Per informazioni dettagliate, vedere <A href="lync-server-2013-deploying-mediation-servers-and-defining-peers.md">Distribuzione di Mediation Server e definizione di peer in Lync Server 2013</A> nella documentazione relativa alla distribuzione.



## Protezione del Mediation Server per il trunking SIP

Per motivi di sicurezza è opportuno configurare una LAN virtuale (VLAN) per ogni connessione tra i due router VPN. La procedura per la configurazione di una VLAN varia in base al produttore del router. Per informazioni dettagliate, rivolgersi al fornitore del router.

È consigliabile attenersi alle linee guida seguenti:

  - Configurare una LAN virtuale (VLAN) tra il Mediation Server e il router VPN nella rete perimetrale, denominata anche DMZ o subnet schermata.

  - Non consentire il trasferimento di pacchetti broadcast o multicast dal router alla VLAN.

  - Bloccare tutte le regole di routing che instradano il traffico ovunque tranne che al Mediation Server.

Se si utilizza un server VPN, è consigliabile attenersi alle linee guida seguenti:

  - Configurare una VLAN tra il server VPN e il Mediation Server.

  - Non consentire la trasmissione di pacchetti broadcast o multicast dal server VPN alla VLAN.

  - Bloccare tutte le regole di routing che instradano il traffico dei server VPN ovunque tranne che al Mediation Server.

  - Crittografare i dati sulla VPN utilizzando Generic Routing Encapsulation (GRE).

