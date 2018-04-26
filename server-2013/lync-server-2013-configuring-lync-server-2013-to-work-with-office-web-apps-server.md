---
title: Configurazione di Lync Server 2013 per l'utilizzo con Office Web Apps Server
TOCTitle: Configurazione di Lync Server 2013 per l'utilizzo con Office Web Apps Server
ms:assetid: 6231e519-9010-4ff9-b5a6-b5859c2b3e11
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204944(v=OCS.15)
ms:contentKeyID: 49300763
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di Lync Server 2013 per l'utilizzo con Office Web Apps Server

 

_**Ultima modifica dell'argomento:** 2013-04-22_

Prima di poter configurare Lync Server 2013 per l'utilizzo del server Office Web Apps, è necessario distribuire e configurare il server Office Web Apps Vedere la guida alla distribuzione del server Office Web Apps e di Office Web Apps per informazioni dettagliate su come installare e configurare un singolo server Office Web Apps o per informazioni su come installare e configurare una server farm Office Web Apps per la disponibilità elevata.

Dopo aver installato correttamente il server Office Web Apps e aver configurato in modo appropriato la Web farm, è necessario proseguire con la configurazione di Lync Server per le comunicazioni con il nuovo server, aggiungendo l'URL di individuazione del server Office Web Apps alla topologia di Lync Server. Per aggiungere il server Office Web Apps alla topologia, eseguire le operazioni seguenti:

1.  Fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013 (Preview)** e quindi **Generatore di topologie di Lync Server**.

2.  Nella finestra di dialogo **Generatore di topologie** selezionare **Scarica topologia dalla distribuzione esistente** e quindi fare clic su **OK**.

3.  Nella casella **Salva topologia con nome** digitare un nome per il documento della topologia (ad esempio **TopologiaPreServerWebApps**) nella casella **Nome file** e quindi fare clic su **Salva**. Questa topologia potrà essere recuperata e ripubblicata in seguito se si verificano problemi con la nuova topologia.

4.  In Generatore di topologie espandere **Lync Server 2013 (Preview)**, espandere il nome del sito, espandere **Pool Enterprise Edition Front End** fare clic con il pulsante destro del mouse sul nome di uno dei pool e quindi scegliere **Modifica proprietà**.

5.  Nella scheda **Generale** della finestra di dialogo **Modifica proprietà** individuare il titolo **Associa il pool a un server Office Web Apps** e quindi fare clic su **Nuovo** oppure selezionare un server Office Web Apps esistente nell'elenco a discesa.

6.  Nella finestra di dialogo **Definire un nuovo server Office Web Apps** digitare il nome di dominio completo (FQDN) del computer del server Office Web Apps nella casella **FQDN server Office Web Apps**. L'URL di individuazione del server Office Web Apps dovrebbe comparire così automaticamente nella casella **URL di individuazione server Office Web Apps**.
    
    Se il server Office Web Apps è installato in locale e nella stessa area di rete di Lync Server 2013, allora l'opzione **Il server Office Web Apps è distribuito in una rete esterna (perimetro/Internet)** non deve essere selezionata.
    
    Se il server Office Web Apps è distribuito all'esterno del firewall interno, allora selezionare l'opzione **Il server Office Web Apps è distribuito in una rete esterna (perimetro/Internet)**.

7.  Nella finestra di dialogo **Definire un nuovo server Office Web Apps** fare clic su **OK** e quindi fare clic su **OK** nella finestra di dialogo **Modifica proprietà**. L'URL di individuazione di Office Web Apps verrà elencato come una delle associazioni del pool.

Sarà necessario ripetere questa procedura per ogni pool che deve essere associato al server Office Web Apps.

Dopo aver aggiunto l'URL di individuazione alla topologia, è necessario pubblicare la topologia aggiornata, operazione da eseguire in Generatore di topologie:

1.  Fare clic su **Azione** e quindi su **Pubblica topologia**.

2.  Nella pagina **Pubblicare la topologia** della procedura guidata Pubblica topologia fare clic su **Avanti**.

3.  Nella pagina **Pubblicazione guidata completata** fare clic su **Fine**.

4.  Chiudere Generatore di topologie.

