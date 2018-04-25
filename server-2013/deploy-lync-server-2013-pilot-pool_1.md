---
title: Distribuire il pool pilota di Lync Server 2013
TOCTitle: Distribuire il pool pilota di Lync Server 2013
ms:assetid: 19c27053-8b21-401f-ad91-75c2dd355e91
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204718(v=OCS.15)
ms:contentKeyID: 49299830
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuire il pool pilota di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-22_

Uno dei primi passaggi necessari per eseguire la migrazione in Lync Server 2013 consiste nel distribuire un pool pilota. In tale pool viene verificata la coesistenza di Lync Server 2013 con la distribuzione di Office Communications Server 2007 R2. La coesistenza è uno stato temporaneo che dura finché tutti gli utenti e i pool non vengono spostati in Lync Server 2013.

Quando si distribuisce un pool pilota, utilizzare la procedura guidata Definisci nuovo pool Front End. Nel pool pilota di Lync Server 2013 è necessario distribuire le stesse funzionalità e gli stessi carichi di lavoro presenti nel pool Office Communications Server 2007 R2. Se si è distribuito Server di archiviazione, Monitoring Server o System Center Operations Manager per l'archiviazione o il monitoraggio dell'ambiente Office Communications Server 2007 R2 e si desidera proseguire l'archiviazione o il monitoraggio per tutta la migrazione, è anche necessario distribuire queste funzionalità nell'ambiente pilota. La versione distribuita per l'archiviazione o il monitoraggio dell'ambiente Office Communications Server 2007 R2 non acquisisce dati nell'ambiente Lync Server 2013.


> [!NOTE]
> Nelle procedure riportate di seguito vengono descritte le funzionalità e le impostazioni da considerare nel processo di distribuzione generale del pool pilota. In questa sezione vengono evidenziati solo i punti chiave di cui è consigliabile tenere conto per la distribuzione del pool pilota. Per i passaggi dettagliati, fare riferimento alla guida alla <A href="lync-server-2013-deploying-lync-server.md">Distribuzione di Lync Server 2013</A>.



**Per distribuire un pool pilota di Lync Server 2013**

1.  Accedere al computer in cui è installato Generatore di topologie come membro del gruppo Domain Admins e del gruppo RTCUniversalServerAdmins.

2.  Aprire il Generatore di topologie e scegliere di creare una nuova topologia.

3.  Specificare il domino SIP primario.
    
    ![Crea nuova topologia - Pagina per la definizione del dominio primario](images/JJ204718.68775d87-f32c-494a-8386-6d4c81e81284(OCS.15).jpg "Crea nuova topologia - Pagina per la definizione del dominio primario")

4.  Continuare a eseguire la procedura guidata fino alla pagina **Definire il nuovo pool Front End**. Fare clic su Avanti.

