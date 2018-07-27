---
title: Monitoraggio dei limiti di capacità della memoria del server
TOCTitle: Monitoraggio dei limiti di capacità della memoria del server
ms:assetid: 1697ea71-6fcf-480d-b4e9-cd79f94d247e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh689982(v=OCS.15)
ms:contentKeyID: 49299793
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Monitoraggio dei limiti di capacità della memoria del server

 

_**Ultima modifica dell'argomento:** 2013-02-16_

    Some information in this topic pertains to Cumulative Updates for Lync Server 2013: February 2013.


> [!WARNING]
> Le informazioni contenute in questo argomento che fanno riferimento alla pianificazione della capacità sono relative solo ai client Lync 2010 Mobile e al servizio Mobility (Mcx). La pianificazione della capacità per l'API Web Unified Communications utilizzata dai client Lync 2013 Mobile, è fornita da Lync Server 2013, Strumento di pianificazione.



Due contatori delle prestazioni dei dispositivi mobili consentono di determinare l'utilizzo corrente, di pianificare la capacità per il servizio Mobility (Mcx) di Lync Server 2013 e di monitorare l'utilizzo di memoria per UCWA. Per UCWA, la categoria dei contatori è **LS:WEB - UCWA**. Per il servizio Mobility (Mcx), i contatori si trovano nella categoria **LS:WEB - Mobile Communication Service**. I contatori da monitorare sono:

  - **Currently Active Session Count with Active Presence Subscriptions**, che indica il numero corrente di endpoint registrati tramite UCWA o il servizio Mobility (Mcx) che dispongono di sottoscrizioni relative alla presenza attive (numero di utenti di dispositivi mobili sempre connessi)

  - **Currently Active Session Count**, che indica il numero corrente di endpoint registrati tramite UCWA o il servizio Mobility

Se la differenza tra il valore del contatore **Currently Active Session Count with Active Presence Subscriptions** e quello del contatore **Currently Active Session Count** è minima nel tempo, significa che la maggior parte degli utenti di dispositivi mobili ha un dispositivo sempre connesso, quale un dispositivo Android o Nokia (solo per Mcx). I dispositivi sempre connessi UCWA includono i dispositivi Apple o Android che eseguono i client Lync 2013 Mobile. Se il valore del contatore **Currently Active Session Count** è considerevolmente superiore a quello del contatore **Currently Active Session Count with Active Presence Subscriptions**, significa che un numero maggiore di utenti utilizza un dispositivo endpoint in background, ad esempio un dispositivo Apple iOS o Windows Phone in Mcx. (Windows Phone è l'unico client Lync 2013 Mobile che eseguirà la registrazione).

Per i contatori delle prestazioni **Currently Active Session Count with Active Presence Subscriptions** e **Currently Active Session Count** è consigliabile impostare un limite in base all'utilizzo previsto, ai risultati della pianificazione della capacità, al monitoraggio continuo del servizio Mobility e ad altri contatori del Front End Server. I limiti impostati dovrebbero consentire una valutazione della capacità del server e attivare avvisi in caso di superamento della capacità.

Per determinare i limiti appropriati, è necessario innanzitutto stabilire quanta memoria è disponibile nel Front End Server per il servizio Mobility. Monitorare i contatori per stabilire quando è necessario pianificare ulteriore capacità secondo la formula seguente:

Memoria totale utilizzata dal servizio Mobility (Mcx) (MB) = 164 + (400 + 134) / 1024 \* **Currently Active Session Count with Active Presence Subscriptions** + 400 / 1024 \* (**Currently Active Session Count** - **Currently Active Session Count with Active Presence Subscriptions**)

> [!IMPORTANT]  
> Microsoft Lync Server 2010 Capacity Calculator è un foglio di calcolo prepopolato con tutte le formule che in fase di pianificazione consentono di stabilire i requisiti necessari per i server, inclusi CPU, memoria e disco rigido. È possibile scaricare il foglio di calcolo e un documento associato all'indirizzo: <a href="http://go.microsoft.com/fwlink/?linkid=212657" class="uri">http://go.microsoft.com/fwlink/?linkid=212657</a>

Il Front End Server deve disporre di memoria sufficiente per supportare il servizio Mobility in situazioni di failover. È possibile monitorare la memoria attualmente disponibile nel Front End Server mediante il contatore **Memory\\Available Mbytes** oppure utilizzando l'equazione sopra riportata per pianificare la quantità di memoria che si prevede verrà utilizzata dal servizio Mobility.

Se la quantità di memoria disponibile nel Front End Server è inferiore a 1.500 MB quando si pianifica il numero previsto di utenti mobili, sarà necessario aggiungere ulteriore hardware per supportare il servizio per dispositivi mobili. Per ulteriori informazioni, vedere [Monitoraggio dei dispositivi mobili per le prestazioni in Lync Server 2013](lync-server-2013-monitoring-mobility-for-performance.md) nella documentazione relativa alle operazioni.

## Vedere anche

#### Ulteriori risorse

[Monitoraggio dei dispositivi mobili per le prestazioni in Lync Server 2013](lync-server-2013-monitoring-mobility-for-performance.md)

