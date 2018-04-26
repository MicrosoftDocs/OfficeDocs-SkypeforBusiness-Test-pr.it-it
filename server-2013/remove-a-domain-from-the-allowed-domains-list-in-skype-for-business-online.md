---
title: Rimuovere un dominio dall'elenco dei domini consentiti
TOCTitle: Rimuovere un dominio dall'elenco dei domini consentiti
ms:assetid: 04948582-363b-49bd-8305-166c4c1d0dd9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362766(v=OCS.15)
ms:contentKeyID: 56269879
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rimuovere un dominio dall'elenco dei domini consentiti

 

_**Ultima modifica dell'argomento:** 2015-06-22_

La rimozione di un dominio dall'elenco dei domini consentiti comporta una serie di passaggi. Il primo consiste nell'usare un comando simile al seguente per recuperare una raccolta di tutti i domini attualmente inclusi nell'elenco:

    $x = (Get-CsTenantFederationConfiguration).AllowedDomains

Eseguire quindi il comando seguente per esaminare i domini:

``` 
$x
```

Prendere nota della posizione numerica del dominio da rimuovere. Se è il primo nell'elenco dei domini, il relativo valore di indice è 0, se è il secondo il valore di indice è 1 e così via.

Dopo avere individuato il numero di indice, usare un comando analogo al seguente per rimuovere il dominio specificato, accertandosi di usare il numero di indice corretto. Questo comando rimuove il primo dominio nell'elenco (numero di indice 0):

    $x.AllowedDomain.RemoveAt(0)

Chiamare infine il cmdlet [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) cmdlet per scrivere le modifiche in Skype for Business online:

    Set-CsTenantFederationConfiguration -AllowedDomains $x

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

