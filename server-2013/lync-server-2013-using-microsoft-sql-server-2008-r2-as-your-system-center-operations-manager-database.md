---
title: Utilizzo di Microsoft SQL Server 2008 R2 come database di System Center Operations Manager
TOCTitle: Utilizzo di Microsoft SQL Server 2008 R2 come database di System Center Operations Manager
ms:assetid: 0efe76da-8854-499e-bdc7-3623244a8e85
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ687969(v=OCS.15)
ms:contentKeyID: 49887444
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Utilizzo di Microsoft SQL Server 2008 R2 come database di System Center Operations Manager

 

_**Ultima modifica dell'argomento:** 2013-07-29_

Per utilizzare SQL Server 2008 R2 come database back-end, eseguire la procedura illustrata in questo argomento.

## Configurazione di SQL Server 2008 R2 e SQL Server Reporting Services

Prima di iniziare l'installazione di System Center Operations Manager, è necessario apportare due modifiche a SQL Server 2008 R2 e alla configurazione di SQL Server Reporting Services (queste modifiche sono necessarie solo se si utilizza SQL Server 2008 R2 come database di Operations Manager). Innanzitutto, eseguire la procedura seguente sul computer che ospiterà il database di Operations Manager:

1.  Fare clic sul pulsante **Start**, quindi scegliere **Esegui**.

2.  Nella finestra di dialogo **Esegui** digitare **C:\\Programmi\\Microsoft SQL Server\\ MSRS10\_50.ARCHINST\\Reporting Services\\ReportServer** e premere INVIO.

3.  Nella cartella **ReportServer** aprire il file **rsreportserver.config** nel Blocco note o in un altro editor di testo.

4.  Quasi all'inizio del file è presente una serie di nodi "Add Key". Individuare la voce che inizia con **\<Add Key="SecureConnectionLevel"** e impostare il valore su **0**:
    
        <Add Key="SecureConnectionLevel" Value="0"/>

5.  Salvare il file **rsreportserver.config** e chiudere l'editor di testo.

Dopo avere aggiornato il file di configurazione del server di report, è necessario assegnare il certificato corretto a SQL Server Reporting Services. A questo scopo:

1.  Fare clic su **Start**, scegliere **Tutti i programmi**, **Microsoft SQL Server 2008 R2**, **Strumenti di configurazione** e quindi **Gestione configurazione Reporting Services**.

2.  Nella finestra di dialogo **Connessione configurazione Reporting Services** verificare che nella casella **Nome server** sia presente il nome del server. Selezionare l'istanza di SQL Server che ospiterà il database di Operations Manager, ad esempio **ARCHINST**, nell'elenco a discesa **Istanza server di report**, quindi fare clic su **Connetti**.

3.  In Gestione configurazione Reporting Services fare clic su **URL servizio Web**.

4.  Nella pagina **URL servizio Web** selezionare il certificato da utilizzare per l'istanza di Reporting Services nell'elenco a discesa **Certificato SSL**, quindi fare clic su **Applica**. Dopo alcuni secondi comparirà una coppia di URL in **URL servizio Web ReportServer**.

5.  Fare clic su entrambi gli URL per verificare di poter accedere a SQL Server Reporting Services.

6.  Chiudere Gestione configurazione Reporting Services.

## Creazione di un database di System Center Operations Manager da utilizzare con SQL Server 2008 R2

Per configurare System Center Operations Manager per l'utilizzo di un database di SQL Server 2008 R2, sarà necessario creare "manualmente" il database di Operations Manager nel computer che esegue SQL Server 2008 R2. Anche in questo caso, questa procedura è necessaria solo se si utilizza SQL Server 2005 o SQL Server 2008 come database back-end.

Per creare manualmente un database di Operations Manager, eseguire le operazioni seguenti:

1.  Nel supporto di installazione di System Center Operations Manager 2007 R2, nella cartella SupportTools\\AMD64, fare doppio clic su **DBCreateWizard.exe**.

2.  Nella pagina iniziale della **Configurazione guidata database** fare clic su **Avanti**.

3.  Nella pagina **Informazioni database** lasciare invariate tutte le impostazioni e fare clic su **Avanti**

4.  Nella pagina **Configurazione gruppo di gestione** digitare un nome per il gruppo di gestione, ad esempio **Lync Server Monitoring**, nella casella **Nome gruppo di gestione**, quindi fare clic su **Avanti**.

5.  Nella pagina **Segnalazioni errori di Operations Manager** fare clic su **Avanti**.

6.  Nella pagina **Riepilogo** fare clic su **Fine**.

## Creazione di un data warehouse di System Center Operations Manager da utilizzare con SQL Server 2008 R2

Microsoft Lync Server 2013 include tre nuovi report di System Center Operations Manager:

  - **End to End Scenario Availability Report**   Questo report include informazioni dettagliate su disponibilità/tempi di attività per i servizi chiave di Lync Server come la registrazione o la presenza.

  - **Capacity Report**   Utilizzando le informazioni dei contatori delle prestazioni, questo report mostra le tendenze relative ai componenti del sistema, ad esempio la disponibilità di memoria e l'utilizzo del processore.

  - **Component Report**   In questo report sono elencati i principali generatori di avvisi raggruppati per componente di Lync Server.

