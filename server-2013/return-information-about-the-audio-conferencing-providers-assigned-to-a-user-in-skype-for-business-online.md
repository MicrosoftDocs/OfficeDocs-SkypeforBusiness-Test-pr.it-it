---
title: Ottenere informazioni sui provider di servizi di audioconferenza assegnati a un utente
TOCTitle: Ottenere informazioni sui provider di servizi di audioconferenza assegnati a un utente
ms:assetid: 7fae822f-9f6c-4381-95c5-879661027925
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362814(v=OCS.15)
ms:contentKeyID: 56269943
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ottenere informazioni sui provider di servizi di audioconferenza assegnati a un utente

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Per ottenere informazioni sui provider di servizi di audioconferenza assegnati a un utente, usare il cmdlet [Get-CsUserAcp](get-csuseracp.md) con la sintassi seguente:

    Get-CsUserAcp -Identity "Ken Myer" | Select-Object -ExpandProperty AcpInfo

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

