---
title: Creare le impostazioni di configurazione di un nuovo servizio Web
TOCTitle: Creare le impostazioni di configurazione di un nuovo servizio Web
ms:assetid: f3f04d81-8a1f-427f-bd0f-fb659024e096
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182605(v=OCS.15)
ms:contentKeyID: 49302469
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare le impostazioni di configurazione di un nuovo servizio Web

 

_**Ultima modifica dell'argomento:** 2012-11-01_

È possibile utilizzare la pagina **Servizio Web** per configurare i metodi di autenticazione per l'accesso ai servizi Web e ai server Web correlati a Lync Server 2013.

Eseguire la procedura seguente per eliminare un criterio di servizio Web.

## Per creare criteri del servizio Web

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsServerAdministrator o CsAdministrator, accedere a un computer nella rete in cui è stato distribuito Lync Server 2013.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Sicurezza** e quindi su **Servizio Web**.

4.  Nella scheda **Servizio Web** fare clic su **Nuovo** e quindi eseguire una delle operazioni seguenti:
    
      - Per configurare il servizio Web per un sito, fare clic su **Configurazione sito**. In **Seleziona un sito** fare clic sul sito a cui verranno applicati i criteri del servizio Web e fare clic su **OK**.
    
      - Per configurare il servizio Web per un pool, fare clic su **Configurazione pool**. In **Seleziona un servizio** fare clic sul servizio a cui verranno applicati i criteri del servizio Web e fare clic su **OK**.

5.  In **Impostazione nuovo servizio Web**, in **Autenticazione integrata di Windows** selezionare **Negoziazione**, **Autenticazione integrata di Windows** o **Nessuno**.

6.  Selezionare una o più delle seguenti opzioni a seconda delle funzionalità dei client e del supporto nell'ambiente:
    
      - **Abilita autenticazione PIN** per abilitare l'autenticazione dei client mediante i numeri PIN.
    
      - **Abilita autenticazione certificato** per fare in modo che i server nel pool emettano i certificati per i client.
    
      - **Abilita download catena di certificati** per fare in modo che i server a cui viene presentato un certificato di autenticazione scarichino la catena di certificati per tale certificato.

7.  Fare clic su **Commit**.

