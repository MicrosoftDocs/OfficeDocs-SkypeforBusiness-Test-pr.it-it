---
title: Distribuire un server perimetrale pilota
TOCTitle: Distribuire un server perimetrale pilota
ms:assetid: 11a59c48-0a53-4de1-83ed-875f850febd5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204682(v=OCS.15)
ms:contentKeyID: 49299724
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuire un server perimetrale pilota

 

_**Ultima modifica dell'argomento:** 2012-10-19_

In questo argomento vengono illustrate le impostazioni di configurazione da tenere presenti prima di distribuire il server perimetrale di  Lync Server 2013. In questa sezione vengono evidenziati solo i punti chiave di cui è consigliabile tenere conto nell'ambito della distribuzione del pool di server perimetrali pilota. Per una procedura dettagliata, vedere [Distribuzione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-deploying-external-user-access.md) nella documentazione relativa alla distribuzione, in cui viene descritto il processo di distribuzione e vengono fornite anche informazioni sulla configurazione per l'accesso di utenti esterni.

Man mano che si va avanti nella procedura guidata **Definisci pool di server perimetrali** , esaminare le impostazioni di configurazione chiave illustrate nei passaggi seguenti. Si noti che sono visualizzate solo alcune pagine della procedura guidata **Definisci pool di server perimetrali** .

**Definire un pool di server perimetrali**

1.  Aprire la topologia pool pilota utilizzando Generatore di topologie.

2.  Passare al nodo Lync Server 2013. Fare clic con il pulsante destro del mouse su **Pool di server perimetrali** e quindi scegliere **Nuovo pool di server perimetrali** .
    
    ![Finestra di dialogo Definire il nuovo pool di server perimetrali](images/JJ205306.a90d388c-49ff-4620-a19d-42e2f1bb559c(OCS.15).jpg "Finestra di dialogo Definire il nuovo pool di server perimetrali")

3.  Un pool di server perimetrali può essere un **Pool di più computer** o un **Pool computer singolo** .
    
    ![Finestra di dialogo Definire l'FQDN del pool di server perimetrali](images/JJ205306.4904fe8f-537c-4e66-a399-1bd8a316dc10(OCS.15).jpg "Finestra di dialogo Definire l'FQDN del pool di server perimetrali")

4.  Nella pagina **Selezionare funzionalità** non abilitare la federazione o la federazione XMPP. Attualmente il routing della federazione e della federazione XMPP viene eseguita mediante il server perimetrale legacy di Office Communications Server 2007 R2. Queste funzionalità verranno configurate in una fase successiva della migrazione.
    
    ![Finestra di dialogo Selezionare funzionalità](images/JJ205306.cb0b45a4-2856-45ba-bd97-e49fafbb077e(OCS.15).jpg "Finestra di dialogo Selezionare funzionalità")

5.  Successivamente, completare le pagine seguenti della procedura guidata: **Selezionare le opzioni IP** , **FQDN esterni** , **Definire l'indirizzo IP interno** e **Definire l'indirizzo IP esterno** .

6.  Nella pagina **Definire l'hop successivo** selezionare il Server Director per l'hop successivo del pool di server perimetrali di Lync Server 2013.
    
    ![Finestra di dialogo Definisci pool di server perimetrali - Elenco Pool hop successivo](images/JJ204682.61d963d5-e0bd-4b1f-b437-e37c267347ba(OCS.15).jpg "Finestra di dialogo Definisci pool di server perimetrali - Elenco Pool hop successivo")

7.  Nella pagina **Associare pool Front End** non associare un pool a questo pool di server perimetrali in questa fase. Attualmente il routing del traffico multimediale esterno viene eseguito mediante l' server perimetrale legacy di Office Communications Server 2007 R2. Questa impostazione verrà configurata in una fase successiva della migrazione.
    
    ![Finestra di dialogo Definisci pool di server perimetrali](images/JJ204682.bb538039-bd2a-40ed-a120-8b80bd2cefc2(OCS.15).jpg "Finestra di dialogo Definisci pool di server perimetrali")

8.  Fare clic su **Fine** e quindi su **Pubblica** per pubblicare la topologia.

9.  Eseguire la procedura descritta in [Installare server perimetrali per Lync Server 2013](lync-server-2013-install-edge-servers.md) nella documentazione relativa alla distribuzione per installare i file nel nuovo server perimetrale, configurare i certificati e avviare i servizi.

È molto importante attenersi alle linee guida riportate nell'argomento [Distribuzione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-deploying-external-user-access.md) nella documentazione relativa alla distribuzione. In questa sezione vengono fornite solo indicazioni sulle impostazioni di configurazione per l'installazione di questi ruoli del server.

A questo punto dovrebbe essere presente una distribuzione di server perimetrale Office Communications Server 2007 R2 legacy, indicata dalla presenza di BackCompatSite, parallelamente a una distribuzione di server perimetrale Lync Server 2013. La federazione è configurata in modo da utilizzare il Director di Office Communications Server 2007 R2. Prima di passare alla fase successiva, verificare che entrambe le distribuzioni funzionino correttamente, che i servizi siano stati avviati e che sia possibile amministrare ogni distribuzione.

![Generatore di topologie con server perimetrale OCS](images/JJ204682.171363a3-eaf0-4c94-bd41-02b1ab6fa7dc(OCS.15).jpg "Generatore di topologie con server perimetrale OCS")

