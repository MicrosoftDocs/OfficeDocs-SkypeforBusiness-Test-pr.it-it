---
title: 'Lync Server 2013: Strumenti di gestione di Windows PowerShell e Lync Server'
TOCTitle: Strumenti di gestione di Windows PowerShell e Lync Server 2013
ms:assetid: 6a285f7c-0ef5-4cab-9976-d03be276e35d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn481130(v=OCS.15)
ms:contentKeyID: 59679240
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Strumenti di gestione di Windows PowerShell e Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-10-21_

In Microsoft Lync Server 2013 gli strumenti di gestione vengono implementati utilizzando Windows PowerShell. Windows PowerShell include un ambiente della riga di comando, comandi per prodotti specifici e un linguaggio di scripting completo. Gli strumenti di Lync Server 2013 implementati utilizzando Windows PowerShell includono i seguenti:

  - **Generatore di topologie**. Generatore di topologie viene utilizzato per creare, regolare e pubblicare la topologia pianificata, nonché per convalidare la topologia prima delle installazioni dei server. Quando Lync Server 2013 viene installato nei singoli server, la topologia pubblicata viene letta dai server come parte del processo di installazione e il programma di installazione distribuisce quindi il server come indicato nella topologia. Al termine dell'installazione, le informazioni di configurazione vengono replicate automaticamente in tutti i server. È possibile aggiungere dei componenti alla distribuzione solo utilizzando Generatore di topologie.

  - **Lync Server Management Shell**. Lync Server Management Shell viene utilizzato per gestire la distribuzione interamente dalla riga di comando.

  - **Pannello di controllo di Lync Server**. L'interfaccia utente Pannello di controllo di Microsoft Lync Server 2013 viene utilizzata per gestire le attività più comuni nella distribuzione.

Questi strumenti utilizzano i cmdlet di Windows PowerShell per la gestione della distribuzione, inclusi circa 550 cmdlet per prodotti specifici. I cmdlet relativi alla sicurezza inclusi in Lync Server 2013 vengono utilizzati principalmente per gestire l'autenticazione, nonché le autorizzazioni e i diritti utente. È disponibile un'ampia gamma di cmdlet per la gestione dell'autenticazione, inclusi i cmdlet per l'autenticazione tramite certificato e PIN. Diversi cmdlet inoltre consentono di utilizzare la nuova funzionalità di controllo degli accessi in base al ruolo (RBAC) per delegare il controllo amministrativo di Lync Server 2013. Per informazioni dettagliate sui cmdlet di Lync Server, vedere [Lync Server Management Shell](lync-server-2013-lync-server-management-shell.md) nella documentazione relativa alle operazioni. Per informazioni dettagliate sull'utilizzo di Generatore di topologie e Pannello di controllo di Lync Server 2013 per la gestione delle distribuzioni, vedere [Pannello di controllo di Lync Server 2013](https://technet.microsoft.com/it-it/library/gg133224\(v=ocs.15\)) nella documentazione relativa alle operazioni.

Le funzionalità di sicurezza degli script per Windows PowerShell sono progettate appositamente per impedire alcuni problemi di sicurezza relativi allo scripting di tecnologie non recenti, incluso Microsoft Visual Basic Scripting Edition (VBScript). Le funzionalità di sicurezza di Windows PowerShell sono concepite per creare un ambiente in cui gli utenti non possono eseguire script alla leggera o inconsapevolmente. Le funzionalità di sicurezza di Windows PowerShell sono abilitate per impostazione predefinita. È possibile modificare lo stato delle funzionalità per soddisfare le proprie esigenze di scripting e diversi obiettivi di sicurezza. Ciò non significa che la shell impedisce agli utenti di eseguire gli script, ma piuttosto che diventa più difficile eseguirli in modo inconsapevole. Per informazioni dettagliate, vedere Sicurezza degli script di Windows PowerShell all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=213145](http://go.microsoft.com/fwlink/p/?linkid=213145).

