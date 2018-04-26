---
title: "Lync Online: Aggiungere un dominio all'elenco dei domini bloccati"
TOCTitle: Aggiungere un dominio all'elenco dei domini bloccati
ms:assetid: ea6ebeea-3031-4c42-9a2c-88eaab790636
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362853(v=OCS.15)
ms:contentKeyID: 56269993
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aggiungere un dominio all'elenco dei domini bloccati in Lync Online

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Per aggiungere un dominio all'elenco dei domini bloccati, usare una sintassi simile alla seguente:

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -BlockedDomains @{Add=$x}

Come si può vedere, questo comando richiede due passaggi. Prima si usza [New-CsEdgeDomainPattern](new-csedgedomainpattern.md) per creare un oggetto dominio che rappresenta il dominio da aggiungere all'elenco dei domini bloccati. Quindi, si usa il cmdlet [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) e il metodo Add per aggiungere il dominio all'elenco. In questo esempio, si tratta del dominio archiviato nella variabile $x.

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

