---
title: Visualizzare i domini nell'elenco di domini consentiti
TOCTitle: Visualizzare i domini nell'elenco di domini consentiti
ms:assetid: 13bceaba-5c4f-431f-864f-9e374cafa986
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362772(v=OCS.15)
ms:contentKeyID: 56269884
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare i domini nell'elenco di domini consentiti

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Per visualizzare tutti i domini nell'elenco di domini consentiti, usare [Get-CsTenantFederationConfiguration](get-cstenantfederationconfiguration.md) e la sintassi seguente:

    Get-CsTenantFederationConfiguration | Select-Object -ExpandProperty AllowedDomains | Select-Object AllowedDomain

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

