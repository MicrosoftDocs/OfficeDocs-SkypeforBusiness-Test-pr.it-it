---
title: Ottenere informazioni sul tenant di Lync Online
TOCTitle: Ottenere informazioni sul tenant di Lync Online
ms:assetid: 06467515-9114-45bb-8d09-26a915c3fc4d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362768(v=OCS.15)
ms:contentKeyID: 56269881
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ottenere informazioni sul tenant di Lync Online

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Per ottenere informazioni sul tenant di Skype for Business online, chiamare il cmdlet [Get-CsTenant](get-cstenant.md) senza parametri aggiuntivi:

    Get-CsTenant

Per ottenere solo il nome e l'ID del tenant (il valore del parametro TenantID è obbligatorio quando si eseguono cmdlet come [Set-CsTenantPublicProvider](set-cstenantpublicprovider.md) e [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)), usare il comando seguente:

    Get-CsTenant | Select-Object Name, TenantID

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

