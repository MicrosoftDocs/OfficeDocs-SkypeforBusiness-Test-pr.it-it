---
title: Ripristino di un server Standard Edition
TOCTitle: Ripristino di un server Standard Edition
ms:assetid: d1845663-3138-4fd6-b3e7-337e294d40d8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh202190(v=OCS.15)
ms:contentKeyID: 52062313
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ripristino di un server Standard Edition

 

_**Ultima modifica dell'argomento:** 2013-02-21_

In caso di errore di un server Standard Edition che non ospita archivio di gestione centrale, seguire le procedure riportate in questa sezione. In caso di errore dell'archivio di gestione centrale, vedere [Ripristino del server che ospita l'archivio di gestione centrale](lync-server-2013-restoring-the-server-hosting-the-central-management-store.md).

> [!tip]  
> È consigliabile creare una copia dell'immagine del sistema prima di avviare il ripristino. È possibile utilizzare questa immagine come punto di rollback, in caso di problemi durante il ripristino. Potrebbe essere utile creare la copia dell'immagine dopo avere installato il sistema operativo e SQL Server, quindi ripristinare o registrare nuovamente i certificati.

## Per ripristinare un server Standard Edition

1.  Iniziare con un server pulito o nuovo che dispone dello stesso nome di dominio completo (FQDN) del computer in cui si è verificato l'errore, installare il sistema operativo e quindi ripristinare o registrare di nuovo i certificati.
    

    > [!NOTE]
    > Per eseguire questo passaggio, attenersi alle procedure per la distribuzione del server dell'organizzazione.



2.  Accedere al server da ripristinare utilizzando un account utente membro del gruppo RTCUniversalServerAdmins e del gruppo Administrators locale.

3.  Ripristinare l'Archivio file copiando l'Archivio file appropriato da $Backup nella posizione dell'Archivio file sul server e condividere la cartella.
    
    > [!IMPORTANT]  
    > Il nome del percorso e del file dell'Archivio file ripristinato devono essere identici a quelli dell'Archivio file di cui è stato eseguito il backup in modo che i componenti che utilizzano i file possano accedervi.

4.  Eseguire Generatore di topologie:
    
    1.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.
    
    2.  Fare clic su **Scarica topologia dalla distribuzione esistente** e quindi su **OK**.
    
    3.  Selezionare la topologia e quindi fare clic su **Salva**. Fare clic su **Sì** per confermare la selezione.

5.  Passare alla cartella o al supporto di installazione di Lync Server, avviare la Distribuzione guidata di Lync Server disponibile nel percorso \\setup\\amd64\\Setup.exe. Utilizzare la Distribuzione guidata di Lync Server per eseguire le operazioni seguenti:
    
    1.  Eseguire **Passaggio 1: Installazione dell'archivio di configurazione locale** per installare i file di configurazione locali.
    
    2.  Eseguire **Passaggio 2: Installazione o rimozione componenti di Lync Server** per installare i ruoli server di Lync Server.
    
    3.  Eseguire **Passaggio 3: Richiesta, installazione o assegnazione dei certificati** per assegnare i certificati.
    
    4.  Eseguire **Passaggio 4: Avvio servizi** per avviare i servizi sul server.
    
    Per informazioni dettagliate sull'esecuzione della Distribuzione guidata, vedere la documentazione relativa alla distribuzione per il ruolo server che si sta ripristinando.

6.  Ripristinare i dati utente eseguendo le operazioni seguenti:
    
    1.  Copiare ExportedUserData.zip da $Backup\\ in una directory locale.
    
    2.  Prima di ripristinare i dati utente, è necessario arrestare i servizi di Lync. A tale scopo, digitare:
        
            Stop-CsWindowsService
    
    3.  Per ripristinare i dati utente, alla riga di comando digitare:
        
            Import-CsUserData -PoolFqdn <Fqdn> -FileName <String>
        
        Ad esempio:
        
            Import-CsUserData -PoolFqdn "atl0cs-001.litwareinc.com" -FileName "C:\Logs\ExportedUserDatal.zip"
    
    4.  Riavviare i servizi di Lync digitando:
        
            Start-CsWindowsService

7.  Se è stato distribuito Response Group in questo server Standard Edition, ripristinare i dati di configurazione di Response Group. Per informazioni dettagliate, vedere [Ripristino delle impostazioni di Response Group](lync-server-2013-restoring-response-group-settings.md).

8.  Se si è distribuito Chat persistente in questo server Standard Edition, ripristinare il database Chat persistente (mgc.mdf).
    
    Se è stato utilizzato il backup di SQL Server per eseguire il backup del database Chat persistente, utilizzare le procedure di ripristino di SQL Server per ripristinarlo.
    
    Se è stato utilizzato il cmdlet Export-CsPersistentChatData per eseguirne il backup, utilizzare Import-CsPersistentChatData per ripristinarlo.

