---
title: Get-CsAddressBookConfiguration per la gestione della rubrica
TOCTitle: Get-CsAddressBookConfiguration per la gestione della rubrica
ms:assetid: bd62f916-caf3-4e10-ada4-631bbb331ef1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429721(v=OCS.15)
ms:contentKeyID: 49301812
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAddressBookConfiguration per la gestione della rubrica

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Utenti autorizzati a eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire localmente il cmdlet Get-CsAddressBookConfiguration: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli del controllo di accesso basato sui ruoli creati personalmente), al prompt di Windows PowerShell eseguire il comando seguente:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Get-CsAddressBookConfiguration"}

Il cmdlet Get-CsAddressBookConfiguration restituisce informazioni su una configurazione già esistente.

Ad esempio:

    Get-CsAddressBookConfiguration -Identity site:Redmond

Combinando le funzionalità di Get-CsAddressBookConfiguration e Set-CsAddressBookConfiguration, l'amministratore ha la possibilità di definire quali configurazioni modificare e quindi applicare le modifiche. Questi comandi combinati, ad esempio:

    Get-CsAddressBookConfiguration -Filter site:* | Set-CsAddressBookConfiguration -RunTimeOfDay 23:00

restituiscono tutte le configurazioni in tutti i siti e quindi applicano il valore RunTimeOfDay 23.00 alle configurazioni.

Per una descrizione dettagliata del comando completo, fare riferimento all'argomento seguente nella documentazione di riferimento principale per i cmdlet RTC di Windows PowerShell per Lync Server.

## Vedere anche

#### Ulteriori risorse

[Get-CsAddressBookConfiguration](get-csaddressbookconfiguration.md)

