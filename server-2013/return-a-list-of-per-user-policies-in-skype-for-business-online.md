---
title: Visualizzare un elenco di criteri per utente
TOCTitle: Visualizzare un elenco di criteri per utente
ms:assetid: e95a2755-3501-40cc-a704-5ecd01839d76
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362856(v=OCS.15)
ms:contentKeyID: 56269990
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare un elenco di criteri per utente

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Per visualizzare un elenco di criteri per utente, selezionare innanzitutto il cmdlet **Get-Cs** appropriato (ad esempio, il cmdlet [Get-CsVoicePolicy](get-csvoicepolicy.md) per recuperare i criteri vocali per utente). Usare quindi la sintassi seguente per fare in modo che venga restituito il parametro Identity per ogni criterio per utente:

    Get-CsVoicePolicy -Filter "tag:*" | Select-Object Identity

Tenere presente che, considerata l'esistenza di contratti di licenza diversi e di restrizioni differenti in base ai paesi e alle aree geografiche, potrebbe non essere consentita l'assegnazione a un particolare utente di determinati criteri per conferenze, accesso esterno o dispositivi mobili. Per verificare i criteri per utente che possono essere effettivamente assegnati a un determinato utente, ad esempio kenmyer@litwareinc.com, usare uno dei comandi seguenti e il parametro ApplicableTo nel modo appropriato:

    Get-CsConferencingPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsExternalAccessPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsMobilityPolicy -ApplicableTo "kenmyer@litwareinc.com"

La sintassi precedente restituisce solo i criteri per utente effettivamente assegnabili a Ken Myer.

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

