---
title: Utilizzo del servizio di registrazione centralizzato
TOCTitle: Utilizzo del servizio di registrazione centralizzato
ms:assetid: 7b05aaef-f0ea-4649-ba8a-02e68b0cdf23
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688101(v=OCS.15)
ms:contentKeyID: 49887618
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Utilizzo del servizio di registrazione centralizzato

 

_**Ultima modifica dell'argomento:** 2012-11-01_

La funzione servizio di registrazione centralizzato è nuova in Lync Server 2013. È una versione sostitutiva e migliorata degli strumenti **OCSLogger** e **OCSTracer** presenti nelle versioni precedenti. È possibile utilizzare la funzione servizio di registrazione centralizzato per eseguire le seguenti operazioni:

  - Avviare la registrazione su uno o più computer e pool da una località singola, con un singolo comando.

  - Interrompere la registrazione su uno o più computer e pool da una località singola, con un singolo comando.

  - Cercare registri su uno o più computer e pool per località singola o singolo comando. È possibile personalizzare il comando di ricerca affinché restituisce l'intera aggregazione di registri raccolti e archiviati su tutti i computer, o affinché restituisca un risultato più filtrato, contenente soltanto dati specifici.

  - Configurare sessioni di registrazione come segue:
    
      - Definire uno **Scenario**, oppure utilizzarne uno predefinito. Uno *scenario* in servizio di registrazione centralizzato è costituito da un ambito (globale o sito), un nome dello scenario per identificarne la finalità, e uno o più provider. È possibile eseguire due scenari contemporaneamente su un computer.
    
      - Utilizzare un *provider* esistente, o crearne uno nuovo. Un *provider* definisce cosa viene raccolto da una sessione di registrazione, nonché il livello di dettagli, i componenti da tracciare e i contrassegni applicati.
        
        > [!tip]  
        > Se si ha familiarità con OCSLogger, il termine <em>provider</em> fa riferimento alla raccolta di <strong>componenti</strong> (ad esempio, S4, SIPStack), un <strong>tipo di registrazione</strong> (ad esempio, WPP, EventLog o IIS logfile), un <strong>livello di traccia</strong> (ad esempio, All, verbose, debug) e <strong>contrassegni</strong> (ad esempio, TF_COMPONENT, TF_DIAG). Questi elementi sono definiti nel provider (una variabile di Windows PowerShell) e passati al comando di servizio di registrazione centralizzato.    
      - Configurare i computer e i pool dai quali si desidera raccogliere registri.
    
      - Definire l'ambito della sessione di registrazione dalle opzioni **Sito** (per eseguire raccolte di registri su computer che si trovano su quel sito soltanto), o **Globale** (per eseguire raccolte di registri su tutti i computer della distribuzione).

La funzione servizio di registrazione centralizzato è molto potente, e in grado di soddisfare tutte le esigenze di risoluzione dei problemi, dalle minori alle maggiori. Dall'analisi della causa principale ai problemi di rendimento, servizio di registrazione centralizzato rappresenta un importante strumento per qualunque amministratore. Tutti gli esempi sono mostrati attraverso l'utilizzo di Lync Server Management Shell. Esiste un componente da riga di comando per servizio di registrazione centralizzato chiamato **CLSController.exe**. Allo strumento da riga di comando viene offerto supporto dallo strumento stesso. Tuttavia, le funzioni eseguibili dalla riga di comando sono limitate. Attraverso l'utilizzo di Lync Server Management Shell si può accedere a un set di funzioni maggiore e più personalizzabile. È sempre consigliabile considerare Lync Server Management Shell come primo e più importante metodo quando si utilizza il servizio di registrazione centralizzato.

Negli argomenti di questa sezione viene descritto come utilizzare il servizio di registrazione centralizzato, e sono riportati esempi di utilizzo delle molte funzionalità.

## Argomenti della sezione

  - [Panoramica del servizio di registrazione centralizzato](lync-server-2013-overview-of-the-centralized-logging-service.md)

  - [Gestione delle impostazioni di configurazione del servizio di registrazione centralizzato tramite PowerShell](lync-server-2013-managing-the-centralized-logging-service-configuration-settings.md)

  - [Informazioni sulle impostazioni di configurazione del servizio di registrazione centralizzato](lync-server-2013-understanding-centralized-logging-service-configuration-settings.md)

  - [Utilizzo del comando Start per l'acquisizione dei log da parte del servizio di registrazione centralizzato](lync-server-2013-using-start-for-the-centralized-logging-service-to-capture-logs.md)

  - [Utilizzo del comando Stop per il servizio di registrazione centralizzato](lync-server-2013-using-stop-for-the-centralized-logging-service.md)

  - [Utilizzo della ricerca sui log di acquisizione creati dal servizio di registrazione centralizzato](lync-server-2013-using-search-on-capture-logs-created-by-the-centralized-logging-service.md)

  - [Lettura dei log di acquisizione dal servizio di registrazione centralizzato](lync-server-2013-reading-capture-logs-from-the-centralized-logging-service.md)

