---
title: 'Lync Server 2013: Failback del server Chat persistente'
TOCTitle: Failback del server Chat persistente
ms:assetid: 67b91de4-6ddc-43e6-9812-5e1aa84a7980
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204970(v=OCS.15)
ms:contentKeyID: 49300834
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Failback del server Chat persistente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-02-05_

Questa procedura descrive i passaggi necessari per eseguire il ripristino da un errore di un server Chat persistente e per ristabilire l'operatività dal centro dati principale.

Nel caso un errore del server Chat persistente, il centro dati principale risulta completamente interrotto e i database primario e mirror diventano non disponibili. Il centro dati principale esegue il failover al server di backup.

La procedura seguente consente di ripristinare l'operatività normale dopo il backup del centro dati principale e la ricostruzione dei server. Nella procedura si presuppone che il centro dati principale venga ripristinato dopo un'interruzione totale e che i database mgc e mgccomp siano stati ricostruiti e reinstallati tramite Generatore di topologie.

La procedura presuppone inoltre che durante il periodo di failover non siano stati distribuiti nuovi server mirror e di backup e che l'unico server distribuito sia il server di backup con il relativo server mirror, come definito in [Failover del server Chat persistente in Lync Server 2013](lync-server-2013-failing-over-persistent-chat-server.md).

Questi passaggi sono pensati per consentite il ripristino della configurazione esistente prima della situazione di emergenza che ha causato il failover dal server primario a quello di backup.

## Per eseguire il failback del server Chat persistente

1.  Cancellare tutti i server dall'elenco dei server attivi del server Chat persistente utilizzando il cmdlet `Set-CsPersistentChatActiveServer` da Lync Server Management Shell. Verrà così impedito a tutti i server Chat persistente di connettersi ai database mgc e mgccomp durante il failback.
    
    > [!IMPORTANT]  
    > È necessario che SQL Server Agent sia in esecuzione nel server back-end di server Chat persistente secondario con un account privilegiato. In particolare, l'account deve disporre di:    <ul>    
> 
> <li><p>Accesso in lettura alla condivisione di rete in cui vengono posizionati i backup.</p></li>    
> 
> 
> <li><p>Accesso in scrittura alla directory locale specifica in cui vengono copiati i backup.</p></li>    </ul>


2.  Disabilitare il mirroring nel database mgc di backup:
    
    1.  Utilizzare SQL Server Management Studio e connettersi all'istanza del database mgc di backup.
    
    2.  Fare clic con il pulsante destro del mouse sul database mgc, scegliere **Attività** e quindi fare clic su **Server mirror** .
    
    3.  Fare clic su **Rimuovi mirroring** .
    
    4.  Fare clic su **OK** .
    
    5.  Eseguire gli stessi passaggi con il database mgccomp.

3.  Eseguire il backup del database mgc in modo che possa essere ripristinato nel nuovo database primario:
    
    1.  Utilizzare SQL Server Management Studio e connettersi all'istanza del database mgc di backup.
    
    2.  Fare clic con il pulsante destro del mouse sul database mgc, scegliere **Attività** e quindi fare clic su **Backup** . Verrà visualizzata la finestra di dialogo **Backup database** .
    
    3.  In **Tipo backup** selezionare **Completo** .
    
    4.  In **Componente di cui eseguire il backup** fare clic su **Database** .
    
    5.  Accettare il nome del set di backup predefinito indicato in **Nome** oppure immettere un nome diverso per il set di backup.
    
    6.  *\<Facoltativo\>* In **Descrizione** immettere una descrizione del set di backup.
    
    7.  Rimuovere il percorso di backup predefinito dall'elenco di destinazione.
    
    8.  Aggiungere un file all'elenco utilizzando il percorso della posizione condivisa stabilita per il log shipping. Questo percorso è disponibile per il database primario e quello di backup.
    
    9.  Fare clic su **OK** per chiudere la finestra di dialogo e avviare il processo di backup.

4.  Ripristinare il database primario utilizzando il database di backup creato nel passaggio precedente.
    
    1.  Utilizzare SQL Server Management Studio e connettersi all'istanza del database mgc primario.
    
    2.  Fare clic con il pulsante destro del mouse sul database mgc, scegliere **Attività** , **Ripristina** e quindi fare clic su **Database** . Verrà visualizzata la finestra di dialogo **Ripristina database** .
    
    3.  Selezionare **Dispositivo di origine** .
    
    4.  Fare clic sul pulsante Sfoglia per aprire la finestra di dialogo **Seleziona backup** . In **Supporti di backup** selezionare **File** . Fare clic su **Aggiungi** , selezionare il file di backup creato nel passaggio 3 e quindi fare clic su **OK** .
    
    5.  In **Selezionare i set di backup da ripristinare** selezionare il backup.
    
    6.  Fare clic su **Opzioni** nel riquadro **Selezione pagina** .
    
    7.  In **Opzioni di ripristino** selezionare **Sovrascrivi il database esistente** .
    
    8.  In **Stato di recupero** selezionare **Lascia il database pronto per l'utilizzo** .
    
    9.  Fare clic su **OK** per avviare il processo di ripristino.

5.  Configurare il log shipping di SQL Server per il database primario. Seguire le procedure in [Configurazione del server Chat persistente per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013](lync-server-2013-configuring-persistent-chat-server-for-high-availability-and-disaster-recovery.md) per configurare il log shipping per il database mgc primario.

6.  Impostare i server attivi del server Chat persistente. In Lync Server Management Shell utilizzare il cmdlet **Set-CsPersistentChatActiveServer** per impostare l'elenco dei server attivi.
    
    > [!IMPORTANT]  
    > Tutti i server attivi devono essere collocati nello stesso centro dati del nuovo database primario oppure in un centro dati con una connessione a bassa latenza e con larghezza di banda elevata al database.

Per ripristinare lo stato normale del pool, eseguire il comando seguente di Windows PowerShell:

    Set-CsPersistentChatState -Identity "service: lyncpc.dci.discovery.com" -PoolState Normal

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Set-CsPersistentChatState](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsPersistentChatState).

