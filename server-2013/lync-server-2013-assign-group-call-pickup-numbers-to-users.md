---
title: Assegnare numeri di risposta alle chiamate di gruppo agli utenti
TOCTitle: Assegnare numeri di risposta alle chiamate di gruppo agli utenti
ms:assetid: b8e79275-8e7e-4799-b908-f34f61df22f0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945647(v=OCS.15)
ms:contentKeyID: 52062296
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Assegnare numeri di risposta alle chiamate di gruppo agli utenti

 

_**Ultima modifica dell'argomento:** 2013-01-30_

Dopo aver aggiunto alla tabella dei codici orbit del parcheggio di chiamata i numeri dei gruppi di risposta alle chiamate di gruppo, è possibile assegnare i gruppi agli utenti. Utilizzare lo strumento del Resource Kit SEFAUtil (Secondary Extension Feature Activation) per assegnare agli utenti i gruppi di risposta alle chiamate.


> [!NOTE]
> In una distribuzione ibrida, non assegnare un gruppo di risposta alle chiamate di gruppo a utenti ospitati online. Gli utenti ospitati online non possono partecipare alla risposta alle chiamate di gruppo. In altre parole, non possono rispondere alle chiamate indirizzate ad altri utenti e gli altri utenti non possono rispondere alle chiamate indirizzate a loro.



## Per assegnare a un utente un gruppo di risposta alle chiamate di gruppo

1.  Accedere al computer in cui è stato installato lo strumento SEFAUtil con diritti di amministratore.

2.  Nella riga di comando digitare il comando seguente:
    
        SEFAUtil.exe sip:<sip address of user> /server:<pool FQDN> /enablegrouppickup:<group number>
    
    Ad esempio:
    
        SEFAUtil.exe katarina@contoso.com /server:pool01.contoso.com /enablegrouppickup:199

## Vedere anche

#### Attività

[Abilitare la risposta alle chiamate di gruppo per gli utenti](lync-server-2013-enable-group-call-pickup-for-users.md)  
[Disabilitare la risposta alle chiamate di gruppo per gli utenti](lync-server-2013-disable-group-call-pickup-for-users.md)

