---
title: Abilitare o disabilitare la federazione con provider di messaggistica istantanea pubblici
TOCTitle: Abilitare o disabilitare la federazione con provider di messaggistica istantanea pubblici
ms:assetid: 8609682c-97d3-48e6-a243-d84c1f9c8419
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362809(v=OCS.15)
ms:contentKeyID: 56269936
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare o disabilitare la federazione con provider di messaggistica istantanea pubblici

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Per consentire agli utenti dell'organizzazione di comunicare con utenti che dispongono di account presso provider di messaggistica istantanea pubblici, usare il cmdlet [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) e impostare la proprietà AllowPublicUsers su True($True):

    Set-CsTenantFederationConfiguration -AllowPublicUsers $True

Tenere presente che in seguito sarà necessario usare il cmdlet [Set-CsTenantPublicProvider](set-cstenantpublicprovider.md) per specificare i provider di messaggistica istantanea pubblici con cui gli utenti sono autorizzati a comunicare.

Per disabilitare la federazione con i provider pubblici, impostare nuovamente la proprietà AllowPublicUsers su false ($False):

    Set-CsTenantFederationConfiguration -AllowPublicUsers $False

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

