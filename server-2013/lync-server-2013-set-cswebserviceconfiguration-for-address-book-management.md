---
title: Set-CsWebServiceConfiguration per la gestione della rubrica
TOCTitle: Set-CsWebServiceConfiguration per la gestione della rubrica
ms:assetid: 79d0edf5-23f3-4845-a7b7-e11b5a928bab
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429709(v=OCS.15)
ms:contentKeyID: 49301060
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsWebServiceConfiguration per la gestione della rubrica

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Chi può eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet Set-CsWebServiceConfiguration in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli di controllo di accesso basati sui ruoli a cui è stato assegnato questo cmdlet, inclusi tutti gli eventuali ruoli di controllo di accesso basati sui ruoli creati personalmente, eseguire il comando seguente al prompt di Windows PowerShell:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Set-CsWebServiceConfiguration"}

Il cmdlet Set-CsWebServiceConfiguration consente all'amministratore di ridefinire un attributo esistente nella configurazione dei servizi Web.

Ad esempio:

    Set-CsWebServiceConfiguration -Identity site:Redmond -EnableGroupExpansion $True

Per una descrizione dettagliata del comando completo, vedere le informazioni seguenti nella documentazione di riferimento principale su RTCCmdlets di Lync Server Windows PowerShell.

## Vedere anche

#### Ulteriori risorse

[Set-CsWebServiceConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsWebServiceConfiguration)

