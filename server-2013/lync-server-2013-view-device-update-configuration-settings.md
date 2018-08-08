---
title: "Lync Server 2013: Visualizza configurazione di Aggiornamento dispositivi"
TOCTitle: Visualizzare le impostazioni di configurazione di Aggiornamento dispositivi
ms:assetid: aa6a70a9-bd77-4606-b797-ea6a3bab9cf2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994059(v=OCS.15)
ms:contentKeyID: 52062288
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare le impostazioni di configurazione di Aggiornamento dispositivi in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-20_

È possibile visualizzare le impostazioni di configurazione di Servizio Aggiornamento dispositivi utilizzando Lync Server Management Shell e il cmdlet **Get-CsDeviceUpdateConfiguration**, eseguibile da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell.


> [!NOTE]
> Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</A>.





  - 
    
    Per visualizzare informazioni su tutte le route vocali, digitare il comando seguente in Lync Server Management Shell e premere INVIO:
    
        Get-CsDeviceUpdateConfiguration
    
    Questo comando restituisce informazioni simili alle seguenti:
    
        Identity               : Global
        ValidLogFileTypes      : {Watson, Config, Diaglog, CELog}
        ValidLogFileExtensions : {.dmp, .clg, .clg1, .clg2...}
        MaxLogFileSize         : 1024000
        MaxLogCacheLimit       : 512000
        LogCleanUpInterval     : 10.00:00:00
        LogFlushInterval       : 00:05:00
        LogCleanUpTimeOfDay    :

Per informazioni dettagliate su questo cmdlet, vedere l'argomento della Guida [Get-CsDeviceUpdateConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsDeviceUpdateConfiguration).

