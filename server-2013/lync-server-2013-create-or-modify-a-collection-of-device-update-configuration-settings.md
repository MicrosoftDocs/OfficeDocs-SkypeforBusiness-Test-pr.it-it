---
title: Creare o modificare una raccolta di impostazioni per la configurazione dell'aggiornamento dispositivi
TOCTitle: Creare o modificare una raccolta di impostazioni per la configurazione dell'aggiornamento dispositivi
ms:assetid: 3e8ce95f-a8c8-417c-b1f7-0f759a567aff
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994029(v=OCS.15)
ms:contentKeyID: 52062135
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare una raccolta di impostazioni per la configurazione dell'aggiornamento dispositivi

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Le impostazioni di configurazione dell'aggiornamento dei dispositivi possono essere create solo nell'ambio del sito tramite Windows PowerShell e il cmdlet **New-CsDeviceUpdateConfiguration** e modificate tramite il cmdlet **Set-CsDeviceUpdateConfiguration**. Questi cmdlet possono essere eseguiti da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell.


> [!NOTE]
> Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</A>.




## Per creare impostazioni di configurazione dell'aggiornamento dei dispositivi che utilizzano i valori predefiniti

  - Il comando seguente crea un nuovo set di impostazioni di configurazione di aggiornamento dei dispositivi per il sito Redmond:
    
        New-CsDeviceUpdateConfiguration -Identity "site:Redmond"
    
    Poiché nel comando precedente non sono stati specificati parametri, eccetto il parametro obbligatorio Identity, la nuova raccolta di impostazioni di configurazione utilizzerà i valori predefiniti per le relative proprietà.

## Come modificare il valore di una singola proprietà durante la creazione di impostazioni di configurazione dell'aggiornamento dei dispositivi

  - Per creare impostazioni che utilizzano diversi valori di proprietà, è sufficiente includere il parametro e il valore del parametro appropriati. Ad esempio, per creare una raccolta di impostazioni di configurazione dell'aggiornamento dei dispositivi che, per impostazione predefinita, eliminano i file di log esistenti ogni 21 giorni, utilizzare un comando come il seguente:
    
        New-CsDeviceUpdateConfiguration -Identity "site:Redmond" -LogCleanupInterval "21.00:00:00"

## Per modificare i valori di più proprietà durante la creazione di impostazioni di configurazione dell'aggiornamento dei dispositivi

  - Per modificare più valori di proprietà, è possibile includere più parametri nel comando. Ad esempio, questo comando imposta l'intervallo di pulizia del log su 21 giorni e l'intervallo di scaricamento del log su 30 minuti:
    
        New-CsDeviceUpdateConfiguration -Identity "site:Redmond" -LogCleanupInterval "21.00:00:00" -LogFlushInterval "00:30:00"

Per informazioni dettagliate sulla modifica delle impostazioni di configurazione dei dispositivi esistenti, vedere l'argomento della Guida per il cmdlet [Set-CsDeviceUpdateConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsDeviceUpdateConfiguration). Per informazioni dettagliate sulla creazione di raccolte di impostazioni di configurazione, vedere l'argomento della Guida per il cmdlet [New-CsDeviceUpdateConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsDeviceUpdateConfiguration).

