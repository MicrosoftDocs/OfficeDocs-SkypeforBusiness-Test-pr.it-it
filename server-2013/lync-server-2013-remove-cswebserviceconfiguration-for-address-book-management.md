---
title: Remove-CsWebServiceConfiguration per la gestione della rubrica
TOCTitle: Remove-CsWebServiceConfiguration per la gestione della rubrica
ms:assetid: 91947cad-5cdd-41b9-83e1-650703c55879
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429713(v=OCS.15)
ms:contentKeyID: 49301329
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsWebServiceConfiguration per la gestione della rubrica

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Utenti autorizzati a eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire localmente il cmdlet Remove-CsWebServiceConfiguration: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli del controllo di accesso basato sui ruoli creati personalmente), al prompt di Windows PowerShell eseguire il comando seguente:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Remove-CsWebServiceConfiguration"}

Il cmdlet Remove-CsWebServiceConfiguration consente all'amministratore di rimuovere una configurazione dei servizi Web. Il cmdlet non è in grado di rimuovere la configurazione dei servizi Web globale.

Ad esempio:

    Remove-CsWebServiceConfiguration -Identity site:Redmond

Per una descrizione dettagliata del comando completo, fare riferimento all'argomento seguente nella documentazione di riferimento principale per i cmdlet RTC di Windows PowerShell per Lync Server.

## Vedere anche

#### Ulteriori risorse

[Remove-CsWebServiceConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsWebServiceConfiguration)

