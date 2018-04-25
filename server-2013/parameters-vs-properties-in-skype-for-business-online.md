---
title: Parametri e proprietà
TOCTitle: Parametri e proprietà
ms:assetid: 65348f95-f4d4-40cd-8869-f9d72643792d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362796(v=OCS.15)
ms:contentKeyID: 56269924
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Parametri e proprietà

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Durante la consultazione degli argomenti della Guida relativi ai cmdlet di Skype for Business online, si noterà come a volte i termini *parametro* e *proprietà* vengono usati in modo intercambiabile. Questo uso della terminologia non deve creare confusione: sebbene i due termini siano tecnicamente diversi, in Skype for Business online si riferiscono essenzialmente alla stessa cosa.

Dal punto di vista tecnico, i parametri vengono usati per eseguire cmdlet. Nel seguente comando di Windows PowerShell, ad esempio, EnableMicrosoftPushNotificationService e EnableApplePushNotificationService sono parametri del cmdlet [Set-CsPushNotificationConfiguration](set-cspushnotificationconfiguration.md):

    Set-CsPushNotificationConfiguration -EnableMicrosoftPushNotificationService -EnableApplePushNotificationService $True

Una proprietà è un attributo di un oggetto di Skype for Business online, ad esempio una raccolta di impostazioni di configurazione per notifiche Push. Si consideri ad esempio il comando:

    Set-CsPushNotificationConfiguration

Quando si esegue il comando, viene visualizzata una raccolta di proprietà con i valori associati, che includono gli elementi seguenti:

    EnableMicrosoftPushNotificationService : True
    EnableApplePushNotificationService     : True

Come si può vedere, proprietà e parametri condividono lo stesso nome: si usa il parametro EnableMicrosoftPushNotificationService per configurare il valore della proprietà EnableMicrosoftPushNotificationService.

## Vedere anche

#### Concetti

[Introduzione a Windows PowerShell e Lync Online](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

