---
title: Abilitare e disabilitare le notifiche Push per iPhone e Windows Phone
TOCTitle: Abilitare e disabilitare le notifiche Push per iPhone e Windows Phone
ms:assetid: 64482dcb-6354-4fb5-a2e4-1564b3d0e047
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362792(v=OCS.15)
ms:contentKeyID: 56269916
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare e disabilitare le notifiche Push per iPhone e Windows Phone

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Per disabilitare l'invio di notifiche Push a iPhone o Windows Phone, usare il cmdlet [Set-CsPushNotificationConfiguration](set-cspushnotificationconfiguration.md) e impostare i valori di EnableApplePushNotificationService e EnableMicrosoftPushNotificationService properties su False ($False):

    Set-CsPushNotificationConfiguration -EnableApplePushNotificationService $False -EnableMicrosoftPushNotificationService $False

Tenere presente che iPhone e Windows Phone possono essere impostati indipendentemente. Ad esempio, questo comando disabilita le notifiche Push su iPhone, ma le abilita su Windows Phone:

    Set-CsPushNotificationConfiguration -EnableApplePushNotificationService $False -EnableMicrosoftPushNotificationService $True

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

