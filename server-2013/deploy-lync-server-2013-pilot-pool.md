---
title: Distribuire il pool pilota di Lync Server 2013
TOCTitle: Distribuire il pool pilota di Lync Server 2013
ms:assetid: a81aba1e-e636-434b-8c56-4150435bb55d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205144(v=OCS.15)
ms:contentKeyID: 49301597
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuire il pool pilota di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-22_

Uno dei primi passaggi necessari per eseguire la migrazione in Lync Server 2013 consiste nel distribuire un pool pilota. In tale pool viene verificata la coesistenza di Lync Server 2013 con la distribuzione di Lync Server 2010. La coesistenza è uno stato temporaneo che dura finché tutti gli utenti e i pool non vengono spostati in Lync Server 2013.

Quando si distribuisce un pool pilota, si utilizza la procedura guidata Definisci nuovo pool Front End. È necessario distribuire nel pool pilota di Lync Server 2013 le stesse funzionalità e gli stessi carichi di lavoro di cui si dispone nel pool di Lync Server 2010. Se è stato distribuito il server di archiviazione, il Monitoring Server o System Center Operations Manager per archiviare e monitorare l'ambiente Lync Server 2010 e si desidera proseguire con l'archiviazione o il monitoraggio nel corso della migrazione, sarà necessario distribuire anche queste funzionalità nell'ambiente pilota. La versione distribuita per l'archiviazione o il monitoraggio dell'ambiente Lync Server 2010 non acquisirà dati nel'ambiente Lync Server 2013.


> [!NOTE]
> Nelle procedure riportate di seguito vengono descritte le funzionalità e le impostazioni da considerare nel processo di distribuzione generale del pool pilota. In questa sezione vengono evidenziati solo i punti chiave di cui è consigliabile tenere conto per la distribuzione del pool pilota. Per i passaggi dettagliati, fare riferimento alla guida alla <A href="lync-server-2013-deploying-lync-server.md">Distribuzione di Lync Server 2013</A>.



**Per distribuire un pool pilota di Lync Server 2013**

1.  Accedere al computer in cui è installato Generatore di topologie come membro del gruppo Domain Admins e del gruppo RTCUniversalServerAdmins.

2.  Espandere l'albero fino a **Lync Server 2013** - **Pool Enterprise Edition Front End** .

3.  Fare clic con il pulsante destro del mouse su **Pool Enterprise Edition Front End** e scegliere **Nuovo pool Front End** .
    
    ![Sottomenu di selezione del pool di server del Generatore di topologie](images/JJ205144.c2feed27-3418-42a6-a254-76e83607db9c(OCS.15).jpg "Sottomenu di selezione del pool di server del Generatore di topologie")

4.  Immettere l'FQDN del pool. Quando si definisce il pool pilota, è possibile scegliere di distribuire un pool Front End Enterprise Edition o un server Standard Edition. Lync Server 2013 non richiede che le funzionalità del pool pilota corrispondano a quelle distribuite nel pool legacy.
    

    > [!WARNING]
    > Il nome di dominio completo (FQDN) del pool o del server definito per il pool pilota deve essere univoco. Non può corrispondere al nome del pool di Lync Server 2010 attualmente distribuito o ad alcun altro server attualmente distribuito.

    
    ![Pagina per la definizione del nome di dominio completo della procedura guidata Definisci nuovo pool Front End](images/JJ205144.c5fd138c-e75a-413a-827f-b1461c996d40(OCS.15).jpg "Pagina per la definizione del nome di dominio completo della procedura guidata Definisci nuovo pool Front End")

