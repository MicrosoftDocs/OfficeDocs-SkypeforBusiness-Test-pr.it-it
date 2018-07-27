---
title: Configurare le route di federazione e il traffico multimediale
TOCTitle: Configurare le route di federazione e il traffico multimediale
ms:assetid: 8b2f5f81-a955-4ad1-ad74-397322ff9521
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688121(v=OCS.15)
ms:contentKeyID: 49887641
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare le route di federazione e il traffico multimediale

 

_**Ultima modifica dell'argomento:** 2012-10-15_

La federazione è una relazione di trust tra due o più domini SIP che consente a utenti di organizzazioni distinte di comunicare attraverso i confini della rete. Dopo aver eseguito la migrazione nel pool pilota di Lync Server 2013, è necessario compiere la transizione dalla route di federazione dei server perimetrali Lync Server 2010 alla route di federazione dei server perimetrali Lync Server 2013.

Utilizzare le procedure seguenti per la transizione della route di federazione e della route del traffico di contenuto multimediale dal server perimetrale di Lync Server 2010 e dal server Director al server perimetrale di Lync Server 2013, per una distribuzione a singolo sito.

> [!IMPORTANT]  
> Per modificare la route di federazione e la route del traffico multimediale, è necessario pianificare un intervallo di tempo di inattività per la manutenzione per i server perimetrali di Lync Server 2013 e Lync Server 2010. L'intero processo di transizione comporta inoltre la non disponibilità dell'accesso federato per tutta la durata dell'interruzione dei servizi. È consigliabile pianificare il tempo di inattività nel periodo di attività minima degli utenti e inviare una notifica agli utenti finali. Eseguire le pianificazioni tenendo conto di questo periodo di interruzione e definire previsioni appropriate nell'organizzazione.

> [!IMPORTANT]  
> Se il server perimetrale legacy di Lync Server 2010 è configurato per l'uso dello stesso FQDN per il servizio Access Edge, il servizio Web Conferencing Edge e il servizio A/V Edge, le procedure in questa sezione non sono supportate. Se i servizi perimetrali legacy sono configurati per l'uso dello stesso FQDN, è necessario eseguire la migrazione di tutti gli utenti da Lync Server 2010 a Lync Server 2013, quindi la rimozione delle autorizzazioni del server perimetrale di Lync Server 2010 prima di abilitare la federazione nel server perimetrale di Lync Server 2013.

> [!IMPORTANT]  
> Se la federazione XMPP è instradata attraverso un server perimetrale Lync Server 2013, gli utenti legacy di Lync Server 2010 non potranno comunicare con il partner federato XMPP finché tutti gli utenti non saranno stati spostati in Lync Server 2013, i certificati e i criteri XMPP non saranno stati configurati, il partner federato XMPP non sarà stato configurato in Lync Server 2013 e le voci DNS non saranno state aggiornate.

## Per rimuovere l'associazione di federazione legacy dai siti di Lync Server 2013

1.  Nel server Front End di Lync Server 2013, aprire la topologia esistente nel Generatore di topologie.

2.  Nel riquadro sinistro, passare la nodo del sito direttamente sotto **Lync Server**.

3.  Fare clic con il pulsante destro del mouse sul sito e quindi scegliere **Modifica proprietà** .

4.  Nel riquadro sinistro selezionare **Route di federazione**.

5.  In **Assegnazione route federazione sito**, deselezionare la casella di controllo **Abilita federazione SIP** per disabilitare la route di federazione tramite l'ambiente Lync Server 2010 legacy.
    
    ![Finestra di dialogo Modifica proprietà - Pagina Route di federazione](images/JJ688121.8d755ae0-fc7d-4253-b0db-0cf31b863c55(OCS.15).jpg "Finestra di dialogo Modifica proprietà - Pagina Route di federazione")

6.  Fare clic su **OK** per chiudere la pagina Modifica proprietà.

7.  In **Generatore di topologie** selezionare il nodo principale **Lync Server** .

8.  Scegliere **Pubblica topologia** dal menu **Azione** .

9.  Fare clic su **Avanti** per completare il processo di pubblicazione e quindi fare clic su **Fine** al termine del processo.

## Per configurare il server perimetrale legacy come server perimetrale non federato

1.  Nel riquadro sinistro, passare al nodo **Lync Server 2010** e quindi al nodo **Pool di server perimetrali**.

2.  Fare clic con il pulsante destro del mouse sul server perimetrale e quindi scegliere **Modifica proprietà** .

3.  Selezionare **Generale** nel riquadro sinistro.

4.  Deselezionare la casella di controllo **Abilita federazione per pool di server perimetrali (porta 5061)** e fare clic su **OK** per chiudere la pagina.
    
    ![Modifica proprietà, Generale, deselezione di Abilita federazione](images/JJ688121.3be2c8c0-9ed9-4544-bafd-b7694271fafc(OCS.15).jpg "Modifica proprietà, Generale, deselezione di Abilita federazione")

