---
title: Abilitare o disabilitare la registrazione delle conferenze
TOCTitle: Abilitare o disabilitare la registrazione delle conferenze
ms:assetid: f6c5afab-081c-495c-97f7-135dcc2f6085
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362857(v=OCS.15)
ms:contentKeyID: 56269994
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare o disabilitare la registrazione delle conferenze

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Se si vuole impedire agli utenti di registrare conferenze online, usare il cmdlet [Set-CsMeetingConfiguration](set-csmeetingconfiguration.md) e impostare il valore del parametro AllowConferenceRecording su False ($False):

    Set-CsMeetingConfiguration -AllowConferenceRecording $False

Per consentire nuovamente agli utenti di registrare conferenze online, impostare il valore del parametro AllowConferenceRecording su True ($True):

    Set-CsMeetingConfiguration -AllowConferenceRecording $True

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