5.  Nella pagina **Selezionare funzionalità** selezionare le caselle di controllo corrispondenti alle funzionalità desiderate per questo pool Front End. Se ad esempio si è scelto di distribuire solo le funzionalità di messaggistica istantanea e presenza, è necessario selezionare la casella di controllo Servizio di conferenza per consentire la messaggistica istantanea a più parti, ma non le caselle di controllo Servizi di conferenza telefonica con accesso esterno (PSTN), VoIP aziendale o Controllo di ammissione di chiamata perché corrispondono a funzionalità per conferenze vocali, video e di collaborazione. Per ulteriori informazioni sulla selezione delle funzionalità, vedere [Definire e configurare un pool Front End o un server Standard Edition in Lync Server 2013](lync-server-2013-define-and-configure-a-front-end-pool-or-standard-edition-server.md) nella documentazione relativa alla distribuzione.
    
    ![Pagina per la selezione delle funzionalità del pool Front End](images/JJ205144.5c3f3ff9-6e17-4d66-9b13-3bd55b38246b(OCS.15).jpg "Pagina per la selezione delle funzionalità del pool Front End")

6.  Nella pagina **Selezionare ruoli server collocati** è consigliabile collocare il Mediation Server in Lync Server 2013. Quando si unisce una topologia legacy a Lync Server 2013, è necessario innanzitutto collocare Lync Server 2010 Mediation Server. Dopo aver unito le topologie e configurato Lync Server 2013 Mediation Server, è possibile decidere di mantenere il Mediation Server collocato o sostituirlo con un server autonomo quando il ruolo di Mediation Server viene spostato in Lync Server 2013 durante il processo di distribuzione.
    
    ![Pagina per la selezione dei ruoli server collocati del pool Front End](images/JJ205144.e00b7eba-010b-44ed-b0a6-6ab3e534fb8c(OCS.15).jpg "Pagina per la selezione dei ruoli server collocati del pool Front End")

7.  Nella pagina **Associare ruoli server al pool Front End** , durante la distribuzione del progetto pilota, non selezionare l'opzione **Abilita un pool di server perimetrali utilizzato dal componente multimediale di questo pool Front End**. Questa funzionalità verrà abilitata e resa disponibile in una fase successiva della migrazione, pertanto mantenere deselezionata questa impostazione per ora.
    
    ![Pagina per l'associazione dei ruoli server al pool Front End](images/JJ205144.2d95a798-ad76-4dad-9392-ce41f4d938d1(OCS.15).jpg "Pagina per l'associazione dei ruoli server al pool Front End")

8.  Nella pagina **Selezionare un server Office Web Apps** fare clic su **Nuovo** e specificare l'FQDN del server applicazioni.
    
    ![Proprietà del nome di dominio completo di Definire un nuovo server Office Online](images/JJ205144.25c6b455-f1b8-4326-a569-6e338153d398(OCS.15).jpg "Proprietà del nome di dominio completo di Definire un nuovo server Office Online")

9.  Nella pagina **Definire l'archivio SQL Server per l'archiviazione** , durante la definizione dell'archivio di SQL Server per l'archiviazione e il monitoraggio di Lync Server, selezionare l'istanza di SQL Server creata in precedenza per Lync Server 2013.
    
    ![Pagina per la definizione dell'archivio SQL Server di archiviazione](images/JJ205144.0f76f1dc-d0d7-42a0-aea3-400b8e1f35cd(OCS.15).jpg "Pagina per la definizione dell'archivio SQL Server di archiviazione")

10. Per pubblicare la topologia, fare clic con il pulsante destro del mouse sul nodo **Lync Server** e quindi scegliere **Pubblica topologia** .
    
    ![Generatore di topologie con topologia configurata](images/JJ205144.c3eafa20-159e-4355-a23d-9f72aeb26037(OCS.15).jpg "Generatore di topologie con topologia configurata")

11. Al termine del processo di pubblicazione, fare clic su **Fine** .

Per installare una copia locale dell'archivio di configurazione e avviare i servizi necessari, vedere [Configurazione di Front End Server e pool Front End per Lync Server 2013](lync-server-2013-setting-up-front-end-servers-and-front-end-pools.md) nella documentazione relativa alla distribuzione.


