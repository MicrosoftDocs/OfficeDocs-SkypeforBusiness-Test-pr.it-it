---
title: Testare il server Chat persistente con una transazione sintetica
TOCTitle: Testare il server Chat persistente con una transazione sintetica
ms:assetid: 414e43f3-0074-4ecf-a232-398de972cb24
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204837(v=OCS.15)
ms:contentKeyID: 49300333
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Testare il server Chat persistente con una transazione sintetica

 

_**Ultima modifica dell'argomento:** 2012-09-21_

Per testare il server Chat persistente per l'invio e la ricezione di messaggi in una chat room tra due utenti

    Test-CsPersistentChatMessage [-Authentication <TrustedServer | Negotiate | ClientCertificate | 
        LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] -TargetFqdn <String> [-Force <SwitchParameter>] [-OutLoggerVariable <String>] 
        [-OutVerboseVariable <String>] [<CommonParameters>]

oppure

    Test-CsPersistentChatMessage [-Authentication <TrustedServer | Negotiate | ClientCertificate | 
        LiveID>] -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> [-RegistrarPort 
        <Int32>] -SenderCredential <PSCredential> -SenderSipAddress <String> [-TargetFqdn <String>] [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [<CommonParameters>]

oppure

    Test-CsPersistentChatMessage [-Authentication <TrustedServer | Negotiate | ClientCertificate | 
        LiveID>] [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable 
        <String>] [<CommonParameters>]

