---
title: Rimuovere un dominio dall'elenco dei domini bloccati
TOCTitle: Rimuovere un dominio dall'elenco dei domini bloccati
ms:assetid: a11ea475-bb8b-44be-a5a5-4abb2fed42b8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362830(v=OCS.15)
ms:contentKeyID: 56269967
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rimuovere un dominio dall'elenco dei domini bloccati

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Per rimuovere un dominio dall'elenco dei domini bloccati sono necessarie due operazioni. La prima consiste nell'usare il cmdlet [New-CsEdgeDomainPattern](new-csedgedomainpattern.md) per creare un oggetto dominio per il dominio da rimuovere:

    $x = New-CsEdgeDomainPattern "fabrikam.com"

Dopo aver creato l'oggetto, usare la sintassi seguente per rimuovere il dominio (in questo esempio, il dominio memorizzato nella variabile $x) dall'elenco dei domini bloccati:

    Set-CsTenantFederationConfiguration -BlockedDomains @{Remove=$x}

Per rimuovere tutti i domini dall'elenco dei domini bloccati, impostare il valore della proprietà BlockedDomains su null ($Null):

    Set-CsTenantFederationConfiguration -BlockedDomains $Null

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

