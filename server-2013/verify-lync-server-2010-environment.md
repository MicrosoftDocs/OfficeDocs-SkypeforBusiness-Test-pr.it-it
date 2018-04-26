---
title: Verificare l'ambiente Lync Server 2010
TOCTitle: Verificare l'ambiente Lync Server 2010
ms:assetid: bfc7c620-556a-43cd-b1ed-2c268ec2b5cc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205231(v=OCS.15)
ms:contentKeyID: 49301841
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verificare l'ambiente Lync Server 2010

 

_**Ultima modifica dell'argomento:** 2012-10-19_

Prima di distribuire Lync Server 2013 in uno stato di coesistenza con Lync Server 2010, è necessario verificare che i servizi di Lync Server 2010 siano stati configurati e avviati. È importante identificare i servizi e le funzionalità principali presenti nell'ambiente legacy prima di distribuire un pool pilota di Lync Server 2013. Prima di distribuire XMPP di Microsoft Lync Server 2013 XMPP in uno stato di coesistenza con una distribuzione XMPP legacy, è necessario verificare che i servizi XMPP legacy siano stati configurati e avviati e identificare il partner federato supportato dalla configurazione XMPP legacy. Per verificare la distribuzione di Lync Server 2010 legacy, è necessario eseguire le attività seguenti:

  - Verificare che i servizi di Lync Server 2010 siano stati avviati.

  - Esaminare la topologia e gli utenti in Lync Server 2010.

  - Verificare le impostazioni di federazione e server perimetrali.

  - Verificare i servizi e i partner federati XMPP.

**Verificare che i servizi di Lync Server 2010 siano stati avviati**

1.  Dal Front End Server di Lync Server 2010 passare all'applet Strumenti di amministrazione\\Servizi.

2.  Verificare che i servizi seguenti siano in esecuzione nel Front End Server:
    
    ![Elenco dei servizi in esecuzione nel server Front End](images/JJ205231.639f2729-b759-4d8e-b4ad-59d7f68adcd2(OCS.15).jpg "Elenco dei servizi in esecuzione nel server Front End")

**Esaminare la topologia di Lync Server 2010 nel Pannello di controllo di Lync Server**

1.  Eseguire l'accesso al Front End Server con un account membro del gruppo RTCUniversalServerAdmins oppure membro del ruolo amministrativo CsAdministrator o CsUserAdministrator.

2.  Aprire il Pannello di controllo di Lync Server.

3.  Selezionare **Topologia** . Verificare che i diversi server della distribuzione di Lync Server 2010 siano elencati.
    
    ![Pagina della topologia del Pannello di controllo di Lync Server 2010](images/JJ205231.338ce4fb-2162-4176-a249-ec4ae021fa6a(OCS.15).jpg "Pagina della topologia del Pannello di controllo di Lync Server 2010")

**Per esaminare gli utenti di Lync Server 2010 nel Pannello di controllo di Lync Server**

1.  Aprire il Pannello di controllo di Lync Server.

2.  Selezionare **Utenti** e quindi fare clic su **Trova** .

3.  Verificare che nella colonna **Pool di registrazione** sia indicato il pool di Lync Server 2010 per ogni utente elencato.
    
    ![Elenco utenti nel Pannello di controllo di Lync Server 2010](images/JJ205231.a9378c40-7a52-4c78-ad83-1463847c9edb(OCS.15).jpg "Elenco utenti nel Pannello di controllo di Lync Server 2010")

**Per verificare le impostazioni di federazione e server perimetrali di Lync Server 2010**

1.  Avviare Generatore di topologie.

2.  Selezionare **Scarica topologia dalla distribuzione esistente**.

3.  Scegliere un nome di file e salvare la topologia con il tipo di file predefinito con estensione tbxml.

4.  Espandere il nodo Lync Server 2010 per visualizzare i diversi ruoli del server presenti nella distribuzione.

5.  Selezionare il nodo del sito e verificare se è impostato un valore **Assegnazione route federazione sito**.
    
    ![Generatore di topologie - Route federazione sito](images/JJ205231.87de3735-af7e-4280-8d72-c42cb0ea1c05(OCS.15).jpg "Generatore di topologie - Route federazione sito")

6.  Selezionare quindi lo Standard Edition Front End Server o il pool Enterprise Edition Front End. Determinare se è stato configurato un pool di server perimetrali (per componenti multimediali) in **Associazioni**.
    
    ![Generatore di topologie con server e pool](images/JJ205231.5ad5ea3b-b122-44dd-8968-f1147d6d45f1(OCS.15).jpg "Generatore di topologie con server e pool")

7.  Selezionare infine il pool di server perimetrali e identificare se è configurato un pool hop successivo in **Selezione hop successivo**.
    
    ![Generatore di topologie - Selezione hop successivo](images/JJ205231.3121e723-fba7-498e-a786-bde7be1a55e2(OCS.15).jpg "Generatore di topologie - Selezione hop successivo")

**Verificare la configurazione dei partner federati XMPP legacy**

1.  Dal server XMPP legacy passare all'applet Strumenti di amministrazione\\Servizi.

2.  Verificare che il servizio gateway XMPP di Office Communications Server sia avviato.
    
    ![Servizio gateway XMPP di Office Communications Server](images/JJ721906.23223724-3c4b-4cb9-ace2-1cab2c3c91c3(OCS.15).jpg "Servizio gateway XMPP di Office Communications Server")

