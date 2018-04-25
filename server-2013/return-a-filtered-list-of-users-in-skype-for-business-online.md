---
title: Visualizzare un elenco di utenti filtrato
TOCTitle: Visualizzare un elenco di utenti filtrato
ms:assetid: f2c4d13b-8601-4192-8b94-e9a57969da11
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362858(v=OCS.15)
ms:contentKeyID: 56269995
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare un elenco di utenti filtrato

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Mediante il cmdlet [Get-CsOnlineUser](get-csonlineuser.md) e il parametro LdapFilter o Filter è possibile recuperare facilmente informazioni su un set di utenti specifico. Ad esempio, questo comando restituisce tutti gli utenti che lavorano nel reparto Finance:

    Get-CsOnlineUser -LdapFilter "department=Finance"

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