Per utilizzare questi nuovi report è necessario installare un data warehouse di System Center Operations Manager (un data warehouse fornisce l'archiviazione a lungo termine per i dati relativi alle operazioni). Per utilizzare un data warehouse con SQL Server 2008 R2, è necessario eseguire la procedura seguente nel computer che ospita il database di SQL Server:

1.  Nel supporto di installazione di System Center Operations Manager, nella cartella Setup\\SupportTools\\AMD64, fare doppio clic su **DBCreateWizard.exe**.

2.  Nella pagina iniziale della **Configurazione guidata database** fare clic su **Avanti**.

3.  Nella pagina **Informazioni database** selezionare **Database data warehouse di Operations Manager** nell'elenco a discesa **Tipo database**, quindi fare clic su **Avanti**.

4.  Nella pagina **Riepilogo** fare clic su **Fine**.

## Installazione della console di System Center Operations Manager

La console di Operations Manager è lo strumento principale per la gestione di System Center Operations Manager. Prima di installare la console di Operations Manager, assicurarsi di avere installato una versione supportata di SQL Server insieme a SQL Server Reporting Service. È inoltre consigliabile eseguire Gestione configurazione Reporting Services di SQL Server per verificare che Reporting Service sia installato e configurato correttamente.

Per installare la console di System Center Operations Manager:

1.  Nel supporto di installazione di System Center Operations Manager fare doppio clic su **SetupOM.exe**.

2.  In Installazione di System Center Operations Manager 2007 R2 fare clic su **Verifica prerequisiti**.

3.  In Visualizzatore prerequisiti System Center Operations Manager selezionare i componenti di System Center da installare (**Server**, **Console** e **PowerShell**), quindi fare clic su **Controlla**. Verificare che non siano stati riscontrati problemi gravi e quindi fare clic su **Chiudi**. Se viene segnalato un problema grave, correggerlo e fare clic su **Controlla** per ripetere il test dei prerequisiti.

4.  In Installazione di System Center Operations Manager fare clic su **Installa Operations Manager**.

5.  Nell'installazione guidata di System Center Operations Manager, nella pagina **Installazione guidata di System Center Operations Manager**, fare clic su **Avanti**.

6.  Nella pagina **Contratto di licenza con l'utente finale** selezionare **Accetto i termini del Contratto di licenza** e fare clic su **Avanti**.

7.  Nella pagina **Registrazione prodotto** digitare il proprio nome nella casella **Nome utente** e il nome dell'organizzazione nella casella **Organizzazione**. Digitare il codice Product Key di System Center Operations Manager nella casella **Inserire le 25 cifre del codice CD Key**, quindi fare clic su **Avanti**.

8.  Nella pagina **Installazione personalizzata** selezionare le opzioni di System Center da installare, quindi fare clic su **Avanti**. È consigliabile selezionare **Server di gestione**, **Interfacce utente** e **Console Web** per l'installazione, ma non selezionare e installare **Database**.

9.  Nella pagina **Istanza server di database SC** verificare che il nome del computer in cui sono installati i database di Operations Manager sia riportato nella casella **Server di database SC**. Fare clic su **Avanti**.

10. Nella pagina **Account azione server di gestione** selezionare **Dominio o account computer locale** e immettere i valori appropriati nelle caselle **Account utente**, **Password** e **Dominio o computer locale**. Fare clic su **Avanti**.

11. Nella pagina **SDK e account servizio di configurazione** selezionare **Dominio o account computer locale** e immettere i valori appropriati nelle caselle **Account utente**, **Password** e **Dominio o computer locale**. Fare clic su **Avanti**.

12. Nella pagina **Segnalazioni errori di Operations Manager** fare clic su **Avanti**.

13. Nella pagina **Analisi utilizzo software** fare clic su **Avanti**.

14. Nella pagina **Installazione del programma** fare clic su **Avanti**.

15. Nella pagina finale dell'**Installazione di System Center Operations Manager** deselezionare le caselle di controllo **Backup chiave di crittografia** e **Avvia console**, quindi fare clic su **Fine**.

16. In Installazione di System Center Operations Manager fare clic su **Esci**.

## Installazione di System Center Reporting Services

Dopo avere installato e configurato la console di System Center Operations Manager è necessario installare System Center Reporting Services. Se si utilizza SQL Server 2008 R2 come database back-end di Operations Manager, è necessario innanzitutto apportare una modifica temporanea al gruppo di sicurezza associato a SQL Server Reporting Services. Se si utilizza SQL Server 2008 R2, eseguire le operazioni seguenti:

1.  Fare clic su **Start**, scegliere **Strumenti di amministrazione**, quindi **Server Manager**.

2.  In Server Manager espandere **Configurazione** e **Utenti e gruppi locali**, quindi fare clic su **Gruppi**.

3.  Individuare il gruppo seguente, in cui atl-sc-001 rappresenta il nome del computer e ARCHINST rappresenta l'istanza di SQL Server per il database System Center: **SQLServerReportServerUser$atl-sc-001$MSRS10\_50.ARCHINST**.

4.  Fare clic con il pulsante destro del mouse sul gruppo e scegliere **Rinomina**. Rinominare il gruppo eliminando **\_50** dal nome del gruppo, ad esempio: **SQLServerReportServerUser$atl-sc-001$MSRS10.ARCHINST**.

5.  Chiudere Server Manager.

A questo punto è possibile installare System Center Reporting Services. Procedere nel modo seguente:

1.  Nel supporto di installazione di System Center Operations Manager 2007 R2 fare doppio clic su **SetupOM.exe**.

2.  In Installazione di System Center Operations Manager 2007 R2 fare clic su **Installa Operations Manager**.

3.  Nella pagina **Installazione componente di report di Operations Manager** dell'installazione guidata del componente di report di System Center Operations Manager 2007 R2 fare clic su **Avanti**.

4.  Nella pagina **Contratto di licenza con l'utente finale** selezionare **Accetto i termini del Contratto di licenza** e fare clic su **Avanti**.

5.  Nella pagina **Registrazione prodotto** verificare che nelle caselle **Nome utente** e **Organizzazione** siano presenti il proprio nome e il nome dell'organizzazione, quindi fare clic su **Avanti**.

6.  Nella pagina **Installazione personalizzata** fare clic su **Server di report** e selezionare **Il componente e tutti i componenti secondari verranno installati sul disco rigido locale**. Fare clic su **Data warehouse** e selezionare **Il componente non sarà disponibile**, quindi fare clic su **Avanti**.

7.  Nella pagina **Connetti al server di gestione principale** digitare il nome del server di gestione principale di Operations Manager nella casella **Server di gestione principale** e fare clic su **Avanti**.

8.  Nella pagina **Connetti al data warehouse Operations Manager**, nella casella **Istanza di SQL Server**, digitare l'istanza di SQL Server in cui si trova il data warehouse (se il data warehouse si trova nell'istanza predefinita, è sufficiente digitare il nome del server, ad esempio atl-sql-001). Verificare che nella casella **Nome** sia riportato il nome **OperationsManagerDW** e che nella casella **Porta SQL Server** sia presente **1433**. Fare clic su **Avanti**.

