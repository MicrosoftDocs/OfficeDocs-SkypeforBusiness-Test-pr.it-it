---
title: 'Lync Server 2013: Configurazione del log shipping di SQL Server tra il mirror primario e il database secondario di log shipping'
TOCTitle: Configurazione del log shipping di SQL Server tra il mirror primario e il database secondario di log shipping
ms:assetid: 4e8e9ce9-4301-47f2-a0c3-669afeb53295
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204887(v=OCS.15)
ms:contentKeyID: 49300499
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione del log shipping di SQL Server tra il mirror primario e il database secondario di log shipping in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

Eseguire la procedura seguente per continuare il log shipping se per il database Chat persistente primario si attiva il failover al database mirror.

1.  Eseguire manualmente il failover del database Chat persistente primario al database mirror. A tale scopo usare Lync Server Management Shell e il cmdlet **Invoke-CsDatabaseFailover**. Per informazioni dettagliate, vedere "Uso di cmdlet Lync Server Management Shell" in [Distribuzione del mirroring di SQL per la disponibilità elevata del server back-end in Lync Server 2013](lync-server-2013-deploying-sql-mirroring-for-back-end-server-high-availability.md).

2.  Usando SQL Server Management Studio, connettersi all'istanza del mirror server Chat persistente primario.

3.  Assicurarsi che l'agente SQL Server sia in esecuzione.

4.  Fare clic con il pulsante destro del mouse sul database mgc e quindi scegliere **Proprietà** .

5.  In **Selezione pagina** fare clic su **Log shipping delle transazioni** .

6.  Selezionare la casella di controllo **Abilita come database primario in una configurazione per il log shipping** .

7.  In **Backup log delle transazioni** fare clic su **Impostazioni backup** .

8.  Nella casella **Specificare il percorso di rete della cartella di backup** digitare il percorso di rete della condivisione creata per la cartella di backup dei log delle transazioni.

9.  Se la cartella di backup si trova nel server primario, digitare il percorso locale della cartella di backup nella casella **Se la cartella di backup si trova nel server primario, digitare il percorso locale della cartella** . Se la cartella di backup non è nel server primario, lasciare vuota questa casella.
    
    > [!IMPORTANT]  
    > Se l'account del servizio SQL Server nel server primario viene eseguito con l'account di sistema locale, è necessario creare la cartella di backup nel server primario e specificare il percorso locale della cartella.

10. Configurare i parametri **Elimina i file più vecchi di** e **Invia avviso se il backup non viene eseguito entro** .

11. Esaminare il programma del backup presente nella cartella **Pianificazione** in **Processo di backup** . Per personalizzare la pianificazione dell'installazione, fare clic su **Pianificazione** e modificare la pianificazione dell'agente SQL Server secondo le esigenze.
    
    > [!IMPORTANT]  
    > Usare le stesse impostazioni del database primario.

12. In **Compressione** selezionare **Utilizza l'impostazione predefinita del server** e fare clic su **OK** .

13. In **Istanze del server e database secondari** fare clic su **Aggiungi** .

14. Fare clic su **Connetti** e connettersi all'istanza di SQL Server configurata come server secondario.

15. Nella casella **Database secondario** selezionare il database **mgc** dall'elenco.

16. Nella scheda **Inizializza database secondario** selezionare l'opzione **No, il database secondario è già inizializzato** .

17. Nella scheda **Copia file** , in **Cartella di destinazione per i file copiati** , digitare il percorso della cartella in cui copiare i backup dei log delle transazioni e fare clic su **OK** . Spesso questa cartella si trova nel server secondario.

18. Aprire l'elenco a discesa **Script configurazione** e selezionare **Genera script configurazione in nuova finestra Query** .

19. Nella nuova finestra Query, in **Proprietà database** , fare clic su **OK** per avviare il processo di configurazione.

20. Selezionare ed eseguire la prima metà della query (vedere il passaggio 18) fino alla riga: -- \*\*\*\*\*\* Fine: script da eseguire nel server primario: \*\*\*\*\*\*.
    
    > [!IMPORTANT]  
    > È necessario eseguire manualmente questo script perché SQL Server Management Studio non supporta più di un database primario in una configurazione di log shipping di SQL Server.

21. Selezionare **Annulla** per chiudere il pannello di configurazione del log shipping e stabilire una configurazione funzionante per l'implementazione corretta del log shipping sia per il database primario che per il database mirror, in caso di failover.

22. Eseguire manualmente il failback del database Chat persistente primario al database primario. A tale scopo usare Lync Server Management Shell e il cmdlet **Invoke-CsDatabaseFailover**. Per informazioni dettagliate, vedere "Uso di cmdlet Lync Server Management Shell" in [Distribuzione del mirroring di SQL per la disponibilità elevata del server back-end in Lync Server 2013](lync-server-2013-deploying-sql-mirroring-for-back-end-server-high-availability.md).

## Vedere anche

#### Concetti

[Distribuzione del mirroring di SQL per la disponibilità elevata del server back-end in Lync Server 2013](lync-server-2013-deploying-sql-mirroring-for-back-end-server-high-availability.md)  
[Distribuzione del mirroring di SQL per la disponibilità elevata del server back-end in Lync Server 2013](lync-server-2013-deploying-sql-mirroring-for-back-end-server-high-availability.md)

