---
title: Associazione delle relazioni di monitoraggio a un database mirror
TOCTitle: Associazione delle relazioni di monitoraggio a un database mirror
ms:assetid: 42b797c6-8db8-4ad7-886e-8ddf8deb06f9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945624(v=OCS.15)
ms:contentKeyID: 52062138
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Associazione delle relazioni di monitoraggio a un database mirror

 

_**Ultima modifica dell'argomento:** 2014-02-07_

Se si configura un database mirror per il database di monitoraggio, tale database mirror diventerà il database primario in caso di failover. Tuttavia, se si usano le relazioni di monitoraggio di Lync Server e si verifica un failover, è possibile che tali relazioni non si connettano al database mirror. Ciò accade perché durante l'installazione delle relazioni di monitoraggio viene specificata solamente la posizione del database primario e non quella del database mirror.

Per far sì che le relazioni di monitoraggio eseguano automaticamente il failover sul database mirror, è necessario aggiungere il database mirror come "partner di failover" ai due database utilizzati dalle relazioni di monitoraggio (un database per i dati di registrazione dettagli chiamata e un database per i dati QoE). È possibile aggiungere le informazioni sul partner di failover modificando manualmente i valori della stringa di connessione utilizzati dai due database. A tale scopo, eseguire la procedura seguente:

1.  Utilizzare Internet Explorer per aprire la home page di **SQL Server Reporting Services**. L'URL della pagina iniziale di Reporting Services include:
    
      - Il prefisso **http:**.
    
      - Il nome di dominio completo (FQDN) del computer in cui è installato Reporting Services, ad esempio **atl-sql-001.litwareinc.com**.
    
      - La stringa di caratteri **/Reports\_**.
    
      - Il nome dell'istanza di database in cui sono installate le relazioni di monitoraggio, ad esempio **archinst**.
    
    Se ad esempio SQL Server Reporting Services è stato installato nel computer atl-sql-001.litwareinc.com e le relazioni di monitoraggio utilizzano l'istanza di database archinst, l'URL dell'home page sarà il seguente:
    
    **http://atl-sql-001.litwareinc.com/Reports\_archinst**

2.  Dopo aver eseguito l'accesso all'home page di Reporting Services, fare clic su **LyncServerReports** e quindi su **Reports\_Content**. In questo modo si verrà reindirizzati alla pagina **Reports\_Content** per le relazioni di monitoraggio di Lync Server.

3.  Nella pagina **Reports\_Content** fare clic sull'origine dati **CDRDB**.

4.  Nella scheda **Proprietà** della pagina **CDRDB** cercare la casella di testo **Stringa di connessione**. La stringa di connessione corrente avrà un aspetto simile al seguente:
    
    **Data source=(local)\\archinst;initial catalog=LcsCDR**

5.  Modificare la stringa di connessione per includere il nome del server e l'istanza del database per il database mirror. Se ad esempio il nome del server è atl-mirror-001 e il nome del database mirror si trova nell'istanza archinst, sarà necessario apportare un'aggiunta per specificare il database mirror utilizzando questa sintassi:
    
    **Failover Partner=atl-mirror-001\\archinst**
    
    La stringa di connessione modificata sarà simile alla seguente:
    
    **Data source=(local)\\archinst;Failover Partner=atl-mirror-001\\archinst;initial catalog=LcsCDR**

6.  Dopo aver aggiornato la stringa di connessione, fare clic su **Applica**.

7.  Nella pagina **CDRDB** fare clic sul collegamento **Reports\_Content**. Fare clic sull'origine dati **QMSDB** e quindi modificare la stringa di connessione per il database QoE. Ad esempio:
    
    **Data source=(local)\\archinst;Failover Partner=atl-mirror-001\\archinst;initial catalog=QoEMetrics**

8.  Fare clic su **Applica**.

## Vedere anche

#### Concetti

[Installazione dei rapporti di monitoraggio di Lync Server 2013](lync-server-2013-installing-lync-server-2013-monitoring-reports.md)  
[Utilizzo dei rapporti di monitoraggio in Lync Server 2013](lync-server-2013-using-monitoring-reports.md)

