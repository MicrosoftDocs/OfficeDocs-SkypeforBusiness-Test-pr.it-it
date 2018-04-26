---
title: Associazione di un archivio di monitoraggio a un pool Front End
TOCTitle: Associazione di un archivio di monitoraggio a un pool Front End
ms:assetid: d3a20d5e-3f24-4cff-bc9b-4f84fea30e6b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205271(v=OCS.15)
ms:contentKeyID: 49302082
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Associazione di un archivio di monitoraggio a un pool Front End

 

_**Ultima modifica dell'argomento:** 2013-04-22_

In Microsoft Lync Server 2013 i dati di monitoraggio possono essere raccolti solo nei pool Front End che sono stati associati a un archivio di monitoraggio, un'attività che in genere viene eseguita quando si definisce un pool Front End in Generatore di topologie. Per associare un archivio di monitoraggio a un nuovo pool Front End, selezionare l'opzione **Monitoraggio (registrazione dettagli chiamata e registrazione metrica QoE)** nella pagina **Selezionare funzionalità** della procedura guidata Definisci nuovo pool Front End. Si noti che se si seleziona questa opzione, sarà necessario inoltre specificare un archivio SQL per completare la procedura guidata. Questo archivio tuttavia non deve necessariamente esistere già al momento dell'esecuzione della procedura guidata. È possibile pertanto associare innanzitutto un pool a un archivio di monitoraggio e quindi installare e configurare l'archivio in seguito.

In alternativa, è possibile associare un pool Front End esistente a un archivio di monitoraggio nuovo o diverso eseguendo la procedura seguente:

1.  Fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie di Lync Server**.

2.  Nella finestra di dialogo **Generatore di topologie** selezionare **Scarica topologia dalla distribuzione esistente** e quindi fare clic su **OK**.

3.  Nella finestra di dialogo **Salva con nome** immettere un nome file per la topologia corrente e quindi fare clic su **Salva**. La topologia salvata può essere successivamente recuperata e ripubblicata in caso di problemi con la nuova topologia.

4.  In Generatore di topologie espandere **Lync Server 2013**, il nome del sito contenente il pool Front End e quindi **Pool Enterprise Edition Front End**.

5.  Fare clic con il pulsante destro del mouse sul nome del pool da associare all'archivio di monitoraggio e quindi scegliere **Modifica proprietà**.

6.  Nella finestra di dialogo **Modifica proprietà** nella scheda **Generale** selezionare l'opzione **Monitoraggio (registrazione dettagli chiamata e registrazione metrica QoE)** e quindi selezionare un database di SQL Server esistente nell'elenco a discesa **Archivio SQL Server monitoraggio**. In alternativa, fare clic su **Nuovo** per associare il pool a un nuovo archivio database. Se si sceglie di utilizzare il nuovo archivio database, nella finestra di dialogo **Definisci nuovo archivio SQL** immettere il nome di dominio completo del computer SQL Server nella casella **FQDN SQL Server**. Se si desidera utilizzare l'istanza di SQL Server predefinita per l'archivio, selezionare **Istanza predefinita**, altrimenti selezionare **Istanza denominata** e immettere il nome dell'istanza nella casella **Istanza denominata**.
    
    La finestra di dialogo **Modifica proprietà** consente inoltre di creare un mirror SQL per il database di monitoraggio. Un mirror SQL consente di mantenere due copie del database di monitoraggio, una archiviata nel computer dell'archivio di monitoraggio e l'altra nel computer mirror SQL. Per abilitare il mirroring, selezionare **L'istanza SQL è in relazione di mirroring** e immettere il numero di porta del server mirror nella casella **Numero porta di mirroring**.

7.  Nella finestra di dialogo **Modifica proprietà** fare clic su **OK**.

Dopo aver associato l'archivio di monitoraggio a un pool Front End, è necessario pubblicare la nuova topologia per rendere effettive le modifiche. A tale scopo, eseguire le operazioni seguenti in Generatore di topologie:

1.  Fare clic su **Azione**, scegliere **Topologia** e quindi **Pubblica**.

2.  Nella pagina **Pubblicare la topologia** della procedura guidata Pubblica topologia fare clic su **Avanti**.

3.  Nella pagina **Pubblicazione guidata completata** fare clic su **Fine**.

Dopo la pubblicazione della topologia, è possibile installare il database di monitoraggio nel computer che ospiterà l'archivio di monitoraggio. Il database di monitoraggio può essere installato utilizzando Lync Server Management Shell e Windows PowerShell. Per installare il database localmente, ovvero nello stesso computer in cui è in esecuzione Lync Server Management Shell, avviare Management Shell nel computer appropriato, digitare il comando seguente e quindi premere INVIO:

    Install-CsDatabase -LocalDatabases

Quando si esegue il comando sopra riportato, Install-CsDatabase legge la topologia di Lync Server corrente, determina i database da installare nel computer locale e quindi installa e configura automaticamente ognuno dei database.

Per installare il database in un computer remoto, ovvero un computer diverso da quello in cui è in esecuzione Management Shell, è necessario includere almeno due parametri: ConfiguredDatabases e SqlServerFqdn. Questi parametri indicano al cmdlet Install-CsDatabase di recuperare la topologia di Lync Server e quindi installare e configurare i database necessari nel computer specificato dal parametro SqlServerFqdn. Il parametro SqlServerFqdn deve utilizzare un valore di parametro che rappresenta il nome di dominio completo del computer in cui devono essere installati i database.

Con il comando seguente ad esempio il database di monitoraggio viene installato nel computer atl-sql-001.litwareinc.com:

    Install-CsDatabase -ConfiguredDatabases -SqlServerFqdn atl-sql-001.litwareinc.com

In alternativa, è possibile installare il database di monitoraggio eseguendo la Distribuzione guidata di Lync Server nel computer che ospiterà l'archivio di monitoraggio. A tale scopo, accedere al computer appropriato ed eseguire la procedura seguente:

1.  Fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Distribuzione guidata di Lync Server**.

2.  Nella Distribuzione guidata fare clic su **Installa o aggiorna il sistema Lync Server**.

3.  In **Passaggio 2: Installazione o rimozione componenti di Lync Server** nella pagina **Distribuisci** fare clic su **Riesegui**.

4.  Nella pagina **Installazione componenti di Lync Server** della procedura guidata Installazione componenti di Lync Server fare clic su **Avanti**.

5.  Nella pagina **Specifica il percorso dei file MSI** digitare il percorso del file Ocscore.msi (incluso nel supporto di installazione di Lync Server) e quindi fare clic su **Avanti**.

6.  Nella pagina **Esecuzione comandi in corso** fare clic su **Fine**.

Per verificare che siano in esecuzione tutti i servizi di Lync Server necessari, fare clic su **Esegui** al di sotto dell'intestazione **Passaggio 4: Avvio servizi** nella pagina **Distribuisci**.

