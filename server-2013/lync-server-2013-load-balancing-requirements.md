---
title: Requisiti per il bilanciamento del carico per Lync Server 2013
TOCTitle: Requisiti per il bilanciamento del carico per Lync Server 2013
ms:assetid: 84489328-64a4-486c-9384-a3e5c8ed9c8b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615011(v=OCS.15)
ms:contentKeyID: 49301187
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti per il bilanciamento del carico per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-05_

Se sono presenti pool Front End, pool di Server Director o pool di server perimetrale, è necessario distribuire il bilanciamento del carico per questi pool. Il bilanciamento del carico consente di distribuire il traffico tra i server in un pool.

In Lync Server 2013 sono supportati due tipi di soluzioni di bilanciamento del carico per il traffico client-to-server: bilanciamento del carico DNS (Domain Name System) e bilanciamento del carico hardware. Il bilanciamento del carico DNS offre numerosi vantaggi, tra cui amministrazione più semplice, maggiore efficienza per la risoluzione dei problemi e la possibilità di isolare la maggior parte del traffico di Lync Server da potenziali problemi del servizio di bilanciamento del carico hardware.

Per stabilire quale soluzione di bilanciamento del carico è appropriata per ogni pool nella distribuzione, tenere presenti le restrizioni seguenti:

  - Per l'interfaccia perimetrale interna e per quella esterna è necessario utilizzare lo stesso tipo di bilanciamento del carico. Non è possibile utilizzare il bilanciamento del carico DNS in un'interfaccia e il bilanciamento del carico hardware nell'altra.

  - Alcuni tipi di traffico richiedono un servizio di bilanciamento del carico hardware. Il traffico HTTP richiede, ad esempio, un servizio di bilanciamento del carico hardware anziché il bilanciamento del carico DNS. Il bilanciamento del carico DNS non funziona con il traffico Web da client a server.

Per informazioni dettagliate sulla scelta delle soluzioni di bilanciamento del carico hardware, vedere [Requisiti relativi al servizio di bilanciamento del carico hardware per Lync Server 2013](lync-server-2013-hardware-load-balancer-requirements.md).

Se si sceglie di utilizzare il bilanciamento del carico DNS per un pool, ma è comunque necessario implementare servizi di bilanciamento del carico hardware per il traffico, ad esempio il traffico HTTP, l'amministrazione dei servizi di bilanciamento del carico hardware risulta notevolmente semplificata. Ad esempio, la configurazione dei servizi di bilanciamento del carico hardware risulta semplificata poiché gestisce unicamente il traffico HTTP e HTTPS, mentre gli altri servizi sono gestiti dal bilanciamento del carico DNS. Per informazioni dettagliate, vedere [Bilanciamento del carico DNS in Lync Server 2013](lync-server-2013-dns-load-balancing.md).

Per il traffico server-to-server, Lync Server 2013 si serve di un bilanciamento del carico basato sulla topologia. I server leggono la topologia pubblicata in archivio di gestione centrale per ottenere i nomi FQDN dei server in essa contenuti, e distribuiscono automaticamente il carico tra i server. Gli amministratori non devono configurare o gestire questo tipo di bilanciamento del carico.

Se ci si serve del bilanciamento del carico DNS e si ha bisogno di bloccare il traffico diretto verso un computer specifico, non è sufficiente rimuovere le voci di indirizzo IP dal Pool FQDN, ma è necessario rimuovere dal computer anche la voce DNS.

