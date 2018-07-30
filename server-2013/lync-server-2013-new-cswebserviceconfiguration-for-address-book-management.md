---
title: New-CsWebServiceConfiguration per la gestione della rubrica
TOCTitle: New-CsWebServiceConfiguration per la gestione della rubrica
ms:assetid: 49e4ecc5-aa3e-4dd4-a32c-b0dea3758fab
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429703(v=OCS.15)
ms:contentKeyID: 49300424
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsWebServiceConfiguration per la gestione della rubrica

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Chi può eseguire questo cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet New-CsWebServiceConfiguration i membri dei gruppi seguenti: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli di Controllo dell'accesso basato sui ruoli (RBAC) a cui tale cmdlet è stato assegnato, inclusi i ruoli RBAC personalizzati creati personalmente, al prompt di Windows PowerShell eseguire il comando seguente:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "New-CsWebServiceConfiguration"}

Il cmdlet New-CsWebServiceConfiguration definisce una nuova configurazione per i servizi Web nell'organizzazione. L'ambito per la configurazione dei servizi Web può essere solo a livello di sito o di servizio. Non è possibile creare una nuova configurazione di servizi Web a livello globale. Per la Rubrica è di particolare interesse l'attributo EnableGroupExansion. Se impostato su True, i servizi Web possono rispondere alle richieste di espansione dei gruppi.

Ad esempio:

    New-CsWebServiceConfiguration -Identity site:Redmond -EnableGroupExpansion $False -UseCertificateAuth $True

Per una descrizione dettagliata del comando completo, fare riferimento all'argomento seguente nella documentazione di riferimento principale per i cmdlet RTC di Windows PowerShell per Lync Server.

## Vedere anche

#### Ulteriori risorse

[New-CsWebServiceConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsWebServiceConfiguration)

