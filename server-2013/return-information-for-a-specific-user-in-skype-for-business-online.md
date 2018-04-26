---
title: Ottenere informazioni su un utente specifico
TOCTitle: Ottenere informazioni su un utente specifico
ms:assetid: 6c8c2190-8e62-4f92-bbe9-4f692bd7ebf5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362803(v=OCS.15)
ms:contentKeyID: 56269923
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ottenere informazioni su un utente specifico

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Esistono diversi modi per fare riferimento a un account utente specifico quando si usa il cmdlet [Get-CsOnlineUser](get-csonlineuser.md). È possibile usare il nome visualizzato Servizi di dominio Active Directory dell'utente:

    Get-CsOnlineUser -Identity "Ken Myer"

È possibile usare l'indirizzo SIP dell'utente:

    Get-CsOnlineUser -Identity "sip:kenmyer@litwareinc.com"

Oppure, è possibile usare il nome dell'entità utente (UPN) per l'utente:

    Get-CsOnlineUser -Identity "kenmyer@litwareinc.com"

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

