---
title: Modificare le impostazioni di configurazione del servizio Web esistente
TOCTitle: Modificare le impostazioni di configurazione del servizio Web esistente
ms:assetid: bd9c7aa5-d31c-4fab-b31d-8baae26b1296
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182580(v=OCS.15)
ms:contentKeyID: 49301831
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modificare le impostazioni di configurazione del servizio Web esistente

 

_**Ultima modifica dell'argomento:** 2012-11-01_

È possibile utilizzare la pagina **Servizio Web** per configurare i metodi di autenticazione per l'accesso ai servizi Web e ai server Web correlati a Lync Server 2013.

Eseguire la procedura seguente per modificare i criteri per un servizio Web esistente.

## Per modificare un servizio Web esistente

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsServerAdministrator o CsAdministrator, accedere a un computer nella rete in cui è stato distribuito Lync Server 2013.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Sicurezza** e quindi su **Servizio Web**.

4.  Nella pagina **Servizio Web** fare clic su una configurazione, fare clic su **Modifica** e quindi su **Mostra dettagli**.

5.  In **Modifica impostazione servizio Web**, in **Autenticazione integrata di Windows**, selezionare **Negoziazione**, **Autenticazione integrata di Windows** o **Nessuno**.

6.  Selezionare una o più delle opzioni seguenti in base alle capacità dei client e al supporto nell'ambiente:
    
      - **Abilita autenticazione PIN** per consentire l'autenticazione dei client tramite numeri PIN.
    
      - **Abilita autenticazione certificato** per fare in modo che i server nel pool emettano i certificati per i client.
    
      - **Abilita download catena di certificati** per fare in modo che i server a cui viene presentato un certificato di autenticazione eseguano il download della catena di certificati per tale certificato.

7.  Fare clic su **Commit**.

## Vedere anche

#### Ulteriori risorse

[Configurazione della sicurezza](lync-server-2013-configuring-authentication-in-the-lync-server-control-panel.md)

