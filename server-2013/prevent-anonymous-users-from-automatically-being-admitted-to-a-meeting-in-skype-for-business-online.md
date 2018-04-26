---
title: Impedire a utenti anonimi di essere ammessi automaticamente a una riunione
TOCTitle: Impedire a utenti anonimi di essere ammessi automaticamente a una riunione
ms:assetid: 23f120d2-4c39-4509-aa1f-4d186a525075
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362775(v=OCS.15)
ms:contentKeyID: 56269888
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Impedire a utenti anonimi di essere ammessi automaticamente a una riunione

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Per impedire a utenti anonimi di essere ammessi automaticamente a una riunione online, usare il cmdlet [Set-CsMeetingConfiguration](set-csmeetingconfiguration.md) e impostare la proprietà AdmitAnonymousUsersByDefault su False ($False):

    Set-CsMeetingConfiguration -AdmitAnonymousUsersByDefault $False

Per abilitare l'ammissione automatica, impostare di nuovo la proprietà AdmitAnonymousUsersByDefault su True ($True):

    Set-CsMeetingConfiguration -AdmitAnonymousUsersByDefault $True

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

