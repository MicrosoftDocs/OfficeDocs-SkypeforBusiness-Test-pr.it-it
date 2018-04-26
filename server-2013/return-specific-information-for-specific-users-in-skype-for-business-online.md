---
title: Ottenere informazioni specifiche su utenti specifici
TOCTitle: Ottenere informazioni specifiche su utenti specifici
ms:assetid: bbee85bd-d8a7-4b28-90d7-45c43eee48f6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362838(v=OCS.15)
ms:contentKeyID: 56269974
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ottenere informazioni specifiche su utenti specifici

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Per impostazione predefinita, il cmdlet [Get-CsOnlineUser](get-csonlineuser.md) restituisce un'enorme quantità di informazioni per ogni account utente di Skype for Business online. Se si è interessati solo a una parte di queste informazioni, è necessario inviare una pipe dei dati restituiti al cmdlet **Select-Object**. Ad esempio, il comando seguente restituisce tutti i dati relativi all'utente Ken Myer, quindi usa il cmdlet **Select-Object** per limitare le informazioni visualizzate sullo schermo al dial plan e al nome visualizzato di Servizi di dominio Active Directory di Ken Myer:

    Get-CsOnlineUser -Identity "Ken Myer" | Select-Object DisplayName, DialPlan

Il comando seguente restituisce il nome visualizzato e il dial plan di tutti gli utenti.

    Get-CsOnlineUser | Select-Object DisplayName, DialPlan

Per trovare le proprietà di un account utente di Skype for Business online, usare questo comando:

    Get-CsOnlineUser | Get-Member

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

