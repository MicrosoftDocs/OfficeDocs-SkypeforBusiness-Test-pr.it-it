---
title: Rimuovere un provider di servizi di audioconferenza precedentemente assegnato a un utente
TOCTitle: Rimuovere un provider di servizi di audioconferenza precedentemente assegnato a un utente
ms:assetid: 85d59e6c-d646-4908-9767-adb48763f6de
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362808(v=OCS.15)
ms:contentKeyID: 56269935
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rimuovere un provider di servizi di audioconferenza precedentemente assegnato a un utente

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Per rimuovere tutti i provider di servizi di audioconferenza assegnati a un utente, eseguire il cmdlet [Remove-CsUserAcp](remove-csuseracp.md) senza alcun parametro tranne il parametro Identity, che indica l'utente in questione:

    Remove-CsUserAcp -Identity "Ken Myer"

Se a un utente sono stati assegnati più provider di servizi di audioconferenza, è possibile rimuovere un singolo provider includendo il parametro Name, seguito dal provider da rimuovere:

    Remove-CsUserAcp -Identity "Ken Myer" -Name "Contoso ACP"

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