5.  Scegliere **Pubblica topologia** dal menu **Azione** e quindi fare clic su **Avanti** .

6.  Al termine della **Pubblicazione guidata** , fare clic su **Fine** per chiudere la procedura guidata.

7.  Verificare che la federazione del server perimetrale legacy sia disabilitata.
    
    ![Generatore di topologie, pool di server perimetrali, federazione disabilitata](images/JJ688121.a2948438-d51a-4aeb-9eaa-d899ca950758(OCS.15).jpg "Generatore di topologie, pool di server perimetrali, federazione disabilitata")

## Per configurare i certificati nel server perimetrale Lync Server 2010

1.  Esportare il certificato esterno del proxy di accesso con la chiave privata dal server perimetrale Lync Server 2010 legacy.

2.  Nel server perimetrale Lync Server 2013 importare il certificato esterno del proxy di accesso esportato nel passaggio precedente.

3.  Assegnare il certificato esterno del proxy di accesso all'interfaccia esterna Lync Server 2013 del server perimetrale.

4.  Il certificato dell'interfaccia interno del server perimetrale Lync Server 2013 deve essere richiesto e assegnato da un'autorità di certificazione attendibile.

## Per modificare la route di federazione di Lync Server 2010 per l'uso del server perimetrale di Lync Server 2013

1.  Nel riquadro sinistro del Generatore di topologie, passare al nodo **Lync Server 2013** e quindi al nodo **Pool di server perimetrali**.

2.  Fare clic con il pulsante destro del mouse sul server perimetrale e quindi scegliere **Modifica proprietà** .

3.  Selezionare **Generale** nel riquadro sinistro.

4.  Selezionare la casella di controllo **Abilita federazione per pool di server perimetrali (porta 5061)** e quindi fare clic su **OK** per chiudere la pagina.
    
    ![Finestra di dialogo Modifica proprietà - Pagina Generale](images/JJ688121.cc79a88c-cce4-4cab-80ad-4f70325dc7c4(OCS.15).jpg "Finestra di dialogo Modifica proprietà - Pagina Generale")

5.  Scegliere **Pubblica topologia** dal menu **Azione** e quindi fare clic su **Avanti** .

6.  Al termine della **Pubblicazione guidata** , fare clic su **Fine** per chiudere la procedura guidata.

7.  Verificare che **Federazione (porta 5061)** sia impostata su **Abilitata**.
    
    ![Generatore di topologie, pool di server perimetrali, federazione abilitata](images/JJ688121.e8ccdada-23f4-47e5-a99d-5bf795fefc48(OCS.15).jpg "Generatore di topologie, pool di server perimetrali, federazione abilitata")

## Per aggiornare l'hop successivo di federazione del server perimetrale di Lync Server 2013

1.  Nel riquadro sinistro del Generatore di topologie, passare al nodo **Lync Server 2013** e quindi al nodo **Pool di server perimetrali**.

2.  Espandere il nodo, fare clic con il pulsante destro del mouse sul server perimetrale elencato e quindi scegliere **Modifica proprietà** .

3.  In **Selezione hop successivo** nella pagina **Generale** selezionare il pool di Lync Server 2013 dall'elenco a discesa.
    
    ![Finestra di dialogo Modifica proprietà - Pagina Hop successivo](images/JJ688121.5741b9a8-e729-4457-9f62-38f08a2c5b02(OCS.15).jpg "Finestra di dialogo Modifica proprietà - Pagina Hop successivo")

4.  Fare clic su **OK** per chiudere la pagina Modifica proprietà.

5.  In **Generatore di topologie** selezionare il nodo principale **Lync Server** .

6.  Nel menu **Azione** fare clic su **Pubblica topologia** e quindi completare la procedura guidata.

## Per configurare il percorso del contenuto multimediale in uscita dei server perimetrali Lync Server 2013

1.  Nel riquadro sinistro del Generatore di tipologie passare al nodo **Lync Server 2013** e quindi al pool sotto **Standard Edition Front End Server** o **Pool Enterprise Edition Front End** .

2.  Fare clic con il pulsante destro del mouse sul pool e quindi scegliere **Modifica proprietà** .

3.  Nella sezione **Associazioni** selezionare la casella di controllo **Associa pool di server perimetrali (per componenti multimediali)** .
    
    ![Modifica proprietà, Generale - Associa pool di server perimetrali](images/JJ688121.fd9b18ca-fda2-4764-9bf0-726bf39f6a12(OCS.15).jpg "Modifica proprietà, Generale - Associa pool di server perimetrali")

