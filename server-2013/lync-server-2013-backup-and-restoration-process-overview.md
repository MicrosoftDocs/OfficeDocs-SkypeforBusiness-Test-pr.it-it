---
title: Panoramica del processo di backup e ripristino
TOCTitle: Panoramica del processo di backup e ripristino
ms:assetid: e0f23b21-070f-4df5-b795-cea2f5338d85
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh202192(v=OCS.15)
ms:contentKeyID: 52062455
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica del processo di backup e ripristino

 

_**Ultima modifica dell'argomento:** 2013-03-26_

In questa sezione viene fornita una panoramica del processo di backup e ripristino per Lync Server 2013. Utilizzare lo stesso processo per tutti i server Standard Edition ed Enterprise Edition, indipendentemente dalla posizione.

In generale, il funzionamento del processo di backup è il seguente:

  - Creare un percorso di backup come cartella condivisa in un computer autonomo che non fa parte di un pool. Al percorso di backup viene fatto riferimento in **$Backup**.

  - In base a una pianificazione regolare, eseguire il backup di tutti i database di Lync Server e di tutti gli archivi file descritti in [Requisiti di backup e ripristino: dati](lync-server-2013-backup-and-restoration-requirements-data.md) eseguendo le procedure riportate in [Eseguire il backup di Lync Server](lync-server-2013-backing-up-lync-server.md). L'archivio di gestione centrale include tutte le impostazioni e le configurazioni dei server.

  - Ogni volta che si esegue un backup successivo, creare una nuova cartella e modificare il percorso a cui fa riferimento **$Backup**.

In generale, il funzionamento del processo ripristino è il seguente:

  - In caso di errore o guasto, ripristinare i dati nel percorso a fui fa riferimento **$Backup** in un computer nuovo o pulito.
    
    > [!important]  
    > I dati non vengono ripristinati in uno stato del server esistente, ovvero è necessario che il server sia pulito o nuovo.

  - Per consentire il recupero di informazioni utente o conferenza fino al punto di errore, è possibile implementare una topologia di ripristino di emergenza con pool Front End abbinati, come descritto in [Pianificazione per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md). Oltre a questa opzione, Lync Server supporta solo il modello di recupero con registrazione minima per i database, che prevede il recupero fino al punto dell'ultimo backup completo. Non sarà quindi possibile ripristinare un database fino al punto di errore o fino a un punto specifico nel tempo. Il modello di recupero con registrazione minima risulta ottimale per molte organizzazioni, perché il database back-end di Lync Server (RTCXDS.mdf) ha in effetti dimensioni minori rispetto ai file di log delle transazioni e ha dimensioni significativamente minori rispetto a quelle delle applicazioni database line-of-business tipiche.

  - Quando viene eseguito il ripristino, la configurazione DNS (Domain Name System), la configurazione DHCP (Dynamic Host Configuration Protocol), i nomi di dominio, i nomi di dominio completi (FQDN) dei computer, i percorsi degli archivi file e così via devono essere tutti uguali a come erano quando è stato eseguito il backup.

Se si verifica un errore in un server che esegue Lync Server, il ripristino include i passaggi seguenti:

  - Installare il sistema operativo in un computer nuovo o pulito con lo stesso FQDN del computer in errore.

  - Reinstallare i certificati.

  - Se il server ospita un database, installare Microsoft SQL Server 2012 o Microsoft SQL Server 2008 R2.

  - In generale, se il server ospita un database, eseguire Generatore di topologie per creare e installare il database e configurare gli elenchi di controllo di accesso.

  - In generale, se il server ospita un ruolo del server, eseguire i passaggi da 1 a 4 della Distribuzione guidata di Lync Server per installare i file di configurazione locali e i componenti del ruolo del server, assegnare i certificati e avviare i servizi.
    

    > [!NOTE]
    > Se il server ospita un database nella stessa posizione del ruolo del server, con l'esecuzione del passaggio 2 della Distribuzione guidata di Lync Server è possibile ricreare il database.



  - Se il server ospita un database, ripristinare i dati sottoposti a backup.

