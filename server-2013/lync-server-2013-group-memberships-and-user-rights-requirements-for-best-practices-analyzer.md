---
title: Requisiti di appartenenze ai gruppi e diritti utente per Best Practices Analyzer
TOCTitle: Requisiti di appartenenze ai gruppi e diritti utente per Best Practices Analyzer
ms:assetid: f812e343-8f75-454e-b7a8-1b404e32071a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg591354(v=OCS.15)
ms:contentKeyID: 49302511
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti di appartenenze ai gruppi e diritti utente per Best Practices Analyzer

 

_**Ultima modifica dell'argomento:** 2012-10-21_

Per eseguire correttamente Best Practices Analyzer, è necessario che l'account utente utilizzato per accedere sia un membro del gruppo Administrators nel computer locale. Inoltre, per analizzare l'ambiente, è necessario che l'utente sia un membro dei gruppi seguenti:

  - **Domain Admins**   Per enumerare le informazioni dei Servizi di dominio Active Directory e per richiamare i provider di Strumentazione gestione Windows (WMI) nei controller di dominio e server di catalogo globale.

  - **Administrators**   Obbligatorio in tutti i computer interni di Lync Server 2013 e nei server perimetrali per richiamare i provider di Strumentazione gestione Windows (WMI) e accedere al Registro di sistema.

  - **RTCUniversalReadOnlyAdmins**   Diritti amministrativi di Lync Server 2013 completi o delegati in sola lettura.

  - **Amministratore di Exchange solo visualizzazione**   Amministratore di Exchange solo visualizzazione completo o delegato nell'organizzazione di Microsoft Exchange.

Se l'account utente non dispone di diritti utente sufficienti, sono disponibili due opzioni:

  - Nel prompt dei comandi utilizzare il comando **runas** per eseguire lo strumento in un account che non dispone diritti utenti sufficienti. Di seguito viene illustrata la sintassi del comando:
    
        runas /netonly /user:<domain>\<userName> rtcbpa.exe

  - Nella pagina **Connessione a Active Directory** impostare le credenziali per gli account che si prevede di utilizzare per eseguire lo strumento Best Practices Analyzer. Fare clic su **Mostra opzioni di accesso avanzate**. È possibile immettere tre account: uno per connettersi ai Servizi di dominio Active Directory, uno per connettersi ai server perimetrali di Lync Server 2013 e uno per connettersi a Exchange Server. Se non si specifica nessuno dei tre account, verrà utilizzato l'account utente utilizzato per accedere ed eseguire lo strumento Best Practices Analyzer.

