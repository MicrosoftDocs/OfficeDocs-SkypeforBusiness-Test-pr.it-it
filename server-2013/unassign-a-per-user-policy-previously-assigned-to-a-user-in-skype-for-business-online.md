---
title: Rimozione di un criterio per utente precedentemente assegnato a un utente
TOCTitle: Rimozione di un criterio per utente precedentemente assegnato a un utente
ms:assetid: bdba1d22-28e4-4203-a109-a3fb408783d3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362840(v=OCS.15)
ms:contentKeyID: 56269977
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rimozione di un criterio per utente precedentemente assegnato a un utente

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Per rimuovere un criterio per utente precedentemente assegnato a un utente, eseguire di nuovo il cmdlet **Grant-Cs** appropriato (ad esempio il cmdlet [Grant-CsVoicePolicy](grant-csvoicepolicy.md) per rimuovere l'assegnazione di un criterio vocale), quindi impostare il parametro PolicyName su un valore null ($Null):

    Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName $Null

Per rimuovere l'assegnazione di criteri vocali da tutti gli utenti, usare il comando seguente:

    Get-CsOnlineUser | Grant-CsVoicePolicy -PolicyName $Null

Se si rimuove l'assegnazione di un criterio per un utente, l'utente verrà gestito dal criterio globale.

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

