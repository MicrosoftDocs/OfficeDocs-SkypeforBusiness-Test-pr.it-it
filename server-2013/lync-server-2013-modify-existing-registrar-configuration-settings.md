---
title: "Lync Server 2013: Modifica configurazione di Registrazione avanzata"
TOCTitle: "Lync Server 2013: Modifica configurazione di Registrazione avanzata"
ms:assetid: a8931511-3e66-49ed-a3ec-03bcd61ce1f0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182566(v=OCS.15)
ms:contentKeyID: 49301590
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modificare le impostazioni di configurazione esistenti di Registrazione avanzata

 

_**Ultima modifica dell'argomento:** 2012-11-01_

È possibile utilizzare la funzione di registrazione per configurare i protocolli di autenticazione dei server proxy. Per informazioni sui protocolli disponibili, vedere [Creare le impostazioni di configurazione di Registrazione avanzata](lync-server-2013-create-registrar-configuration-settings.md).


> [!NOTE]
> Se un server supporta l'autenticazione sia per client remoti che per client aziendali, è consigliabile abilitare sia Kerberos che NTLM. Il server perimetrale e i server interni sono in comunicazione per garantire che ai client remoti sia fornita solo l'autenticazione NTLM. Se in questi server è abilitato solo Kerberos, non sono in grado di autenticare gli utenti remoti. Se attraverso questi server avviene anche l'autenticazione degli utenti aziendali, viene utilizzato Kerberos.



Per modificare una funzione di registrazione esistente, seguire la procedura seguente.

## Per modificare una funzione di registrazione esistente

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsServerAdministrator o CsAdministrator, accedere a un computer nella rete in cui è stato distribuito Lync Server 2013.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Sicurezza** e quindi su **Funzione di registrazione**.

4.  Nella pagina **Funzione di registrazione** fare clic su un servizio, fare clic su **Modifica** e quindi su **Mostra dettagli**.

5.  In **Modifica impostazione funzione di registrazione** selezionare una o più delle opzioni seguenti in base alle capacità dei client e al supporto nell'ambiente:
    
      - **Abilita autenticazione Kerberos** perché i server del pool emettano richieste utilizzando l'autenticazione Kerberos.
    
      - **Abilita autenticazione NTLM** perché i server del pool emettano richieste utilizzando l'autenticazione NTLM.
    
      - **Abilita autenticazione certificato** per fare in modo che i server nel pool emettano i certificati per i client.

6.  Fare clic su **Commit**.

