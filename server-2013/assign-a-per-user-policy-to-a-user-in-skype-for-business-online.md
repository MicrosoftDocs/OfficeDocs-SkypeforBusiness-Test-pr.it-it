---
title: Assegnare un criterio per utente a un utente
TOCTitle: Assegnare un criterio per utente a un utente
ms:assetid: 37e07da7-6391-4d6d-a428-c70272897039
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362779(v=OCS.15)
ms:contentKeyID: 56269896
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Assegnare un criterio per utente a un utente

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Per assegnare un criterio per utente a un utente, è necessario prima di tutto selezionare il cmdlet **Grant-Cs** appropriato, ad esempio il cmdlet [Grant-CsVoicePolicy](grant-csvoicepolicy.md) se si desidera assegnare un criterio vocale per utente. Eseguire il cmdlet, accertandosi di specificare sia l'identità dell'utente a cui assegnare il criterio sia il nome del criterio da assegnare:

    Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName "RedmondVoicePolicy"

Per assegnare lo stesso criterio a tutti gli utenti, usare questa sintassi:

    Get-CsOnlineUser | Grant-CsVoicePolicy -PolicyName "RedmondVoicePolicy"

Tenere presente che, considerata l'esistenza di contratti di licenza diversi e di restrizioni differenti in base ai paesi e alle aree geografiche, potrebbe non essere consentita l'assegnazione a un particolare utente di determinati criteri per conferenze, accesso esterno o dispositivi mobili. Per verificare i criteri per utente che possono essere effettivamente assegnati a un determinato utente, ad esempio kenmyer@litwareinc.com, usare uno dei comandi seguenti e il parametro ApplicableTo nel modo appropriato:

    Get-CsConferencingPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsExternalAccessPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsMobilityPolicy -ApplicableTo "kenmyer@litwareinc.com"

La sintassi precedente restituisce solo i criteri per utente effettivamente assegnabili a Ken Myer.

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

