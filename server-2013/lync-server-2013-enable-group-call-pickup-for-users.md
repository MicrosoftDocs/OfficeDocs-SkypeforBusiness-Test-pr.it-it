---
title: Abilitare la risposta alle chiamate di gruppo per gli utenti
TOCTitle: Abilitare la risposta alle chiamate di gruppo per gli utenti
ms:assetid: 20ec5f41-6ba2-4156-82ed-b91d05b62a6d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945620(v=OCS.15)
ms:contentKeyID: 52062111
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare la risposta alle chiamate di gruppo per gli utenti

 

_**Ultima modifica dell'argomento:** 2013-01-30_

Utilizzare lo strumento SEFAUtil del Resource Kit per abilitare la risposta alle chiamate di gruppo per gli utenti. Per abilitare la risposta alle chiamate di gruppo, agli utenti deve essere assegnato un numero di gruppo con tipo GroupPickup nella tabella dei codici orbit del parcheggio di chiamata. Assegnare un numero per la risposta alle chiamate di gruppo e allo stesso tempo abilitare la risposta alle chiamate di gruppo utilizzando il parametro /enablegrouppickup quando si esegue SEFAUtil.exe.

## Per abilitare la risposta alle chiamate di gruppo per un utente

1.  Accedere al computer in cui è stato installato lo strumento SEFAUtil con diritti di amministratore.

2.  Nella riga di comando digitare il comando seguente:
    
        SEFAUtil.exe sip:<sip address of user> /server:<pool FQDN> /enablegrouppickup:<group number>
    
    Ad esempio:
    
        SEFAUtil.exe katarina@contoso.com /server:pool01.contoso.com /enablegrouppickup:199

## Vedere anche

#### Attività

[Assegnare numeri di risposta alle chiamate di gruppo agli utenti](lync-server-2013-assign-group-call-pickup-numbers-to-users.md)  
[Disabilitare la risposta alle chiamate di gruppo per gli utenti](lync-server-2013-disable-group-call-pickup-for-users.md)

