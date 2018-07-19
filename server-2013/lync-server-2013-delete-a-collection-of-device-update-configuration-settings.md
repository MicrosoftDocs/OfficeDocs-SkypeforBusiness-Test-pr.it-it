---
title: Eliminare una raccolta di impostazioni per la configurazione dell'aggiornamento dispositivi
TOCTitle: Eliminare una raccolta di impostazioni per la configurazione dell'aggiornamento dispositivi
ms:assetid: 1a649136-34a9-42a7-a5b3-a78bbfe93f36
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994019(v=OCS.15)
ms:contentKeyID: 52062104
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare una raccolta di impostazioni per la configurazione dell'aggiornamento dispositivi

 

_**Ultima modifica dell'argomento:** 2013-02-20_

Le impostazioni di configurazione per l'aggiornamento dei dispositivi possono essere eliminate anche utilizzando Windows PowerShell e il cmdlet **Remove-CsdeviceUpdateConfiguration**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).


## Per rimuovere una raccolta specifica di impostazioni di configurazione per l'aggiornamento dei dispositivi

  - Questo comando elimina le impostazioni di configurazione per l'aggiornamenti dei dispositivi applicate al sito di Redmond:
    
        Remove-CsDeviceUpdateConfiguration -Identity "site:Redmond"

## Per rimuovere tutte le impostazioni di configurazione per l'aggiornamento dei dispositivi applicate all'ambito del sito

  - Questo comando elimina tutte le impostazioni di configurazione degli aggiornamenti dei dispositivi applicate all'ambito del sito:
    
        Get-CsDeviceUpdateConfiguration -Filter "site:*" | Remove-CsDeviceUpdateConfiguration

## Per rimuovere le impostazioni di configurazione per l'aggiornamento dei dispositivi in base al valore della proprietà LogCleanUpInterval

  - Il comando seguente elimina tutte le impostazioni di configurazione per l'aggiornamento dei dispositivi in cui l'intervallo di pulizia del log è maggiore di 10 giorni (10.00:00:00):
    
        Get-CsDeviceUpdateConfiguration | Where-Object {$_.LogCleanUpInterval -gt "10.00:00:00" | Remove-CsDeviceUpdateConfiguration

Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet [Remove-CsDeviceUpdateConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsDeviceUpdateConfiguration).

