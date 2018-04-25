---
title: Requisiti dell'infrastruttura di rete per Lync Server 2013
TOCTitle: Requisiti dell'infrastruttura di rete per Lync Server 2013
ms:assetid: 35c7bb3f-8e0f-48b7-8a2c-857d4b42a4c4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425841(v=OCS.15)
ms:contentKeyID: 49300158
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti dell'infrastruttura di rete per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-08-28_

La scheda di rete di ogni server della topologia di Lync Server 2013 deve supportare almeno 1 gigabit al secondo (Gbps). È in genere consigliabile connettere tutti i ruoli del server all'interno della topologia di Lync Server tramite una rete locale (LAN) a bassa latenza e a elevata larghezza di banda. Le dimensioni della rete LAN dipendono da quelle della topologia:

  - Nelle topologie Standard Edition standard i server devono trovarsi in una rete che supporta una scheda Ethernet da 1 Gbps o equivalente.

  - Nelle topologie pool Front End la maggior parte dei server deve trovarsi in una rete che supporta più di 1 Gbps, soprattutto se vengono supportate le conferenze audio/video (A/V) e la condivisione delle applicazioni.

È possibile supportare l'integrazione della rete PSTN (Public Switched Telephone Network) utilizzando linee T1/E1 o il trunking SIP.

## Requisiti di rete audio/video

Tra i requisiti di rete per le funzionalità audio/video (A/V) in una distribuzione di Lync Server sono inclusi:

  - Se si distribuisce un server perimetrale singolo o un pool di server perimetrali usando il bilanciamento del carico DNS, è possibile configurare il firewall esterno come NAT. Non è possibile configurare il firewall interno come NAT. Per informazioni dettagliate su questi requisiti, vedere [Determinare i requisiti di porte e firewall A/V esterni per Lync Server 2013](lync-server-2013-determine-external-a-v-firewall-and-port-requirements.md) nella documentazione relativa alla pianificazione.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Se si dispone di un pool di server perimetrali e si utilizza un bilanciamento del carico hardware, è necessario usare indirizzi IP pubblici per ciascuno dei server perimetrali e non è possibile usare il NAT per i server del pool nel dispositivo NAT (ad esempio il firewall o un altro dispositivo dell'infrastruttura che eseguirebbe il NAT del traffico in entrata o in uscita). Per informazioni dettagliate, vedere <a href="lync-server-2013-port-summary-scaled-consolidated-edge-with-hardware-load-balancers.md">Riepilogo delle porte - topologia perimetrale consolidata con scalabilità implementata e servizi di bilanciamento del carico hardware in Lync Server 2013</a> nella documentazione relativa alla pianificazione per l'accesso utente esterno.</td>
    </tr>
    </tbody>
    </table>


  - Se nell'organizzazione è prevista un'infrastruttura di qualità del servizio (QoS), il sottosistema multimediale è progettato per essere utilizzato nell'infrastruttura esistente.

  - Se si utilizza IPSec (Internet Protocol security), è consigliabile disabilitarlo per gli intervalli di porte usati per il traffico A/V. Per informazioni dettagliate, vedere [Eccezioni Ipsec in Lync Server 2013](lync-server-2013-ipsec-exceptions.md) nella documentazione relativa alla pianificazione.

Per garantire una qualità multimediale ottimale, eseguire le operazioni seguenti:

  - Effettuare il provisioning dei collegamenti di rete in modo da supportare la velocità effettiva di 65 kilobit al secondo (Kbps) per flusso audio e 500 Kbps per flusso video, se abilitati, durante i periodi di picco di utilizzo. Una sessione audio o video bidirezionale è costituita da due flussi.

  - Per gestire picchi di traffico non previsti che superano questo livello e un utilizzo sempre maggiore nel tempo, gli endpoint multimediali di Lync Server possono adattarsi a diverse condizioni di rete e supportare carichi pari alla velocità effettiva triplicata (vedere il paragrafo precedente) per audio e video, conservando comunque una qualità accettabile. Questa adattabilità non deve tuttavia lasciar supporre che venga supportata una rete sottodimensionata. In una rete sottodimensionata la capacità degli endpoint multimediali di Lync Server di gestire in modo dinamico condizioni di rete variabili, ad esempio un'elevata perdita di pacchetti, è ridotta.

  - Per i collegamenti di rete in cui il provisioning è un'operazione estremamente costosa e difficile, potrebbe essere necessario valutare la possibilità di effettuare il provisioning per un volume di traffico inferiore. In questo scenario l'elasticità degli endpoint multimediali di Lync Server assorbe la differenza tra il volume di traffico e il livello di traffico di picco, con una leggera flessione della qualità vocale. Si verifica inoltre una riduzione della capacità aggiuntiva altrimenti disponibile per assorbire picchi di traffico improvvisi.

  - Per i collegamenti di cui non è possibile effettuare correttamente il provisioning in tempi brevi, ad esempio un sito con collegamenti WAN insufficienti, valutare la possibilità di disabilitare la funzionalità video per alcuni utenti.

  - Effettuare il provisioning della rete in modo da garantire un ritardo (latenza) end-to-end massimo di 150 millisecondi (ms) in condizioni di carico di picco. La latenza è uno dei problemi di rete che non può essere ridotto dai componenti multimediali di Lync Server. È importante quindi individuare ed eliminare i punti deboli.

  - Per i server che eseguono software antivirus, includere tutti i server che eseguono Lync Server nell'elenco delle eccezioni in modo da garantire qualità audio e prestazioni ottimali.

## Requisiti di rete per le conferenze

La larghezza di banda utilizzata per il download del contenuto delle conferenze dal server Internet Information Services (IIS) dipende dalle dimensioni del contenuto caricato.

