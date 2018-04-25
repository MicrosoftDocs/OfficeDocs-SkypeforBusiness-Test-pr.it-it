---
title: Disabilitare la risposta alle chiamate di gruppo per gli utenti
TOCTitle: Disabilitare la risposta alle chiamate di gruppo per gli utenti
ms:assetid: 91b06f9e-2840-45a2-bbb3-6a29179b9a9f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945638(v=OCS.15)
ms:contentKeyID: 52062200
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disabilitare la risposta alle chiamate di gruppo per gli utenti

 

_**Ultima modifica dell'argomento:** 2013-01-30_

Utilizzare la procedura seguente per disabilitare la risposta alle chiamate di gruppo per un utente.


> [!NOTE]
> Quando si disabilita la risposta alle chiamate di gruppo per un utente, il numero del gruppo per la risposta alle chiamate di gruppo assegnato all'utente non viene conservato. Se in seguito si desidera riabilitare la risposta alle chiamate di gruppo per tale utente, è necessario assegnare di nuovo il numero con il parametro /enablegrouppickup.



## Per disabilitare la risposta alle chiamate di gruppo per un utente

1.  Accedere al computer in cui è stato installato lo strumento SEFAUtil con diritti di amministratore.

2.  Nella riga di comando, eseguire:
    
        SEFAUtil.exe sip:<sip address of user> /server:<pool FQDN> /disablegrouppickup
    
    Ad esempio:
    
        SEFAUtil.exe katarina@contoso.com /server:pool01.contoso.com /disablegrouppickup

## Vedere anche

#### Attività

[Assegnare numeri di risposta alle chiamate di gruppo agli utenti](lync-server-2013-assign-group-call-pickup-numbers-to-users.md)  
[Abilitare la risposta alle chiamate di gruppo per gli utenti](lync-server-2013-enable-group-call-pickup-for-users.md)

