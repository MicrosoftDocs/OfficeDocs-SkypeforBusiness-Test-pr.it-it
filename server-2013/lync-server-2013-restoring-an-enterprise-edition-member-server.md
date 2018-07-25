---
title: Ripristino di un server membro Enterprise Edition
TOCTitle: Ripristino di un server membro Enterprise Edition
ms:assetid: d960b19c-2104-4719-b736-0d940f254d42
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh202191(v=OCS.15)
ms:contentKeyID: 52062452
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ripristino di un server membro Enterprise Edition

 

_**Ultima modifica dell'argomento:** 2013-02-18_

Se si verifica un errore in un server che esegue uno dei ruoli del server seguenti, eseguire la procedura descritta in questo argomento per ripristinarlo. Se si verificano errori in più server indipendenti, eseguire la procedura in ogni server.

  - Front End Server

  - Mediation Server

  - Director

  - Server Chat persistente

  - Server perimetrale

> [!tip]  
> È consigliabile creare una copia dell'immagine del sistema prima di avviare il ripristino. È possibile utilizzarla come punto di rollback in caso di problemi durante il ripristino. È possibile creare questa copia dopo aver installato il sistema operativo e SQL Server e dopo aver ripristinato o registrato di nuovo i certificati.

## Per ripristinare un server membro

1.  Iniziare con un server pulito o nuovo che abbia lo stesso nome di dominio completo (FQDN) del server in cui si è verificato l'errore, installare il sistema operativo e quindi ripristinare o registrare di nuovo i certificati.
    

    > [!NOTE]
    > Per eseguire questo passaggio, attenersi alle procedure per la distribuzione del server dell'organizzazione.



2.  Con un account utente membro del gruppo RTCUniversalServerAdmins accedere al server da ripristinare.

3.  Passare alla cartella o al supporto di installazione di Lync Server e avviare la Distribuzione guidata di Lync Server dal percorso \\setup\\amd64\\Setup.exe.

4.  Tramite la Distribuzione guidata, eseguire le operazioni seguenti:
    
    1.  Eseguire **Passaggio 1: Installazione dell'archivio di configurazione locale** per installare i file di configurazione locali.
    
    2.  Eseguire **Passaggio 2: Installazione o rimozione componenti di Lync Server** per installare i ruoli server di Lync Server.
    
    3.  Eseguire **Passaggio 3: Richiesta, installazione o assegnazione dei certificati** per assegnare i certificati.
    
    4.  Eseguire **Passaggio 4: Avvio servizi** per avviare i servizi sul server.
    
    Per informazioni dettagliate sull'esecuzione della Distribuzione guidata, vedere la documentazione relativa alla distribuzione per il ruolo del server che si sta ripristinando.