9.  Nella pagina **Istanza di SQL Server Reporting Services** selezionare il server di report di SQL Server nell'elenco a discesa **Immettere il server SQL Server Reporting Services** e fare clic su **Avanti**.

10. Nella pagina **Account scrittura data warehouse**, nelle caselle **Account utente** e **Password** immettere il nome e la password dell'utente a cui assegnare inizialmente le autorizzazioni di scrittura per il data warehouse. Selezionare il dominio dell'utente nell'elenco a discesa **Dominio** e fare clic su **Avanti**.

11. Nella pagina **Account lettore dati**, nelle caselle **Account utente** e **Password** immettere il nome utente e la password dell'account utente da utilizzare per le query di SQL Reporting Services sul data warehouse. Selezionare il dominio dell'account nell'elenco a discesa **Dominio** e fare clic su **Avanti**.

12. Nella pagina **Rapporti dati operativi** fare clic su **Avanti**.

13. Nella pagina **Microsoft Update**fare clic su **Avanti**.

14. Nella pagina **Installazione del programma** fare clic su **Avanti**.

15. Nella pagina **Completamento dell'installazione guidata componenti di report di Operations Manager** fare clic su **Fine**.

16. In Installazione di System Center Operations Manager 2007 R2 fare clic su **Esci**.

Dopo avere installato la funzionalità di report di System Center, è possibile utilizzare la procedura riportata di seguito per reimpostare il nome del gruppo di sicurezza associato alla creazione di report di SQL Server. Anche in questo caso, questa procedura è necessaria solo se si utilizza SQL Server:

1.  Fare clic su **Start**, scegliere **Strumenti di amministrazione**, quindi **Server Manager**.

2.  In Server Manager espandere **Configurazione** e **Utenti e gruppi locali**, quindi fare clic su **Gruppi**.

3.  Individuare il gruppo seguente, in cui atl-sc-001 rappresenta il nome del computer e ARCHINST rappresenta l'istanza di SQL Server per i database di archiviazione e monitoraggio: **SQLServerReportServerUser$atl-sc-001$MSRS10\_50.ARCHINST**.

4.  Fare clic con il pulsante destro del mouse sul gruppo e scegliere **Rinomina**. Rinominare il gruppo aggiungendo **\_50** alla fine del nome del gruppo, appena prima del nome dell'istanza di SQL Server, ad esempio: **SQLServerReportServerUser$atl-sc-001$MSRS10\_50.ARCHINST**.

5.  Chiudere Server Manager.

Se la Console operatore di System Center è aperta, è necessario chiudere l'applicazione e riavviarla, altrimenti la scheda **Report** non comparirà nell'interfaccia utente della Console operatore. Tenere presente che, dopo il primo riavvio della Console operatore, è possibile che siano necessari alcuni minuti perché vengano visualizzati tutti i report di monitoraggio nella scheda **Report**.

