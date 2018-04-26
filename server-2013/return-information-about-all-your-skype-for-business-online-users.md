---
title: Ottenere informazioni su tutti gli utenti di Lync Online
TOCTitle: Ottenere informazioni su tutti gli utenti di Lync Online
ms:assetid: 0b59fadf-67e6-48ea-86f1-2efef500ebdf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362769(v=OCS.15)
ms:contentKeyID: 56269885
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ottenere informazioni su tutti gli utenti di Lync Online

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Per ottenere informazioni su tutti gli utenti abilitati per Skype for Business online, chiamare il cmdlet [Get-CsOnlineUser](get-csonlineuser.md) senza parametri aggiuntivi:

    Get-CsOnlineUser

Per ottenere informazioni su un singolo utente selezionato casualmente, ad esempio per usare l'account a scopo di test, chiamare il cmdlet **Get-CsOnlineUser** e impostare il parametro ResultSize su 1:

    Get-CsOnlineUser -ResultSize 1

In questo modo il cmdlet **Get-CsOnlineUser** restituirà informazioni per un solo utente, indipendentemente dal numero di utenti presenti nell'organizzazione. Per ottenere informazioni per cinque utenti, impostare il valore del parametro ResultSize su 5:

    Get-CsOnlineUser -ResultSize 5

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

