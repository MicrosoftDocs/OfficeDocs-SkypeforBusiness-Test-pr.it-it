---
title: Set-CsAddressBookConfiguration per la gestione della rubrica
TOCTitle: Set-CsAddressBookConfiguration per la gestione della rubrica
ms:assetid: 3a64ceb1-9f79-4f3b-bf33-eaf346dbd60d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429700(v=OCS.15)
ms:contentKeyID: 49300255
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAddressBookConfiguration per la gestione della rubrica

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Chi può eseguire questo cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet Set-CsAddressBookConfiguration i membri dei gruppi seguenti: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli di Controllo dell'accesso basato sui ruoli (RBAC) a cui tale cmdlet è stato assegnato, inclusi i ruoli RBAC personalizzati creati personalmente, al prompt di Windows PowerShell eseguire il comando seguente:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Set-CsAddressBookConfiguration"}

Set-CsAddressBookConfiguration è simile al cmdlet New-CsAddressBookConfiguration, con la differenza che viene utilizzato per modificare una configurazione esistente.

Ad esempio:

    Set-CsAddressBookConfiguration -identity site:Redmond -RunTimeOfDay 23:00

Per una descrizione dettagliata del comando completo, vedere quanto segue nella guida di riferimento principale RTCCmdlets per Lync Server Windows PowerShell.

## Vedere anche

#### Ulteriori risorse

[Set-CsAddressBookConfiguration](set-csaddressbookconfiguration.md)

