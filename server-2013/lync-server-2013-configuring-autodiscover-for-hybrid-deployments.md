---
title: Configurazione dell'individuazione automatica per le distribuzioni ibride
TOCTitle: Configurazione dell'individuazione automatica per le distribuzioni ibride
ms:assetid: ca605e62-181c-42ca-80a1-e37e610f8277
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945653(v=OCS.15)
ms:contentKeyID: 52062265
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione dell'individuazione automatica per le distribuzioni ibride

 

_**Ultima modifica dell'argomento:** 2012-12-12_

Le distribuzioni ibride sono configurazioni che utilizzano sia il servizio cloud di Microsoft Lync Online che la distribuzione locale. In questo tipo di configurazione, il servizio di individuazione automatica deve essere in grado di individuare l'effettiva posizione dell'utente. In altre parole, il servizio di individuazione automatica permette di individuare l'account utente e il server che ospita l'account utente, indipendentemente dal fatto che si trovi nella distribuzione locale o nella distribuzione di Skype for Business online.

Ad esempio, se un account utente è ospitato in un server di Skype for Business online, il tentativo di individuare l'utente avverrà nel modo seguente, in base a un processo noto come *individuazione*:

  - L'utente avvia un tentativo di connessione alla distribuzione locale, **contoso.com**.

  - Il tentativo viene inviato a lyncdiscover.contoso.com, il nome DNS associato al servizio di individuazione automatica.

  - Il servizio di individuazione automatica fa riferimento al pool di registrazione presupposto nella distribuzione locale di contoso.com e riceve informazioni sul server principale dell'utente ospitato in Skype for Business online. A questo punto, il servizio di individuazione automatica invia all'utente una segnalazione al servizio di individuazione automatica online **lync.com**.

  - L'utente avvia un tentativo di connessione ai servizio di individuazione automatica online lync.com ed è in grado di individuare l'account utente e il server principale dell'utente.

Per abilitare i client per l'individuazione della distribuzione in cui si trova il server principale dell'utente, configurare il servizio di individuazione automatica con un nuovo URL (Uniform Resource Locator). Eseguire la procedura seguente per configurare il servizio di configurazione automatica.

## Configurazione del servizio di individuazione automatica per le distribuzione ibride

1.  Nell'argomento [Requisiti del servizio di individuazione automatica per Lync Server 2013](lync-server-2013-autodiscover-service-requirements.md) viene utilizzato Get-CsHostingProvider per recuperare il valore dell'attributo ProxyFQDN.

2.  In Lync Server Management Shell digitare
    
        Set-CsHostingProvider -Identity [identity] -AutodiscoverUrl https://webdir.online.lync.com/autodiscover/autodisccoverservice.svc/root
    
    Dove \[identity\] viene sostituito dal nome di dominio dello spazio di indirizzi SIP condiviso.

## Vedere anche

#### Ulteriori risorse

[Get-CsHostingProvider](get-cshostingprovider.md)  
[Set-CsHostingProvider](set-cshostingprovider.md)

