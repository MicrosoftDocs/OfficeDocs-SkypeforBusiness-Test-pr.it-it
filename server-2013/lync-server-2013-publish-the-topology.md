---
title: 'Lync Server 2013: Pubblicare la topologia'
TOCTitle: Pubblicare la topologia
ms:assetid: 3b5a744b-b3a8-4538-a55e-e2e4f72dff47
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425880(v=OCS.15)
ms:contentKeyID: 49300250
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pubblicare la topologia in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-10-01_

Per pubblicare, abilitare o disabilitare correttamente una topologia quando si aggiunge o si rimuove un ruolo del server, è necessario essere connessi come utenti membri dei gruppi RTCUniversalServerAdmins e Domain Admins. È inoltre possibile delegare le autorizzazioni e i diritti di amministratore appropriati. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md). Per poter apportare altre modifiche relative alla configurazione, è necessario appartenere solo al gruppo RTCUniversalServerAdmins.

Dopo aver definito la topologia in Generatore di topologie, è necessario pubblicarla nell' archivio di gestione centrale. L' archivio di gestione centrale offre un meccanismo di archiviazione schematizzata avanzata per i dati necessari per la definizione, la configurazione, la gestione, l'amministrazione, la descrizione e l'utilizzo di una distribuzione di Lync Server 2013. Consente inoltre di convalidare i dati per garantire la coerenza della configurazione. Tutte le modifiche dei dati di configurazione avvengono a livello dell' archivio di gestione centrale, eliminando i problemi dovuti alla mancanza di sincronizzazione. Le copie di sola lettura dei dati sono replicate in tutti i server della topologia, inclusi i server perimetrali.


> [!NOTE]
> SQL Server richiede almeno 20 GB di spazio libero per pubblicare la topologia iniziale e creare il server di gestione centrale.




> [!NOTE]
> Solo per Enterprise Edition: per pubblicare la topologia, il server back-end basato su SQL Server deve essere online e accessibile con le eccezioni del firewall configurate. Per informazioni dettagliate su come specificare le eccezioni del firewall, vedere <A href="lync-server-2013-understanding-firewall-requirements-for-sql-server.md">Informazioni sui requisiti del firewall per SQL Server con Lync Server 2013</A>. Per informazioni dettagliate sulla configurazione di SQL Server, vedere <A href="lync-server-2013-configure-sql-server-for-lync-server.md">Configurare SQL Server per Lync Server 2013</A>.



## Per pubblicare una topologia

1.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

2.  Scegliere di aprire la topologia da un file locale. Se si utilizza il computer in cui è stata definita la topologia, il file si troverà nel percorso in cui è stato precedentemente salvato, generalmente nella cartella Documenti dell'utente che ha configurato la topologia.

3.  Fare clic con il pulsante destro del mouse sul nodo **Lync Server 2013** e scegliere **Pubblica topologia** .

4.  Nella pagina **Pubblicare la topologia** fare clic su **Avanti** .

5.  Nella pagina **Creare database** selezionare i database che si desidera pubblicare.
    

    > [!NOTE]
    > Se non si dispone dei diritti appropriati per creare i database, è possibile deselezionare le caselle di controllo accanto a tali database e un utente con i diritti appropriati potrà successivamente crearli. Per informazioni dettagliate, vedere <A href="lync-server-2013-deployment-permissions-for-sql-server.md">Autorizzazioni di distribuzione per SQL Server in Lync Server 2013</A>.



6.  Facoltativamente, fare clic su **Avanzate** . Le opzioni avanzate di posizionamento dei file di dati di SQL Server consentono di scegliere tra le opzioni seguenti:
    
      - **Determina automaticamente il percorso dei file di database** - Questa opzione determinerà le prestazioni operative migliori in base alla configurazione del disco nel server basato su SQL Server distribuendo i file di registro e di dati nel percorso migliore.
    
      - **Utilizza i valori predefiniti dell'istanza di SQL Server** - Questa opzione posiziona i file di registro e di dati nel server basato su SQL Server utilizzando le impostazioni dell'istanza. Non utilizza la funzionalità operativa del server basato su SQL Server di determinazione dei percorsi ottimali per i registri e i dati. L'amministratore di SQL Server in genere sposta i file di registro e di dati nei percorsi appropriati per le procedure di gestione del server basato su SQL Server e dell'organizzazione.
    
    Fare clic su **OK** e quindi su **Avanti** .

7.  Nella pagina **Selezionare server di gestione centrale** selezionare un pool Front End.

8.  Facoltativamente, fare clic su **Avanzate** . Le opzioni avanzate di posizionamento dei file di dati di SQL Server consentono di scegliere tra le opzioni seguenti:
    
      - **Determina automaticamente il percorso dei file di database** - Questa opzione determinerà le prestazioni operative migliori in base alla configurazione del disco nel server basato su SQL Server distribuendo i file di registro e di dati nel percorso migliore.
    
      - **Utilizza i valori predefiniti dell'istanza di SQL Server** - Questa opzione posiziona i file di registro e di dati nel server basato su SQL Server utilizzando le impostazioni dell'istanza. Non utilizza la funzionalità operativa del server basato su SQL Server di determinazione dei percorsi ottimali per i registri e i dati. L'amministratore di SQL Server in genere sposta i file di registro e di dati nei percorsi appropriati per le procedure di gestione del server basato su SQL Server e dell'organizzazione.
    
    Fare clic su **OK** .

9.  Fare clic su **Avanti** per completare il processo di pubblicazione.

10. Al termine del processo di pubblicazione, fare clic su **Fine** .
    
    Dopo la pubblicazione della topologia, è possibile iniziare a installare una replica locale dell' archivio di gestione centrale in ogni server che esegue Lync Server 2013 nella topologia. È consigliabile iniziare con il primo pool Front End.

## Vedere anche

#### Ulteriori risorse

[Configurazione di Front End Server e pool Front End per Lync Server 2013](lync-server-2013-setting-up-front-end-servers-and-front-end-pools.md)

