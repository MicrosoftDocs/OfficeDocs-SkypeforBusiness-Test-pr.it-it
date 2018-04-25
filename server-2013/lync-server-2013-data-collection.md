---
title: 'Lync Server 2013: Raccolta dati'
TOCTitle: Raccolta dati
ms:assetid: e40b03e5-455d-4bbc-831a-c61b1380db53
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399008(v=OCS.15)
ms:contentKeyID: 49302263
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Raccolta dati in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-08_

Nel software di comunicazioneMicrosoft Lync Server 2013 è possibile utilizzare Microsoft Lync Server 2013, Strumento di pianificazione senza documentare gli indirizzi IP esistenti e proposti e i nomi di dominio completo (FQDN) degli Edge Server, ma è molto più complesso procedere in questo modo senza causare errori di configurazione. Se ad esempio è necessaria la coesistenza per un periodo di tempo, un errore comune è il riutilizzo degli FQDN da una distribuzione perimetrale esistente per la distribuzione perimetrale di Lync Server 2013. Prendendo nota degli indirizzi IP esistenti e proposti e degli FQDN in un foglio di calcolo, in una tabella oppure in un altro tipo di modulo grafico, si evitano problemi di configurazione durante l'installazione.


> [!WARNING]
> Se si conoscono versioni precedenti dello Strumento di pianificazione, è possibile che lo strumento sia stato utilizzato per creare la topologia ed esportare il documento della topologia da utilizzare in Generatore di topologie per pubblicare la topologia. La possibilità di esportare la topologia non è più disponibile nello Strumento di pianificazione. L'utilizzo di una versione precedente dello Strumento di pianificazione per creare un documento relativo alla topologia per Lync Server 2013 è caldamente sconsigliato e produrrà risultati imprevisti.



Pertanto, l'approccio consigliato consiste nell'utilizzare il modello di raccolta dati seguente che corrisponde alla specifica topologia perimetrale per raccogliere i vari FQDN e indirizzi IP da immettere nello Strumento di pianificazione. Documentando la configurazione corrente e quella proposta, è possibile inserire i valori nel contesto corretto per l'ambiente di produzione. Si è inoltre costretti a valutare come configurare la coesistenza e funzionalità come URL semplici, condivisioni file e bilanciamento del carico.

Per una corretta distribuzione di Microsoft Lync Server 2013, è necessario comprendere le interazioni tra i singoli componenti e le dipendenze dai singoli componenti. Tramite la raccolta dei dati dall'infrastruttura di rete e server esistente e attenendosi alle indicazioni per la pianificazione in queste sezioni, è possibile integrare i componenti del server perimetrale di Lync Server 2013 nell'infrastruttura.

Come indicato nelle informazioni introduttive in [Scelta di una topologia in Lync Server 2013](lync-server-2013-choosing-a-topology.md), esistono tre architetture principali con due varianti, per un totale di cinque scenari di distribuzione possibili. Uno di questi scenari rappresenterà il punto di partenza per la raccolta dei dati. Gli indirizzi IP, i nomi dei server e i nomi di dominio sono esempi che coincidono con il certificato, il firewall e i diagrammi DNS corrispondenti che descrivono in dettaglio le informazioni richieste per una soluzione di pianificazione completa. I diagrammi e la compilazione dei valori richiesti per certificato, DNS e firewall sono particolarmente importanti per le comunicazioni tra team, nei casi in cui la gestione dell'Autorità di certificazione, della configurazione del firewall e del sistema DNS è responsabilità di team diversi dal team che si occupa della pianificazione della distribuzione. I diagrammi offrono informazioni sui componenti necessari che è possibile utilizzare per la comunicazione dei requisiti nell'ottica della collaborazione tra team.

I diagrammi forniti sono intenzionalmente generali, ma consentono la raccolta di dati pertinenti che sarebbero necessari per la comunicazione dei requisiti in uno scenario di collaborazione tra team, nel quale la rete, i firewall, la creazione e la gestione dei certificati, la distribuzione dei server e la gestione dei server sono affidati a gruppi diversi. La possibilità di avere a disposizione tutti i dettagli necessari per la configurazione di rete, firewall, porte e protocolli, certificati e server è molto preziosa durane la distribuzione di Lync Server.

**server perimetrale e pool di server perimetrali**

![Server perimetrale e pool di server perimetrali](images/Gg399008.7624717a-ce99-4ae8-a929-2c4d74a2e47d(OCS.15).jpg "Server perimetrale e pool di server perimetrali")

**Proxy inverso**

![Proxy inverso](images/Gg399008.cf63fc50-2d11-4334-afc8-2d664ba1b6bb(OCS.15).jpg "Proxy inverso")

**Server Director o pool di server Director**

![Director e pool di server Director](images/Gg399008.56ba29ff-1309-4d5d-bf5c-35372169e947(OCS.15).jpg "Director e pool di server Director")

