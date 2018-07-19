---
title: Set-CsClientPolicy per la gestione della rubrica
TOCTitle: Set-CsClientPolicy per la gestione della rubrica
ms:assetid: e7788bea-606f-481a-a3a4-1855ac028493
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429723(v=OCS.15)
ms:contentKeyID: 49302318
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClientPolicy per la gestione della rubrica

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Utenti autorizzati a eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire localmente il cmdlet Set-CsClientPolicy: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli del controllo di accesso basato sui ruoli creati personalmente), al prompt di Windows PowerShell eseguire il comando seguente:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Set-CsClientPolicy"}

In modo analogo a New-CsClientPolicy, il cmdlet Set-CsClientPolicy consente di modificare le impostazioni dei client già implementate.

Ad esempio:

    Set-CsClientPolicy -Identity RedmondClientPolicy -WebServicePollInterval "00:15:00" -AddressBookAvailability "WebSearchAndFileDownload"

Per una descrizione dettagliata del comando completo, fare riferimento all'argomento seguente nella documentazione di riferimento principale per i cmdlet RTC di Windows PowerShell per Lync Server.

## Vedere anche

#### Ulteriori risorse

[Set-CsClientPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClientPolicy)

