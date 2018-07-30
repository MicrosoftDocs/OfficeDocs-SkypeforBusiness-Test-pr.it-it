---
title: Spostare oggetti contatto della messaggistica unificata di Exchange
TOCTitle: Spostare oggetti contatto della messaggistica unificata di Exchange
ms:assetid: 35c7e987-41b5-4798-b617-3303f20e52e3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688022(v=OCS.15)
ms:contentKeyID: 49887519
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Spostare oggetti contatto della messaggistica unificata di Exchange

 

_**Ultima modifica dell'argomento:** 2012-10-19_

Per eseguire la migrazione degli oggetti contatto Operatore automatico e Accesso sottoscrittore nella nuova distribuzione di Lync Server 2013, è innanzitutto necessario spostare gli oggetti dalla distribuzione legacy di Office Communications Server 2007 R2 alla nuova distribuzione di Lync Server 2013 mediante i cmdlet **Get-CsExUmContact** e **Move-CsExUmContact**. In Exchange Server è quindi necessario eseguire lo script **ExchUCUtil** di Windows PowerShell per eseguire le operazioni seguenti sul pool di Lync appena distribuito:

  - Aggiungerlo ai gateway IP di messaggistica unificata.

  - Aggiungerlo ai gruppi di risposta di messaggistica unificata.


> [!NOTE]
> Per poter utilizzare i cmdlet <STRONG>Get-CsExUmContact</STRONG> e <STRONG>Move-CsExUmContact</STRONG>, è necessario essere membri del gruppo RTCUniversalUserAdmins e disporre dell'autorizzazione per l'unità organizzativa (OU) in cui sono archiviati gli oggetti contatto. Tale autorizzazione può essere concessa eseguendo il cmdlet <STRONG>Grant-OUPermission</STRONG>.



## Per spostare gli oggetti contatto utilizzando Lync Server Management Shell

1.  Aprire Lync Server Management Shell.

2.  Per ogni pool registrato nella Messaggistica unificata di Exchange (dove pool1.contoso.net è un pool della distribuzione di Office Communications Server 2007 R2 e pool2.contoso.net è il pool della distribuzione di Lync Server 2013), nella riga di comando digitare quanto segue:
    
        Get-CsExUmContact -Filter {RegistrarPool -eq "pool01.contoso.net"} | Move-CsExUmContact -Target pool02.contoso.net
    
    Per accertarsi che gli oggetti contatto siano stati spostati, eseguire il cmdlet **Get-CsExumContact** e verificare che **RegistrarPool** ora punti al nuovo pool.

## Per eseguire lo script ExchUCUtil di Windows PowerShell

1.  Accedere al server di messaggistica unificata di Exchange come utente con privilegi di amministratore dell'organizzazione di Exchange.

2.  Passare allo script ExchUCUtil di Windows PowerShell.
    
    In Exchange 2007 ExchUCUtil.ps1 si trova in: **%Program Files%\\Microsoft\\Exchange Server\\Scripts\\ExchUCUtil.ps1**
    
    In Exchange 2010 ExchUCUtil.ps1 si trova in: **%Program Files%\\Microsoft\\Exchange Server\\V14\\Scripts\\ExchUCUtil.ps1**

3.  Se Exchange è distribuito in una singola foresta, digitare quanto indicato di seguito:
    
        exchucutil.ps1
    
    In alternativa, se Exchange è distribuito in più foreste, digitare quanto indicato di seguito:
    
        exchucutil.ps1 -Forest:" <forest FQDN>"
    
    dove *forest FQDN* specifica la foresta in cui è distribuito Lync Server 2013.
    
    > [!IMPORTANT]  
    > Riavviare il servizio <strong>Lync Server Front End</strong> (rtcsrv.exe) <em>dopo</em> aver eseguito exchucutil.ps1. In caso contrario Lync Server 2013 non rileverà la messaggistica unificata nella topologia.
