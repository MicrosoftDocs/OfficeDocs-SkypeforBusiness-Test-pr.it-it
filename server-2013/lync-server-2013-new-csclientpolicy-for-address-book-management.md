---
title: New-CsClientPolicy per la gestione della rubrica
TOCTitle: New-CsClientPolicy per la gestione della rubrica
ms:assetid: ef4415fc-82c4-4dc8-97d1-37a084553343
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429726(v=OCS.15)
ms:contentKeyID: 49302409
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClientPolicy per la gestione della rubrica

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Utenti autorizzati a eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire localmente il cmdlet New-CsClientPolicy: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli del controllo di accesso basato sui ruoli creati personalmente), al prompt di Windows PowerShell eseguire il comando seguente:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "New-CsClientPolicy"}

Il cmdlet New-CsClientPolicy definisce un numero elevato di impostazioni per il provisioning dei client per le caratteristiche disponibili in Lync Server 2013. Per il servizio Rubrica, è importante il parametro AddressBookAvailability, che influisce direttamente sulle opzioni disponibili per i client e prevede tre opzioni possibili:

  - WebSearchAndFileDownload

  - WebSearchOnly

  - FileDownloadOnly

Se definito, questo parametro determina la modalità di accesso dei client alla Rubrica. Insieme al parametro è necessario definire una delle opzioni. Se questa impostazione non viene modificata, rimarrà effettiva l'impostazione predefinita WebSearchAndFileDownload.

Ad esempio:

    New-CsClientPolicy -Identity RedmondClientPolicy -DisableCalendarPresence $True -DisablePhonePresence $True -DisplayPhoto "PhotosFromADOnly" -AddressBookAvailability "WebSearchOnly"

## Vedere anche

#### Ulteriori risorse

[New-CsClientPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClientPolicy)

