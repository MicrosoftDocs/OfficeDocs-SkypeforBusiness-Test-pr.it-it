---
title: Assegnare un provider di servizi di audioconferenza a un utente
TOCTitle: Assegnare un provider di servizi di audioconferenza a un utente
ms:assetid: 60db6896-9c5c-4d64-ab7e-10d91748587c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362791(v=OCS.15)
ms:contentKeyID: 56269913
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Assegnare un provider di servizi di audioconferenza a un utente

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Il cmdlet [Set-CsUserAcp](set-csuseracp.md) consente di assegnare un provider di servizi di audioconferenza a un utente:

    Set-CsUserAcp -Identity "Ken Myer" -TollNumber "12065551219" -TollFreeNumbers "18005550712" -ParticipantPasscode "p@ssw0rd" -Domain "sip.contoso.com" -Name "Contoso ACP"

Questa assegnazione non avrà alcun effetto a meno che non sia già stato stipulato un contratto con il provider specificato.

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

