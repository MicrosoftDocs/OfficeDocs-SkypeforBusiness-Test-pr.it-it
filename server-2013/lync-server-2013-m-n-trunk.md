---
title: 'Lync Server 2013: Trunk con relazioni molti-a-molti'
TOCTitle: Trunk con relazioni molti-a-molti
ms:assetid: dc4c5d66-297c-48a5-91b9-b9b8ce44a6e0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398971(v=OCS.15)
ms:contentKeyID: 49302185
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Trunk con relazioni molti-a-molti in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-01_

Lync Server 2013 offre una maggiore flessibilità per la definizione di un trunk per il routing delle chiamate rispetto alle versioni precedenti. Un trunk è un'associazione logica tra un Mediation Server e il numero di una porta di attesa e un gateway e il numero di una porta di attesa. Questo significa che un Mediation Server può disporre di più trunk per lo stesso gateway, un Mediation Server può disporre di più trunk per gateway diversi, mentre un gateway può disporre di più trunk per Mediation Server diversi.

È comunque necessario creare un trunk radice quando viene aggiunto un gateway alla topologia di Lync utilizzando Generatore di topologie. Il numero di gateway che un determinato Mediation Server può gestire dipende dalla capacità di elaborazione del server nelle ore di punta. Se si distribuisce un Mediation Server in un computer che supera i requisiti minimi per Lync Server 2013, come decritto in [Hardware supportato per Lync Server 2013](lync-server-2013-supported-hardware.md) nella documentazione relativa al supporto, la stima del numero di chiamate attive senza bypass gestibili da un Mediation Server autonomo è pari circa a 1000. Se la distribuzione viene eseguita in un computer che soddisfa queste specifiche, il Mediation Server dovrebbe eseguire la transcodifica, ma continuare comunque a instradare le chiamate per più gateway anche se i gateway non supportano il bypass multimediale.

Quando si definisce una route di chiamata, si specificano i trunk ma non i Mediation Server associati a tale route. Per associare i trunk ai Mediation Server si utilizza invece Generatore di topologie. In altri termini, il routing determina quale trunk utilizzare per una chiamata e quindi a quale Mediation Server associato a tale trunk viene inviata la segnalazione per la la chiamata.

Il Mediation Server può essere distribuito come pool, che può essere collocato con un pool Front End o distribuito come pool autonomo. Quando un Mediation Server è collocato con un pool Front End, la dimensione massima del pool può essere pari a 12 (il limite della dimensione del pool di registrazione). Nell'insieme, queste nuove funzionalità consentono di usufruire di una maggiore affidabilità e di una flessibilità di distribuzione superiore per i Mediation Server, ma richiedono funzionalità associate nelle entità peer seguenti:

  - **Gateway PSTN.** Un gateway PSTN (Public Switched Telephone Network) qualificato per Lync Server 2013 deve implementare il bilanciamento del carico DNS, tramite il quale può agire come servizio di bilanciamento del carico per un pool di Mediation Server e pertanto bilanciare il carico delle chiamate nel pool.

  - **Session Border Controller**. Per un trunk SIP, l'entità peer è costituita da un Session Border Controller (SBC) presso un provider di servizi di telefonia Internet. Nella direzione dal pool di Mediation Server all'SBC, l'SBC può ricevere connessioni da qualsiasi Mediation Server del pool. Nella direzione dall'SBC al pool, il traffico può essere inviato a qualsiasi Mediation Server del pool. Per ottenere questo risultato, uno dei metodi disponibili è il bilanciamento del carico DNS, se supportato dal provider di servizi e dall'SBC. Un'alternativa consiste nel fornire al provider di servizi gli indirizzi IP di tutti i Mediation Server del pool. Il provider di servizi ne effettuerà quindi il provisioning nel relativo SBC come trunk SIP separato per ogni Mediation Server. Infine, il provider di servizi gestirà il bilanciamento del carico per i propri server. Non tutti i provider di servizi o SBC supportano queste funzionalità. Inoltre, il provider di servizi potrebbe addebitare costi aggiuntivi. Ogni trunk SIP per l'SBC in genere prevede una tariffa mensile.

  - **IP-PBX**. Nella direzione dal pool di Mediation Server alla terminazione SIP del sistema IP-PBX, il sistema IP-PBX può ricevere connessioni da qualsiasi Mediation Server del pool. Nella direzione dal sistema IP-PBX al pool, il traffico può essere inviato a qualsiasi Mediation Server del pool. Poiché la maggior parte dei sistemi IP-PBX non supporta il bilanciamento del carico DNS, è consigliabile definire singole connessioni SIP dirette dal sistema IP-PBX a ogni Mediation Server del pool. Il sistema IP-PBX gestirà quindi il bilanciamento del carico distribuendo il traffico sul gruppo di trunk. Si presuppone che il gruppo di trunk disponga di un insieme coerente di regole di routing nel sistema IP-PBX. Prima di decidere se un cluster di Mediation Server può interagire correttamente con un sistema IP-PBX, è necessario determinare se questo concetto di gruppo di trunk è supportato dal sistema IP-PBX e come interagisce con l'architettura di ridondanza e di clustering del sistema IP-PBX.

Un pool di Mediation Server deve disporre di una visibilità uniforme del gateway peer con cui interagisce. Questo significa che tutti i membri del pool accedono alla stessa definizione del gateway peer dall'archivio di configurazione e hanno le stesse probabilità di interagire con esso per le chiamate in uscita. Pertanto, non è possibile segmentare il pool in modo che alcuni Mediation Server comunichino solo con determinati peer gateway per le chiamate in uscita. Se tale segmentazione è necessaria, utilizzare un pool distinto di Mediation Server, ad esempio nel caso in cui non siano presenti le funzionalità associate nei gateway PSTN, nei trunk SIP o nei sistemi IP-PBX per l'interazione con un pool, come decritto più indietro in questo argomento.

Un gateway PSTN, un sistema IP-PBX o un peer trunk SIP può eseguire il routing a più Mediation Server o trunk. Il numero di gateway controllabili da un determinato pool di Mediation Server dipende dal numero di chiamate che utilizzano il bypass multimediale. Se un numero elevato di chiamate utilizza questa funzionalità, un Mediation Server del pool può gestire molte più chiamate, perché è necessaria una sola elaborazione del livello di segnalazione.

