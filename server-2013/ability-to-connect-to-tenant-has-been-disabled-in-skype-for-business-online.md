---
title: La possibilità di connettersi al tenant è stata disabilitata
TOCTitle: La possibilità di connettersi al tenant è stata disabilitata
ms:assetid: 7365d31b-173e-4339-b0a3-98ab73a9558f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362820(v=OCS.15)
ms:contentKeyID: 56269941
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# La possibilità di connettersi al tenant è stata disabilitata

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Per poter usare Windows PowerShell per la gestione di Skype for Business online, è necessario che la proprietà EnableRemotePowerShellAccess del criterio del tenant di Windows PowerShell in uso sia impostata su True. In caso contrario, la connessione non riesce e viene visualizzato un messaggio di errore simile al seguente:

    New-PSSession: [admin.vdomain.com] Elaborazione dei dati provenienti dal server remoto admin.vdomain.com non riuscita con il seguente messaggio di errore: La possibilità di connettersi a questo tenant mediante una sessione remota di PowerShell è stata disabilitata. Consultare la Guida di Lync per controllare i criteri di PowerShell per il tenant. Per ulteriori informazioni, vedere l'argomento della Guida about_Remote_Troubleshooting.

Se viene visualizzato questo messaggio di errore, contattare il supporto tecnico di Office 365 per richiedere l'abilitazione dell'accesso remoto a Windows PowerShell.

## Vedere anche

#### Concetti

[Diagnosi e risoluzione dei problemi di connessione di Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

