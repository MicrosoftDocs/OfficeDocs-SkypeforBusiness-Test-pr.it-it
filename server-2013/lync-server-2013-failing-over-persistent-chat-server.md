---
title: 'Lync Server 2013: Failover del server Chat persistente'
TOCTitle: Failover del server Chat persistente
ms:assetid: 2cd79ffd-fee6-44ce-96cf-b98bf25e2690
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204772(v=OCS.15)
ms:contentKeyID: 49300042
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Failover del server Chat persistente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-02-05_

Il failover per il server Chat persistente è stato progettato come un processo principalmente manuale.

La procedura di failover si basa sul presupposto che il data center secondario sia attivo e in esecuzione e che i servizi del server Chat persistente in cui è ubicato il database primario Chat persistente non siano affatto disponibili, inclusi i seguenti:

  - Il database primario del server Chat persistente e il database mirror del server Chat persistente (inattivi).

  - Lync ServerFront End Server (inattivo).

La procedura prevede due passaggi di base:

  - Ripristino del database Chat persistente primario (mgc).

  - Configurazione del mirroring per il nuovo database primario.

Il database di conformità Chat persistente (mgccomp) non viene sottoposto a failover. Il contenuto di questo database è temporaneo e viene eliminato durante l'elaborazione dei dati nell'adattatore di conformità. È responsabilità dell'utente, in qualità di amministratore di Chat persistente, gestire correttamente l'output dell'adattatore per evitare una perdita dei dati.

## Per eseguire il failover di server Chat persistente

1.  Rimuovere la distribuzione dei log dal database Backup Log Shipping del server Chat persistente.
    
    1.  Usando SQL Server Management Studio, connettersi all'istanza del database in cui si trova il database mgc di backup del server Chat persistente.
    
    2.  Aprire una finestra di query nel database master.
    
    3.  Usare questo comando per eliminare la distribuzione dei log:
        
            exec sp_delete_log_shipping_secondary_database mgc

2.  Copiare i file di backup non copiati dalla condivisione di backup nella cartella di destinazione della copia del server di backup.

3.  Applicare i backup dei log delle transazioni non applicati in sequenza al database secondario. Per informazioni dettagliate, vedere "Procedura: Applicazione di un backup del log delle transazioni (Transact-SQL)" all'indirizzo http://go.microsoft.com/fwlink/?linkid=247428\&clcid=0x410

4.  Connettere il database mgc di backup. Usando la finestra di query aperta al passaggio 1b, eseguire le operazioni seguenti:
    
    1.  Terminare tutte le connessioni al database mgc, se disponibili:
        
        1.  **exec sp\_who2** per identificare le connessioni al database mgc.
        
        2.  **kill \<spid\>** per terminare queste connessioni.
    
    2.  Connettere il database:
        
        1.  **restore database mgc with recovery**.

5.  In Lync Server Management Shell utilizzare il comando **Set-CsPersistentChatState -Identity "service:atl-cs-001.litwareinc.com" –PoolState FailedOver** per il failover sul database di backup mgc. Assicurarsi di sostituire il nome di dominio completo del pool di Chat persistente per atl-cs-001.litwareinc.com.
    
    Il database mgc di backup funge ora da database primario.

6.  In Lync Server Management Shell usare il cmdlet **Install-CsMirrorDatabase** per stabilire un mirror a disponibilità elevata per il database di backup che ora funge da database primario. Usare l'istanza del database di backup come database primario e l'istanza del database mirror di backup come istanza mirror. Questo mirror non corrisponde al mirror configurato inizialmente per il database primario durante l'installazione. Per informazioni dettagliate, vedere la sezione "Uso dei cmdlet di Lync Server Management Shell" in [Distribuzione del mirroring di SQL per la disponibilità elevata del server back-end in Lync Server 2013](lync-server-2013-deploying-sql-mirroring-for-back-end-server-high-availability.md).

7.  Impostare i server attivi del server Chat persistente. Dalla shell dei comandi di Lync Server usare il cmdlet **Set-CsPersistentChatActiveServer** per impostare l'elenco dei server attivi.
    
    > [!important]  
    > Tutti i server attivi devono essere collocati nello stesso centro dati del nuovo database primario oppure in un centro dati con una connessione a bassa latenza e con larghezza di banda elevata al database.    
    A questo punto, il failover dal database primario del server Chat persistente al database di backup del server Chat persistente viene completato.

