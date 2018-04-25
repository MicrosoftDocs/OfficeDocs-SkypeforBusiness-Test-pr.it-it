---
title: Distribuire un server perimetrale pilota
TOCTitle: Distribuire un server perimetrale pilota
ms:assetid: dab345c0-8577-4c11-ac73-fe8b2a75f4cf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205306(v=OCS.15)
ms:contentKeyID: 49302171
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuire un server perimetrale pilota

 

_**Ultima modifica dell'argomento:** 2012-10-19_

In questo argomento vengono illustrate le impostazioni di configurazione da prendere in considerazione prima della distribuzione del server perimetrale di Lync Server 2013. I processi di distribuzione e configurazione per Lync Server 2013 sono molto simili a quelli per Lync Server 2010. In questa sezione vengono evidenziati solo i punti chiave di cui è consigliabile tenere conto nella distribuzione del pool pilota. Per i passaggi dettagliati, vedere [Distribuzione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-deploying-external-user-access.md) nella documentazione relativa alla distribuzione, in cui viene descritto il processo di distribuzione e in cui vengono fornite inoltre informazioni di configurazione per l'accesso degli utenti esterni.

Man mano che si va avanti nella procedura guidata **Definisci pool di server perimetrali** , esaminare le impostazioni di configurazione chiave illustrate nei passaggi seguenti. Si noti che sono visualizzate solo alcune pagine della procedura guidata **Definisci pool di server perimetrali** .

**Definire un pool di server perimetrali**

1.  Accedere al computer in cui è installato Generatore di topologie come membro del gruppo Domain Admins e del gruppo RTCUniversalServerAdmins.

2.  Passare al nodo Lync Server 2013. Fare clic con il pulsante destro del mouse su **Pool di server perimetrali** e quindi scegliere **Nuovo pool di server perimetrali** .
    
    ![Finestra di dialogo Definire il nuovo pool di server perimetrali](images/JJ205306.a90d388c-49ff-4620-a19d-42e2f1bb559c(OCS.15).jpg "Finestra di dialogo Definire il nuovo pool di server perimetrali")

3.  Un pool di server perimetrali può essere un **Pool di più computer** o un **Pool computer singolo** .
    
    ![Finestra di dialogo Definire l'FQDN del pool di server perimetrali](images/JJ205306.4904fe8f-537c-4e66-a399-1bd8a316dc10(OCS.15).jpg "Finestra di dialogo Definire l'FQDN del pool di server perimetrali")

4.  Nella pagina **Selezionare funzionalità** non abilitare la federazione o la federazione XMPP. La federazione e la federazione XMPP vengono entrambe instradate attualmente tramite il server perimetrale di Lync Server 2010 legacy. Queste funzionalità verranno configurate in una fase successiva della migrazione.
    
    ![Finestra di dialogo Selezionare funzionalità](images/JJ205306.cb0b45a4-2856-45ba-bd97-e49fafbb077e(OCS.15).jpg "Finestra di dialogo Selezionare funzionalità")

5.  Continuare quindi con le pagine seguenti della procedura guidata: **FQDN esterni** , **Definire l'indirizzo IP interno** e **Definire l'indirizzo IP esterno** .

6.  Nella pagina **Definire l'hop successivo** selezionare il Server Director per l'hop successivo del pool di server perimetrali di Lync Server 2010.
    
    ![Finestra di dialogo Definire l'hop successivo](images/JJ205306.11baf3ea-74f5-4eb7-8650-b03b3b190416(OCS.15).jpg "Finestra di dialogo Definire l'hop successivo")

7.  Nella pagina **Associare pool Front End o Mediation** non associare un pool a questo pool di server perimetrali in questa fase. Il routing del traffico multimediale esterno viene eseguito attualmente mediante il server perimetrale di Lync Server 2010 legacy. Questa impostazione verrà configurata in una fase successiva della migrazione.
    
    ![Finestra di dialogo Associare pool Front End](images/JJ205306.fe0da887-7b51-4564-afc5-d57da95a2eb6(OCS.15).jpg "Finestra di dialogo Associare pool Front End")

8.  Fare clic su **Fine** e quindi su **Pubblica** per pubblicare la topologia.

9.  Eseguire la procedura descritta in [Installare server perimetrali per Lync Server 2013](lync-server-2013-install-edge-servers.md) nella documentazione relativa alla distribuzione per installare i file nel nuovo server perimetrale, configurare i certificati e avviare i servizi.

È molto importante attenersi alle linee guida riportate nell'argomento [Distribuzione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-deploying-external-user-access.md) nella documentazione relativa alla distribuzione. In questa sezione vengono fornite solo indicazioni sulle impostazioni di configurazione per l'installazione di questi ruoli del server.

Si disporrà ora di un server perimetrale di Lync Server 2010 legacy distribuito in parallelo con un server perimetrale di Lync Server 2013. Prima di passare alla fase successiva, verificare che entrambe le distribuzioni funzionino correttamente, che i servizi siano stati avviati e che sia possibile amministrare ogni distribuzione.

