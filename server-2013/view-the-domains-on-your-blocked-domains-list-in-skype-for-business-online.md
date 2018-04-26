---
title: Visualizzare i domini nell'elenco dei domini bloccati
TOCTitle: Visualizzare i domini nell'elenco dei domini bloccati
ms:assetid: 67c65dbf-1a68-4c77-aabd-bed5001b4267
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362797(v=OCS.15)
ms:contentKeyID: 56269927
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare i domini nell'elenco dei domini bloccati

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Per visualizzare tutti i domini presenti nell'elenco dei domini bloccati, usare il cmdlet [Get-CsTenantFederationConfiguration](get-cstenantfederationconfiguration.md), quindi inviare i dati restituiti tramite pipe al cmdlet **Select-Object**

    Get-CsTenantFederationConfiguration | Select-Object -ExpandProperty BlockedDomains

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

