---
title: 'Lync Server 2013: Configurazione del log shipping di SQL Server per il database primario del server chat persistente'
TOCTitle: Configurazione del log shipping di SQL Server per il database primario del server chat persistente
ms:assetid: 088ea1c2-d592-4a11-b3b8-f1e2f8beae93
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204653(v=OCS.15)
ms:contentKeyID: 49299600
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione del log shipping di SQL Server in Lync Server 2013 per il database primario del server chat persistente

 

_**Ultima modifica dell'argomento:** 2012-11-12_

Utilizzando SQL Server Management Studio, eseguire la connessione all'istanza del database secondario per il log shipping di server Chat persistente e verificare che SQL Server Agent sia in esecuzione.

Utilizzando SQL Server Management Studio connesso all'istanza del database primario di Chat persistente, eseguire la procedura seguente:

1.  Assicurarsi che l'agente SQL Server sia in esecuzione.

2.  Fare clic con il pulsante destro del mouse sul database mgc e quindi scegliere **Proprietà** .

3.  In **Selezione pagina** fare clic su **Log shipping delle transazioni** .

4.  Selezionare la casella di controllo **Abilita come database primario in una configurazione per il log shipping** .

5.  In **Backup log delle transazioni** fare clic su **Impostazioni backup** .

6.  Nella casella **Specificare il percorso di rete della cartella di backup** digitare il percorso di rete della condivisione creata per la cartella di backup del log delle transazioni.

7.  Se la cartella di backup si trova nel server primario, digitare il percorso locale nella casella **Se la cartella di backup si trova nel server primario, digitare il percorso locale della cartella (esempio c:\\backup)** . In caso contrario si può lasciare la casella vuota.
    
    > [!important]  
    > Se l'account del servizio SQL Server nel server primario viene eseguito con l'account di sistema locale, è necessario creare la cartella di backup nel server primario e specificare il percorso locale della cartella.

8.  Configurare i parametri **Elimina i file più vecchi di** e **Invia avviso se il backup non viene eseguito entro** .

9.  Esaminare la pianificazione di backup indicata nella casella **Pianificazione** in **Processo di backup** . Per personalizzare la pianificazione dell'installazione fare clic su **Pianificazione** e modificare la pianificazione di SQL Server Agent in base alle proprie esigenze.

10. In **Compressione** selezionare **Utilizza l'impostazione predefinita del server** e quindi fare clic su **OK** .

11. In **Istanze del server e database secondari** fare clic su **Aggiungi** .

12. Fare clic su **Connetti** ed eseguire la connessione all'istanza di SQL Server configurata come server secondario.

13. Nella casella **Database secondario** selezionare il database **mgc** dall'elenco.

14. Nella scheda **Inizializza database secondario** selezionare l'opzione **Sì, genera un backup completo del database primario e ripristinalo nel database secondario (e crea il database secondario se non esiste)**.

15. Nella scheda **Copia file** , nella casella **Cartella di destinazione per i file copiati** digitare il percorso della cartella in cui copiare i backup del log delle transazioni. Questa cartella è spesso situata nel server secondario.

16. Esaminare la pianificazione di copia indicata nella casella **Pianificazione** in **Processo di copia** . Per personalizzare la pianificazione dell'installazione fare clic su **Pianificazione** e modificare la pianificazione di SQL Server Agent in base alle proprie esigenze. Questa pianificazione dovrebbe essere abbastanza simile alla pianificazione di backup.

17. Nella scheda **Ripristino** , in **Stato del database durante il ripristino dei backup** selezionare l'opzione **Modalità nessun recupero** .

18. In **Ritardo minimo per il ripristino dei backup:** selezionare **0 minuti** .

19. Scegliere una soglia di avviso nell'area **Invia avviso se il ripristino non viene eseguito entro** .

20. Esaminare la pianificazione di ripristino indicata nella casella **Pianificazione** in **Processo di ripristino** . Per personalizzare la pianificazione dell'installazione fare clic su **Pianificazione** , modificare la pianificazione di SQL Server Agent in base alle proprie esigenze e fare clic su **OK** . Questa pianificazione dovrebbe essere abbastanza simile alla pianificazione di backup.

21. Nella finestra di dialogo **Proprietà database** fare clic su **OK** per iniziare il processo di configurazione.