5.  Immettere l'FQDN del pool. Quando si definisce il pool pilota, è possibile scegliere di distribuire un pool Front End Enterprise Edition o un server Standard Edition. Lync Server 2013 non richiede che le funzionalità del pool pilota corrispondano a quelle distribuite nel pool legacy.
    

    > [!WARNING]
    > Il nome di dominio completo (FQDN) del pool o del server definito per il pool pilota deve essere univoco. Non può corrispondere al nome del pool di Office Communications Server 2007 R2 attualmente distribuito o ad alcun altro server attualmente distribuito.

    
    ![Pagina Definire l'FQDN del pool Front End](images/JJ204718.5ff4336c-13fa-47cc-899b-066f267eb3f0(OCS.15).jpg "Pagina Definire l'FQDN del pool Front End")

6.  Definire il computer che verrà aggiunto al pool.
    
    ![Finestra di dialogo Definisci nuovo pool Front End](images/JJ204718.374f0ed4-988b-465f-9861-8d1db401e76f(OCS.15).jpg "Finestra di dialogo Definisci nuovo pool Front End")

7.  Nella pagina **Selezionare funzionalità** selezionare le caselle di controllo corrispondenti alle funzionalità desiderate per questo pool Front End. Se ad esempio si è scelto di distribuire solo le funzionalità di messaggistica istantanea e presenza, è necessario selezionare la casella di controllo Servizio di conferenza per consentire la messaggistica istantanea a più parti, ma non le caselle di controllo Servizi di conferenza telefonica con accesso esterno (PSTN), VoIP aziendale o Controllo di ammissione di chiamata perché corrispondono a funzionalità per conferenze vocali, video e di collaborazione. Per ulteriori informazioni sulla selezione delle funzionalità, vedere [Definire e configurare un pool Front End o un server Standard Edition in Lync Server 2013](lync-server-2013-define-and-configure-a-front-end-pool-or-standard-edition-server.md) nella documentazione relativa alla distribuzione.
    
    ![Pagina per la selezione delle funzionalità del pool Front End](images/JJ205144.5c3f3ff9-6e17-4d66-9b13-3bd55b38246b(OCS.15).jpg "Pagina per la selezione delle funzionalità del pool Front End")

8.  Nella pagina **Selezionare ruoli server collocati** è consigliabile collocare il Mediation Server in Lync Server 2013. Quando si unisce una topologia legacy a Lync Server 2013, è necessario innanzitutto collocare Office Communications Server 2007 R2  Mediation Server. Dopo aver unito le topologie e configurato Lync Server 2013  Mediation Server, è possibile decidere di mantenere il Mediation Server collocato o sostituirlo con un server autonomo quando il ruolo di Mediation Server viene spostato in Lync Server 2013 durante il processo di distribuzione.
    
    ![Pagina per la selezione dei ruoli server collocati del pool Front End](images/JJ205144.e00b7eba-010b-44ed-b0a6-6ab3e534fb8c(OCS.15).jpg "Pagina per la selezione dei ruoli server collocati del pool Front End")

9.  Nella pagina **Associare ruoli server al pool Front End** , durante la distribuzione del progetto pilota, non selezionare l'opzione **Abilita un pool di server perimetrali utilizzato dal componente multimediale di questo pool Front End**. Questa funzionalità verrà abilitata e resa disponibile in una fase successiva della migrazione, pertanto mantenere deselezionata questa impostazione per ora.
    
    ![Pagina per l'associazione dei ruoli server al pool Front End](images/JJ205144.2d95a798-ad76-4dad-9392-ce41f4d938d1(OCS.15).jpg "Pagina per l'associazione dei ruoli server al pool Front End")

10. Nella pagina **Selezionare un server Office Web Apps** fare clic su **Nuovo** e specificare l'FQDN del server applicazioni.
    
    ![Proprietà del nome di dominio completo di Definire un nuovo server Office Online](images/JJ205144.25c6b455-f1b8-4326-a569-6e338153d398(OCS.15).jpg "Proprietà del nome di dominio completo di Definire un nuovo server Office Online")

11. Nella pagina **Definire l'archivio SQL Server per l'archiviazione** selezionare l'istanza SQL Server creata precedentemente per Lync Server 2013.
    
    ![Pagina per la definizione dell'archivio SQL Server di archiviazione](images/JJ205144.0f76f1dc-d0d7-42a0-aea3-400b8e1f35cd(OCS.15).jpg "Pagina per la definizione dell'archivio SQL Server di archiviazione")

12. Nella pagina **Definire l'archivio SQL Server per il monitoraggio** selezionare l'istanza SQL Server creata in precedenza per Lync Server 2013. Fare clic su **Fine**.

13. Nel nodo principale del Generatore di topologie fare clic con il pulsante destro del mouse su **Lync Server** e scegliere **Modifica proprietà.** Fare clic su **URL semplici**.

14. Aggiornare l' **URL di accesso amministrativo**.
    
    ![Modifica proprietà - Pagina URL semplici](images/JJ204718.ef596dd2-1983-47e0-b342-4fc7a0e36380(OCS.15).jpg "Modifica proprietà - Pagina URL semplici")
    
    Per ulteriori informazioni sugli URL semplici, vedere l'argomento [Modificare o configurare URL semplici in Lync Server 2013](lync-server-2013-edit-or-configure-simple-urls.md) nella documentazione relativa alla distribuzione.

15. In **Modifica proprietà** fare clic su **Server di gestione centrale**.

16. Nell'elenco a discesa selezionare il pool Lync Server 2013.
    
    ![Modifica proprietà - Pagina Server di gestione centrale](images/JJ204718.211955fc-85f2-462d-8709-e6ea67092e89(OCS.15).jpg "Modifica proprietà - Pagina Server di gestione centrale")

17. Fare clic su OK per chiudere la pagina **Modifica proprietà**.

18. Nel menu **Azione** scegliere **Pubblica topologia**.

19. Al termine del processo di pubblicazione, fare clic su **Fine** .

20. Tornati nella distribuzione guidata di Lync Server 2013 fare clic su **Installa o aggiorna il sistema Lync Server**.
    
    ![Distribuzione guidata di Lync Server 2013](images/JJ204718.fb05adef-ad29-4905-9090-d409261b0e48(OCS.15).jpg "Distribuzione guidata di Lync Server 2013")

Per installare una copia locale dell'archivio di configurazione e avviare i servizi necessari, vedere [Configurazione di Front End Server e pool Front End per Lync Server 2013](lync-server-2013-setting-up-front-end-servers-and-front-end-pools.md) nella documentazione relativa alla distribuzione.