4.  Nell'elenco a discesa selezionare il server perimetrale Lync Server 2013.

5.  Fare clic su **OK** per chiudere la pagina **Modifica proprietà** .

## Per attivare la federazione del server perimetrale Lync Server 2013

1.  Nel riquadro sinistro del Generatore di topologie, passare al nodo **Lync Server 2013** e quindi al nodo **Pool di server perimetrali**.

2.  Espandere il nodo, fare clic con il pulsante destro del mouse sul server perimetrale elencato e quindi scegliere **Modifica proprietà** .
    

    > [!NOTE]
    > È possibile abilitare la federazione solo per un singolo pool di server perimetrali. Se si dispone di più pool di server perimetrali, selezionarne uno da utilizzare come pool di server perimetrali federativo.



3.  Nella pagina **Generale** verificare che l'impostazione **Abilita federazione per pool di server perimetrali (porta 5061)** sia selezionata.
    
    ![Finestra di dialogo Modifica proprietà - Pagina Generale](images/JJ688121.cc79a88c-cce4-4cab-80ad-4f70325dc7c4(OCS.15).jpg "Finestra di dialogo Modifica proprietà - Pagina Generale")

4.  Fare clic su **OK** per chiudere la pagina Modifica proprietà.

5.  Passare quindi al nodo del sito.

6.  Fare clic con il pulsante destro del mouse sul sito e quindi scegliere **Modifica proprietà** .

7.  Nel riquadro sinistro fare clic su **Route di federazione** .

8.  In **Assegnazione route federazione sito** selezionare **Abilita federazione SIP** e quindi nell'elenco selezionare il server perimetraleLync Server 2013 elencato.
    
    ![Modifica proprietà - Pagina Route di federazione](images/JJ688121.c50c13b8-0859-4e3e-8793-45c431a5b4b5(OCS.15).jpg "Modifica proprietà - Pagina Route di federazione")

9.  Fare clic su **OK** per chiudere la pagina **Modifica proprietà** .
    
    Nel caso di distribuzioni multisito, eseguire questa procedura in ogni sito.

## Per pubblicare le modifiche di configurazione del server perimetrale

1.  In **Generatore di topologie** selezionare il nodo principale **Lync Server** .

2.  Scegliere **Pubblica topologia** dal menu **Azione** e quindi completare la procedura guidata.

3.  Attendere il completamento della replica di Active Directory in tutti i pool della distribuzione.
    

    > [!NOTE]
    > Potrebbe essere visualizzato il messaggio seguente:<BR><STRONG>Avviso: la topologia contiene più di un server perimetrale federato. Questa situazione può verificarsi durante la migrazione a una versione successiva del prodotto. In questo caso, per la federazione viene utilizzato attivamente un solo server perimetrale. Verificare che il record SRV DNS punti al server perimetrale corretto. Se si desidera distribuire più server perimetrali federati in modo che siano attivi contemporaneamente (ovvero non in uno scenario di migrazione), verificare che tutti i partner federati utilizzino Lync Server e che il record SRV DNS esterno elenchi tutti i server perimetrali abilitati per la federazione</STRONG> .<BR>Si tratta di un avviso previsto che può essere tranquillamente ignorato.



## Per configurare un server perimetrale di Lync Server 2013

1.  Portare online tutti i server perimetrali Lync Server 2013.

2.  Aggiornare le regole di routing del firewall esterno o le impostazioni del dispositivo di bilanciamento del carico hardware in modo da inviare il traffico SIP per l'accesso esterno (solitamente, porta 443) e la federazione (in genere, porta 5061) al server perimetraleLync Server 2013, anziché al server perimetrale legacy.
    

    > [!NOTE]
    > Se non si dispone di un servizio di bilanciamento del carico hardware, è necessario aggiornare il record A DNS per la federazione in modo che venga risolto nel nuovo server Access Edge Server di Lync Server. Per eseguire questa operazione causando una minima interruzione del servizio, ridurre il valore TLL per l'FQDN Access Edge di Lync Server esterno in modo che se il DNS viene aggiornato per puntare al nuovo Access Edge Server di Lync Server, la federazione e l'accesso remoto vengano aggiornati rapidamente.



3.  Arrestare quindi il servizio **Lync Server Access Edge** in ogni computer server perimetrale.

4.  In ogni computer server perimetrale legacy aprire l'applet **Servizi** in **Strumenti di amministrazione** .

5.  Nell'elenco di servizi, individuare **Lync Server Access Edge** .

6.  Fare clic con il pulsante destro del mouse sul nome del servizio e quindi scegliere **Arresta** per arrestare il servizio.

7.  Impostare il tipo di avvio su **Disabilitato** .

8.  Fare clic su **OK** per chiudere la finestra **Proprietà** .

