---
title: "Lync Online: Aggiungere un dominio all'elenco dei domini consentiti"
TOCTitle: Aggiungere un dominio all'elenco dei domini consentiti
ms:assetid: 7b7f76c8-3047-40be-a938-8ac2868a6bc8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362818(v=OCS.15)
ms:contentKeyID: 56269928
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aggiungere un dominio all'elenco dei domini consentiti in Lync Online

 

_**Ultima modifica dell'argomento:** 2015-06-22_

L'aggiunta di un primo dominio all'elenco dei domini consentiti è un processo in tre passaggi. Usare innanzitutto il cmdlet [New-CsEdgeDomainPattern](new-csedgedomainpattern.md) per creare un oggetto dominio per il dominio da aggiungere:

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"

Usare quindi il cmdlet [New-CsEdgeAllowList](new-csedgeallowlist.md) per creare un nuovo elenco di domini consentiti che includa l'oggetto dominio:

    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x

Usare infine il cmdlet [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) per scrivere il nuovo elenco di domini consentiti in Skype for Business online:

    Set-CsTenantFederationConfiguration -AllowedDomains $newAllowList

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

