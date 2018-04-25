---
title: Ottenere informazioni sui provider di servizi di audioconferenza
TOCTitle: Ottenere informazioni sui provider di servizi di audioconferenza
ms:assetid: df9c8fc0-8bb6-4416-a5cc-aa9b1601a688
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362848(v=OCS.15)
ms:contentKeyID: 56269986
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ottenere informazioni sui provider di servizi di audioconferenza

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Per ottenere informazioni sui provider di servizi di audioconferenza assegnati a un utente, usare il cmdlet [Get-CsUserAcp](get-csuseracp.md) con la sintassi seguente:

    Get-CsUserAcp -Identity "Ken Myer" | Select-Object -ExpandProperty AcpInfo

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

