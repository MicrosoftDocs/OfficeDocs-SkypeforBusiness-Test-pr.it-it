---
title: L'utente non dispone delle autorizzazioni per la gestione del tenant
TOCTitle: L'utente non dispone delle autorizzazioni per la gestione del tenant
ms:assetid: 714ccf81-9451-4585-b62d-979f2a606315
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362812(v=OCS.15)
ms:contentKeyID: 56269930
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# L'utente non dispone delle autorizzazioni per la gestione del tenant

 

_**Ultima modifica dell'argomento:** 2015-06-22_

A meno che non si faccia parte del gruppo di amministratori del tenant, non è possibile stabilire una connessione remota di Windows PowerShell a Skype for Business online. Se non si è membri di questo gruppo, il tentativo di connessione non riuscirà e verrà visualizzato il messaggio di errore seguente:

    New-PSSession : [admin.vdomain.com] Elaborazione dei dati provenienti dal server remoto admin.vdomain.com non riuscita con il seguente messaggio di errore: L'utente 'user@foo.com' non dispone dell'autorizzazione per gestire questo tenant. È possibile concedere autorizzazioni assegnando l'utente al ruolo Controllo degli accessi in base al ruolo appropriato. Per ulteriori informazioni, vedere l'argomento della Guida about_Remote_Troubleshooting.

Se si ritiene di essere, o di dover essere, un membro del gruppo degli amministratori del tenant, contattare il supporto tecnico di Office 365.

## Vedere anche

#### Concetti

[Diagnosi e risoluzione dei problemi di connessione di Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

