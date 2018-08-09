---
title: "#VALUE!"
TOCTitle: "#VALUE!"
ms:assetid: 454c68df-2ef5-4b5f-a44c-4eee02635d45
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204860(v=OCS.15)
ms:contentKeyID: 49300386
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pubblicazione della topologia aggiornata per l'aggiunta dei database di archiviazione

 

_**Ultima modifica dell'argomento:** 2012-10-01_

Dopo aver aggiornato la topologia nel Generatore di topologie, è necessario pubblicarla nell'Archivio di gestione centrale prima di configurare e utilizzare l'archiviazione. In tutti i server della topologia vengono replicate copie di sola lettura dei dati in modo che siano sincronizzati con la topologia e altre modifiche della configurazione.

## Per pubblicare una topologia aggiornata

1.  In un computer che esegue Lync Server 2013 o in cui sono installati gli strumenti di amministrazione di Lync Server eseguire l'accesso con un account membro del gruppo locale Users o un account con diritti utente equivalenti.
    

    > [!NOTE]
    > È possibile definire una topologia utilizzando un account membro del gruppo locale Users, ma per pubblicare una topologia richiesta per aggiungere un server, è necessario utilizzare un account membro del gruppo <STRONG>Domain Admins</STRONG> e del gruppo <STRONG>RTCUniversalServerAdmins</STRONG> e con autorizzazioni di controllo completo (ovvero, lettura, scrittura e modifica) per la condivisione file utilizzata per l'archivio file Lync Server 2013 (in modo che il Generatore di topologie possa configurare gli elenchi di controllo di accesso discrezionale (DACL) richiesti o un account con diritti utente equivalenti.



2.  Aprire la topologia creata nella sezione precedente utilizzando il Generatore di topologie.

3.  Nell'albero della console fare clic con il pulsante destro del mouse su **Lync Server 2013** e quindi scegliere **Pubblica topologia**.

4.  Nella pagina **Pubblicare la topologia** fare clic su **Avanti**.

5.  Nella pagina **Crea altri database** verificare che il database sia selezionato e quindi fare clic su **Avanti**.
    

    > [!NOTE]
    > Se non si dispone delle autorizzazioni appropriate per la creazione dei database, è possibile annullare la selezione del database. Qualcuno con le autorizzazioni appropriate potrà creare il database. Per informazioni dettagliate sulle autorizzazioni e sui diritti di amministratore necessari, vedere <A href="lync-server-2013-deployment-permissions-for-sql-server.md">Autorizzazioni di distribuzione per SQL Server in Lync Server 2013</A> nella documentazione relativa alla distribuzione.<BR>Solo i database in computer SQL Server dedicati possono essere installati con il Generatore di topologie. I database in computer SQL Server collocati con altri componenti server devono essere installati eseguendo il programma di installazione locale nel computer in questione.



6.  Nella pagina **Pubblicazione guidata completata** verificare che la topologia sia stata pubblicata correttamente e quindi fare clic su **Fine**.
    
    > [!IMPORTANT]  
    > Dopo aver pubblicato la topologia, è necessario configurare le opzioni e i criteri per l'archiviazione, prima che sia possibile archiviare qualsiasi contenuto. Per informazioni dettagliate, vedere <a href="lync-server-2013-configuring-support-for-archiving.md">Configurazione del supporto per l'archiviazione in Lync Server 2013</a> nella documentazione relativa alla distribuzione.
