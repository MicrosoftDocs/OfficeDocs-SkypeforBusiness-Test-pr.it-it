---
title: "Lync Server 2013: Abilita risposta a chiamate di gruppo e assegna num. gruppo"
TOCTitle: "Lync Server 2013: Abilita risposta a chiamate di gruppo e assegna num. gruppo"
ms:assetid: c33bb6c2-d43b-4fb6-a0fa-6d82a7b09abe
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945650(v=OCS.15)
ms:contentKeyID: 52062307
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare la risposta alle chiamate di gruppo per gli utenti e assegnare un numero di gruppo

 

_**Ultima modifica dell'argomento:** 2013-01-30_

Dopo aver aggiunto i numeri dei gruppi di risposta alle chiamate alla tabella di codici orbit del parcheggio di chiamata, assegnare i numeri dei gruppi agli utenti e abilitare la risposta alle chiamate di gruppo. Utilizzare lo strumento del Resource Kit SEFAUtil (Secondary Extension Feature Activation) per assegnare i numeri dei gruppi e abilitare la risposta alle chiamate di gruppo.


> [!NOTE]
> In una distribuzione ibrida, non assegnare un gruppo di risposta alle chiamate di gruppo a utenti ospitati online. Gli utenti ospitati online non possono partecipare alla risposta alle chiamate di gruppo. In altre parole, non possono rispondere alle chiamate indirizzate ad altri utenti e gli altri utenti non possono rispondere alle chiamate indirizzate a loro.



## Per assegnare un numero di gruppo e abilitare la risposta alle chiamate di gruppo per un utente

1.  Accedere al computer in cui è stato installato lo strumento SEFAUtil con diritti di amministratore.

2.  Nella riga di comando digitare il comando seguente:
    
        SEFAUtil.exe sip:<sip address of user> /server:<pool FQDN> /enablegrouppickup:<group number>
    
    Ad esempio, per assegnare il numero di gruppo 199 a un utente:
    
        SEFAUtil.exe katarina@contoso.com /server:pool01.contoso.com /enablegrouppickup:199 

## Vedere anche

#### Attività

[Disabilitare la risposta alle chiamate di gruppo per gli utenti](lync-server-2013-disable-group-call-pickup-for-users.md)

