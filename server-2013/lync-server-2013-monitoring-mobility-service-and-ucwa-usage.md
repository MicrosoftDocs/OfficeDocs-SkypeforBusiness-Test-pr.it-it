---
title: Monitoraggio del servizio per dispositivi mobili e dell'utilizzo di UCWA
TOCTitle: Monitoraggio del servizio per dispositivi mobili e dell'utilizzo di UCWA
ms:assetid: 8389b37a-ca3e-4047-8b51-85bc07da87e8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690025(v=OCS.15)
ms:contentKeyID: 49301176
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Monitoraggio del servizio per dispositivi mobili e dell'utilizzo di UCWA

 

_**Ultima modifica dell'argomento:** 2013-02-14_

È necessario monitorare la CPU e la memoria utilizzate dal servizio Mobility di Lync Server (Mcx) e l'API Web Unified Communications (UCWA) con regolarità. Per monitorare l'utilizzo, è possibile utilizzare uno degli strumenti seguenti:

**Per l'API Web Unified Communications (UCWA):**

  - Il processo di lavoro **LyncUcwa** in Gestione Internet Information Services (IIS). Nel riquadro **Processi di lavoro** analizzare le colonne **% CPU** e **Byte privati (KB)** (memoria).

  - Contatori delle prestazioni relativi a **CPU** e **Processore**.

Per la maggior parte delle distribuzioni, l'utilizzo della CPU da parte di UCWA deve essere inferiore a una media del 15%. L'utilizzo della memoria deve rientrare nei limiti descritti in [Monitoraggio dei limiti di capacità della memoria del server](lync-server-2013-monitoring-for-server-memory-capacity-limits.md).

Oltre ai contatori di utilizzo della CPU e della memoria, è possibile utilizzare i contatori delle prestazioni seguenti per determinare quando un server è sovraccarico di richieste:

  - **LS:WEB – Throttling and Authentication\\WEB – Total Requests in Processing**, che indica il numero di richieste Web in sospeso nel server. Quando il contatore raggiunge 10.000, le richieste successive avranno esito negativo con il messaggio di errore "503 - Servizio non disponibile".

  - **ASP.NET\\Requests Queued** (deve essere sempre zero).


> [!NOTE]
> Se si raggiungono o superano questi valori, è consigliabile verificare e ricalcolare la pianificazione delle capacità per ottenere dimensioni corrette per CPU, numero di core e memoria per i computer che ospitano i servizi Web.



**Per il servizio Mobility (Mcx):**

  - Processi di lavoro **CSIntMcxAppPool** e **CSExtMcxAppPool** in Gestione Internet Information Services (IIS). Nel riquadro **Processi di lavoro** analizzare le colonne **% CPU** e **Byte privati (KB)** (memoria).

  - Contatori delle prestazioni relativi a **CPU** e **Processore**.

Per la maggior parte delle distribuzioni, l'utilizzo della CPU da parte del servizio Mobility deve essere inferiore a una media del 15%. L'utilizzo della memoria deve rientrare nei limiti descritti in [Monitoraggio dei limiti di capacità della memoria del server](lync-server-2013-monitoring-for-server-memory-capacity-limits.md).

Oltre ai contatori di utilizzo della CPU e della memoria, è possibile utilizzare il contatori delle prestazioni ASP.NET seguenti per determinare quando un server è sovraccarico di richieste:

  - **ASP.NET v2.0.50727\\Requests Current**, che indica il numero di richieste Web in sospeso nel server. Quando il contatore raggiunge 5.000, le richieste successive avranno esito negativo con il messaggio di errore "503 - Servizio non disponibile".

  - **ASP.NET\\Requests Queued** (deve essere sempre zero).


> [!NOTE]
> Se si raggiungono o superano questi valori, è consigliabile verificare e ricalcolare la pianificazione delle capacità per ottenere dimensioni corrette per CPU, numero di core e memoria per i computer che ospitano i servizi Web.



## Vedere anche

#### Concetti

[Monitoraggio dei limiti di capacità della memoria del server](lync-server-2013-monitoring-for-server-memory-capacity-limits.md)

