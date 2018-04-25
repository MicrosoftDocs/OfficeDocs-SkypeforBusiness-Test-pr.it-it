---
title: Procedure consigliate per l'infrastruttura di base in Lync Server 2013
TOCTitle: Procedure consigliate per l'infrastruttura di base in Lync Server 2013
ms:assetid: 44aff88d-536c-4613-a81e-5398c9c6a648
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn518328(v=OCS.15)
ms:contentKeyID: 60490913
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Procedure consigliate per l'infrastruttura di base in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-01-27_

È probabile che siano già state adottate misure per progettare la tolleranza di errore nel sistema, mediante procedure che consentano di garantire la ridondanza hardware, proteggere il sistema in caso di interruzione dell'alimentazione, installare a intervalli regolari aggiornamenti della sicurezza e antivirus, oltre a controllare l'attività di Monitoring Server. Queste procedure costituiscono un vantaggio non solo per l'infrastruttura di Microsoft Lync Server 2013, ma anche per l'intera rete. Se non sono state già implementate, è consigliabile farlo prima di distribuire Lync Server 2013.

Per proteggere i server della distribuzione di Lync Server 2013 da danni accidentali o intenzionali che potrebbero causare l'inattività, adottare le precauzioni seguenti:

  - Tenere i server aggiornati con gli aggiornamenti della sicurezza. Per ricevere una notifica immediata ogni volta che viene rilasciato un bollettino sulla sicurezza per un qualsiasi prodotto Microsoft, è possibile effettuare la sottoscrizione al servizio Notifiche sulla sicurezza Microsoft. Per effettuare la sottoscrizione, visitare il sito Web Notifiche sulla sicurezza Microsoft all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=145202](http://go.microsoft.com/fwlink/p/?linkid=145202).

  - Controllare che i diritti di accesso siano configurati in modo corretto.

  - Installare i server in un ambiente fisico che consente solo accessi non autorizzati. Controllare che in tutti i server sia installato un software antivirus adeguato. Mantenere aggiornato il software con i file più recenti delle impronte digitali dei virus. Usare la funzionalità di aggiornamento automatico dell'antivirus per mantenere aggiornate le impronte digitali dei virus.

  - È consigliabile disabilitare i servizi del sistema operativo Windows Server non necessari nei computer in cui viene installato Lync Server 2013.

  - Crittografare i sistemi operativi e le unità disco in cui sono archiviati i file con un sistema di crittografia dell'intero volume, a meno che non sia possibile garantire un controllo completo e costante dei server, l'isolamento fisico totale e una rimozione delle autorizzazioni corretta e sicura delle unità disco sostituite o malfunzionanti.

  - Disabilitare tutte le porte DMA (Direct Memory Access) esterne del server, a meno che non sia possibile garantire un controllo serrato sull'accesso fisico ai server. Gli attacchi basati su DMA, che possono essere effettuati abbastanza facilmente, possono esporre informazioni particolarmente sensibili, ad esempio le chiavi di crittografia private.

