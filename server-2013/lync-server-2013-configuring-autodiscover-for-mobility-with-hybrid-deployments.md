---
title: "Lync Server 2013: Configurazione dell'individuazione automatica per i dispositivi mobili con distribuzioni ibride"
TOCTitle: Configurazione dell'individuazione automatica per i dispositivi mobili con distribuzioni ibride
ms:assetid: f838af79-d8b4-4122-b81c-7889573d143e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ215885(v=OCS.15)
ms:contentKeyID: 49302529
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione dell'individuazione automatica in Lync Server 2013 per i dispositivi mobili con distribuzioni ibride

 

_**Ultima modifica dell'argomento:** 2014-06-18_

Le distribuzioni ibride sono configurazioni che utilizzano sia il servizio cloud di Microsoft Lync Online che la distribuzione locale. In questo tipo di configurazione, il servizio di individuazione automatica deve essere in grado di individuare l'effettiva posizione dell'utente. In altre parole, il servizio di individuazione automatica permette di individuare l'account utente e il server che ospita l'account utente, indipendentemente dal fatto che si trovi nella distribuzione locale o nella distribuzione di Skype for Business online.

Ad esempio, se un account utente è ospitato in un server di Skype for Business online, il tentativo di individuare l'utente avverrà nel modo seguente, in base a un processo noto come *individuazione* :

  - L'utente avvia un tentativo di connessione alla distribuzione locale, **contoso.com**.

  - Il tentativo viene inviato a lyncdiscover.contoso.com, il nome DNS associato al servizio di individuazione automatica.

  - Il servizio di individuazione automatica fa riferimento al pool di registrazione presupposto nella distribuzione locale di contoso.com e riceve informazioni sul server principale dell'utente ospitato in Skype for Business online. A questo punto, il servizio di individuazione automatica invia all'utente una segnalazione al servizio di individuazione automatica online **lync.com**.

  - L'utente avvia un tentativo di connessione ai servizio di individuazione automatica online lync.com ed è in grado di individuare l'account utente e il server principale dell'utente.

Per abilitare i client mobili per l'individuazione della distribuzione in cui si trova il server principale dell'utente, configurare il servizio di individuazione automatica con un nuovo URL (Uniform Resource Locator). Eseguire la procedura seguente per configurare il servizio di configurazione automatica.

## Configurazione dell'individuazione automatica per le distribuzioni ibride

1.  Get-CsHostingProvider viene utilizzato per recuperare il valore dell'attributo ProxyFQDN.

2.  In Lync Server Management Shell digitare
    
        Set-CsHostingProvider -Identity [identity] -AutodiscoverUrl https://webdir.online.lync.com/autodiscover/autodiscoverservice.svc/root
    
    Dove \[identity\] viene sostituito dal nome di dominio dello spazio di indirizzi SIP condiviso.

## Vedere anche

#### Ulteriori risorse

[Get-CsHostingProvider](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsHostingProvider)  
[Set-CsHostingProvider](set-cshostingprovider.md)

