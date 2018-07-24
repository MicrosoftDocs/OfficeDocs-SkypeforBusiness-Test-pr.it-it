---
title: "Lync Server 2013: Configurazione della messaggistica unificata in Microsoft Exchange Server per l'interazione con Lync Server"
TOCTitle: Configurazione della messaggistica unificata in Microsoft Exchange Server per l'interazione con Lync Server 2013
ms:assetid: 058da9c4-23af-4ddb-9f63-70133a8aafc6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398106(v=OCS.15)
ms:contentKeyID: 49299552
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione della messaggistica unificata in Microsoft Exchange Server per l'interazione con Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-11_

> [!important]  
> Se si desidera utilizzare la Messaggistica unificata di Exchange per garantire il funzionamento del risponditore automatico, di Outlook Voice Access o dei servizi con operatori automatici per gli utenti di VoIP aziendale leggere le informazioni di <a href="lync-server-2013-planning-for-exchange-unified-messaging-integration.md">Pianificazione dell'integrazione della messaggistica unificata di Exchange in Lync Server 2013</a> nella documentazione relativa alla pianificazione e quindi seguire le istruzioni riportate in questa sezione.

Per configurare Messaggistica unificata di Exchange per l'utilizzo con VoIP aziendale sarà necessario eseguire le attività seguenti:

  - Configurare i certificati nel server che esegue i servizi di Messaggistica unificata di Exchange
    

    > [!NOTE]
    > Aggiungere tutti i server Accesso client e Cassette postali a tutti i dial plan di messaggistica unificata URI SIP. In caso contrario, il routing delle chiamate in uscita non funzionerà nel modo previsto.



  - Creare uno o più dial plan di messaggistica unificata URI SIP, insieme ai numeri di telefono di accesso del sottoscrittore necessari, quindi creare i dial plan di Lync Server corrispondenti.

  - Utilizzare lo script **exchucutil.ps1** per eseguire le operazioni seguenti:
    
      - Creare gateway IP di messaggistica unificata.
    
      - Creare gruppi di risposta di messaggistica unificata.
    
      - Concedere a Lync Server 2013 l'autorizzazione per leggere gli oggetti di messaggistica unificata in Servizi di dominio Active Directory.

  - Creare un oggetto operatore automatico di messaggistica unificata

  - Creare un oggetto accesso sottoscrittore

  - Creare un URI SIP per ogni utente e associazione degli utenti a un dial plan di messaggistica unificata URI SIP

## Requisiti e raccomandazioni

Prima di iniziare, nella documentazione di questa sezione si presuppone che siano stati distribuiti i ruoli del server di Exchange 2013 seguenti: Accesso client e Cassette postali. In Microsoft Exchange Server 2013, Messaggistica unificata di Exchange viene eseguito come servizio in tali server.

Per informazioni dettagliate sulla distribuzione di Exchange 2013, vedere la libreria TechNet per Exchange 2013 all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=266637](http://go.microsoft.com/fwlink/p/?linkid=266637).

Tenere inoltre presente quanto segue:

  - Se la messaggistica unificata di Messaggistica unificata di Exchange è installata in più foreste, la procedura di integrazione di Exchange Server deve essere eseguita per ogni foresta di messaggistica unificata. Ogni foresta di messaggistica unificata inoltre deve essere configurata in modo da considerare attendibile la foresta in cui viene distribuito Lync Server 2013 e tale foresta con Lync Server 2013 distribuito deve a sua volta essere configurata in modo da ritenere attendibile ogni foresta di messaggistica unificata.

  - La procedura di integrazione viene eseguita sia nei ruoli di Exchange Server in cui sono in esecuzione i servizi di messaggistica unificata, sia nel server che esegue Lync Server 2013. È consigliabile eseguire la procedura di integrazione della messaggistica unificata di Exchange Server prima di quella per l'integrazione di Lync Server 2013.
    

    > [!NOTE]
    > Per sapere quali passaggi di integrazione vengono eseguiti nei server dai diversi ruoli di amministratore, vedere <A href="lync-server-2013-deployment-process-for-integrating-on-premises-unified-messaging.md">Processo di distribuzione per l'integrazione della messaggistica unificata locale con Lync Server 2013</A>.



Gli strumenti seguenti devono essere disponibili in ogni server che esegue la Messaggistica unificata di Exchange:

  - Exchange Management Shell

  - Script **exchucutil.ps1**, che consente di eseguire le attività seguenti:
    
      - Creazione di un gateway IP di messaggistica unificata per ogni Lync Server 2013.
    
      - Creazione di un gruppo di risposta per ogni gateway. L'identificatore pilota di ogni gruppo di risposta specifica il dial plan di messaggistica unificata URI SIP utilizzato dal pool Front End o dal server Standard Edition associato al gateway.
    
      - Concessione a Lync Server 2013 dell'autorizzazione per leggere gli oggetti di messaggistica unificata di Exchange in Servizi di dominio Active Directory.

## Contenuto della sezione

  - [Configurare i certificati nel server che esegue la messaggistica unificata di Microsoft Exchange Server](lync-server-2013-configure-certificates-on-the-server-running-microsoft-exchange-server-unified-messaging.md)

  - [Configurare la messaggistica unificata in Microsoft Exchange per Lync Server 2013](lync-server-2013-configure-unified-messaging-on-microsoft-exchange.md)

