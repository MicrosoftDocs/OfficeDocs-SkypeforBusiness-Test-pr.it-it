---
title: Configurare un nuovo server applicazioni attendibile in Lync Server 2013
TOCTitle: Configurare un nuovo server applicazioni attendibile in Lync Server 2013
ms:assetid: a7233db7-fac3-43ff-972e-3bc29a56adb3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg617964(v=OCS.15)
ms:contentKeyID: 49301586
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare un nuovo server applicazioni attendibile in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Un'applicazione attendibile è un'applicazione basata su Microsoft Unified Communications Managed API (UCMA) 3.0 Core SDK considerata attendibile da Microsoft Lync Server 2013. Per informazioni dettagliate sulle applicazioni UCMA (Unified Communications Managed API), vedere "Documentazione dell'SDK di UCMA 3.0 Core" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=210320\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=210320%26clcid=0x410).

Per informazioni sulla configurazione di Microsoft Outlook Web Access (OWA) e Lync Server 2013, vedere "Configurazione dell'integrazione di Outlook Web App con Lync Server 2010" nella documentazione di Microsoft Exchange Server 2013.

Per pubblicare, abilitare o disabilitare correttamente una topologia quando si aggiunge o si rimuove un ruolo server, è necessaria una connessione tramite un account utente membro dei gruppi RTCUniversalServerAdmins e Domain Admins. È inoltre possibile delegare le autorizzazioni e i diritti di amministratore per l'aggiunta di ruoli server. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md) nella documentazione relativa allo sviluppo. Per poter apportare altre modifiche relative alla configurazione, è necessario appartenere solo al gruppo RTCUniversalServerAdmins..

## Per configurare un server applicazioni attendibili

1.  Accedere al computer in cui è installato Generatore di topologie come membro del gruppo Domain Admins e del gruppo RTCUniversalServerAdmins.

2.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

3.  Selezionare **Scarica topologia dalla distribuzione esistente** e quindi fare clic su **OK** .

4.  Nella finestra di dialogo **Salva topologia con nome** fare clic sul file di Generatore di topologie che si desidera utilizzare e quindi fare clic su **Salva**.

5.  Nel riquadro sinistro fare clic con il pulsante destro del mouse su **Server applicazioni attendibili** e quindi scegliere **Nuovo pool di applicazioni attendibili**.

6.  Immettere il nome FQDN del pool di applicazioni attendibili in **Pool FQDN**, specificare se sarà un pool a server singolo o a più server e quindi fare clic su **Avanti**.

7.  Nella pagina **Selezionare l'hop successivo** selezionare il pool Front End di Lync Server 2013 nell'elenco.

8.  Fare clic su **Fine**.

9.  Selezionare il nodo principale **Lync Server 2013** e quindi scegliere **Pubblica topologia** dal menu **Azioni**.
    
    Il **Pool di applicazioni attendibili** dovrebbe essere stato creato correttamente e associato al pool Front End corretto.

