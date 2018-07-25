---
title: Distribuzione di una porta e di un alias non standard di SQL Server in Lync Server 2013
TOCTitle: Distribuzione di una porta e di un alias non standard di SQL Server in Lync Server 2013
ms:assetid: 2da92c1f-250e-407a-8651-fb2aec76aeb0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn776290(v=OCS.15)
ms:contentKeyID: 62633759
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuzione di una porta e di un alias non standard di SQL Server in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-01-06_

Microsoft Lync Server 2013 supporta l'utilizzo di un alias e di una porta non standard in SQL Server. L'utilizzo di un alias e di una porta non standard di SQL Server garantisce una maggiore sicurezza e una maggiore flessibilità nell'ambito della distribuzione Lync. Questo è uno dei passaggi per garantire la protezione dell'ambiente Lync Server 2013. Per ridurre la vulnerabilità di un'implementazione Lync Server 2013 sono però necessari altri passaggi.

Nell'articolo seguente vengono descritti i passaggi necessari per configurare un alias e una porta non standard di SQL Server in Lync Server 2013.

## Distribuzione di un alias e di una porta non standard di SQL Server in Lync Server 2013

Lync Server 2013Generatore di topologie supporta l'utilizzo di un alias SQL Server come FQDN (fully qualified domain name, nome di dominio completo) al posto dell'FQDN effettivo di SQL Server durante la configurazione di Lync Server 2013. In tal modo l'FQDN effettivo di SQL Server rimane nascosto e non soggetto a eventuali attacchi. Inoltre, l'utilizzo di una porta non standard tutela la porta effettiva da potenziali attacchi al database nella porta standard 1433, come visualizzato nell'immagine di seguito.

![Un pirata informatico non conosce il numero di porta da attaccare.](images/Dn776290.2f3923e0-2bdc-416b-a66b-bf56599eb14e(OCS.15).jpg "Un pirata informatico non conosce il numero di porta da attaccare.")

Per individuare correttamente la porta utilizzata da Lync Server 2013 per comunicare con SQL Server, l'autore dell'attacco deve esaminare tutte le porte e ottenere le relative informazioni. L'analisi delle porte aumenta le possibilità che l'istruzione venga rilevata e interrotta. Oltre a incrementare la sicurezza con una porta non standard, è possibile utilizzare un alias di SQL Server per una maggiore flessibilità della distribuzione. Questa soluzione è particolarmente utile per ridurre le modifiche della configurazione nei casi in cui è necessaria la modifica di un nome SQL Server.


> [!NOTE]
> SQL Server prevede due metodi di tolleranza di errore (clustering di failover e mirroring). Tutti e tre i metodi di tolleranza di errore di SQL Server sono supportati utilizzando un alias e una porta non standard di SQL Server con Lync Server 2013.



Durante la configurazione della connettività del database di SQL Server all'interno di Generatore di topologie o durante l'utilizzo del cmdlet Install-CsDatabase non è possibile definire esplicitamente un numero di porta non standard di SQL Server e associarlo a un'istanza SQL. Per impostare una porta non standard, è necessario utilizzare le utilità SQL Server e Windows Server.

Per configurare un alias e una porta non standard di SQL Server da utilizzare con Lync Server 2013, è necessario eseguire questi tre passaggi fondamentali:

  - Confermare che in Lync Server 2013 siano stati applicati gli ultimi aggiornamenti.

  - Configurare l'alias e la porta non standard di SQL Server.

  - Configurare Lync Server 2013 con l'alias di SQL Server utilizzando Generatore di topologie.

  - Pubblicare la topologia e verificare il database.

## Confermare che in Lync Server 2013 siano stati applicati gli ultimi aggiornamenti

È importante che Lync Server 2013 sia sempre aggiornato. Per ottenere informazioni sugli ultimi aggiornamenti o su come applicarli, vedere [Aggiornamenti per Lync Server 2013](http://support.microsoft.com/kb/2809243).

## Configurare l'alias e la porta non standard di SQL Server

Prima che Lync Server 2013Generatore di topologie possa farvi riferimento, l'alias e la porta non standard di SQL Server devono essere configurati nell'istanza del database. Per configurare un alias e una porta non standard di SQL Server, è necessario eseguire questi tre passaggi fondamentali:

  - Modificare i valori predefiniti del protocollo TCP/IP.

  - Creare e configurare un alias di SQL Server.

  - Creare un record di risorse CNAME DNS.

**Modificare i valori predefiniti del protocollo TCP/IP**

1.  Selezionare **Start** e scegliere **Gestione configurazione SQL Server** , come illustrato nell'immagine di seguito.
    
    ![Icona di SQL Server Management Studio](images/Dn776290.6e811f27-cea9-4437-b44c-55bff013150f(OCS.15).png "Icona di SQL Server Management Studio")

2.  Nel riquadro di navigazione fare clic per espandere **l'istanza di SQL Server**, fare clic per espandere **Configurazione di rete SQL Server** e selezionare **Protocolli per \<nome istanza\>**, come visualizzato nell'immagine seguente.
    
    ![Passare alle proprietà TCP/IP](images/Dn776290.3d7a964c-f17e-47fd-8f0c-535453da7fad(OCS.15).jpg "Passare alle proprietà TCP/IP")

3.  Nel riquadro destro fare clic con il pulsante destro del mouse su **TCP/IP** e scegliere **Proprietà**. Verrà visualizzata la finestra di dialogo delle proprietà TCP/IP.

4.  Selezionare la scheda **Indirizzi IP**. La scheda Indirizzi IP visualizza tutti gli indirizzi IP attivi sul server. Questi indirizzi sono in formato IP1, IP2, fino ad arrivare a IPAll, come mostra l'immagine.
    
    ![Aprire le proprietà TCP/IP.](images/Dn776290.ed2fd70d-1836-4ebf-80fe-09191d96585e(OCS.15).jpg "Aprire le proprietà TCP/IP.")

5.  Cancellare il contenuto del campo **Porte dinamiche TCP** per tutti gli indirizzi IP. Se nel campo è presente il valore zero, vuol dire che SQL Server sta creando un'istanza di attesa sulle porte dinamiche. Verificare che questi campi siano vuoti e che non contengano il valore zero.

6.  Per l'indirizzo IP che verrà utilizzato da Lync Server per la connessione al database, verificare che il campo **Abilitato** sia impostato su **Sì**, come visualizza l'immagine.
    
    ![Impostare Abilitato su Sì per l'indirizzo IP corretto.](images/Dn776290.7f818b91-0793-4594-8932-90447270fad9(OCS.15).jpg "Impostare Abilitato su Sì per l'indirizzo IP corretto.")

7.  Nella sezione **IPAll** in fondo alla finestra di dialogo immettere la porta desiderata nel campo **Porta TCP**, come illustra l'immagine. In questo esempio viene utilizzata la porta 50062, ma è possibile utilizzare qualsiasi numero di porta compreso tra 49152 e 65535. Utilizzando queste porte, per cui è previsto un utilizzo di tipo dinamico e privato, non si creeranno conflitti con altre porte utilizzate nella distribuzione di Lync Server 2013.
    
    ![Impostare la porta nella sezione IPAll.](images/Dn776290.b5af53e2-7961-4664-b586-3ca8f3a17f06(OCS.15).jpg "Impostare la porta nella sezione IPAll.")

8.  Scegliere **OK** per chiudere la finestra di dialogo delle proprietà TCP/IP.

9.  Riavviare l'istanza di SQL Server selezionando **Servizi di SQL Server** nel riquadro sinistro di Gestione configurazione SQL Server. Quindi fare clic con il pulsante destro del mouse su **SQL Server \<nome istanza\>** nel riquadro destro e selezionare **Riavvia**, come suggerisce l'immagine.
    
    ![Reimpostare il servizio SQL Server per l'istanza.](images/Dn776290.a965c8cf-f769-4b52-bb38-c48a438cf491(OCS.15).jpg "Reimpostare il servizio SQL Server per l'istanza.")

> [!important]  
> Assicurarsi di aggiornare le impostazioni firewall in funzione della nuova porta di SQL Server.

**Creare e configurare un alias di SQL Server**

1.  Selezionare **Start** e scegliere **Gestione configurazione SQL Server**, come illustrato nell'immagine di seguito.
    
    ![Icona di SQL Server Management Studio](images/Dn776290.6e811f27-cea9-4437-b44c-55bff013150f(OCS.15).png "Icona di SQL Server Management Studio")

2.  Nel riquadro sinistro fare clic per espandere **l'istanza di SQL Server**, fare clic per espandere **Configurazione SQL Native Client \<versione\>**, quindi selezionare **Alias**, come mostrato nell'immagine.
    
    ![Alias in Gestione configurazione SQL Server.](images/Dn776290.95341826-55d7-425f-ae19-d47d6668c5d8(OCS.15).jpg "Alias in Gestione configurazione SQL Server.")

3.  Fare clic con il pulsante destro del mouse su **Alias** e quindi scegliere **Nuovo alias…**.

4.  Immettere **Nome alias**, **Numero di porta**, **Protocollo** e **Server**, come mostrato di seguito.
    
    ![Creazione di un nuovo alias](images/Dn776290.03653588-aecf-4fdd-b58a-95f5b372d478(OCS.15).jpg "Creazione di un nuovo alias")
    
    > [!Caution]  
    > Assicurarsi di inserire la stessa porta non standard utilizzata nel passaggio precedente. SQL Server utilizzerà infatti questa porta per creare un'istanza di attesa. Se un alias configurato si connette a un FQDN errato o a un'istanza errata di SQL Server, disabilitare e riabilitare il protocollo di rete associato. In questo modo verranno cancellate tutte le informazioni di connessione memorizzate nella cache e il client potrà connettersi correttamente.

**Creare un record di risorse CNAME DNS**

1.  Accedere al computer che gestisce DNS.

2.  Selezionare **Start** e scegliere **Server Manager**, come illustrato nell'immagine di seguito.
    
    ![Apertura di Server Manager](images/Dn776290.3e4bd8ad-2a65-4a05-af40-c8dd3583bc8f(OCS.15).jpg "Apertura di Server Manager")

3.  Selezionare il menu a discesa **Strumenti**, quindi **DNS**, come mostrato.
    
    ![Apertura di DNS da Server Manager.](images/Dn776290.415e1da1-7c9a-4a4e-a896-ca34a76aaeff(OCS.15).jpg "Apertura di DNS da Server Manager.")

4.  Nel riquadro sinistro espandere il nodo del nome server, espandere il nodo Zone di ricerca diretta e scegliere il relativo dominio.

5.  Fare clic con il pulsante destro del mouse sul dominio, quindi selezionare **Nuovo alias (CNAME)…**, come visualizzato di seguito.
    
    ![Selezione dell'opzione per creare un nuovo alias CNAME](images/Dn776290.abe66cca-b53c-427a-9094-1a59dc6840ca(OCS.15).jpg "Selezione dell'opzione per creare un nuovo alias CNAME")

6.  Inserire il **Nome alias** e l'**FQDN per SQL Server**, come dimostra la figura.
    
    ![Compilazione della finestra di dialogo del nuovo alias CNAME.](images/Dn776290.dd0ebd2d-3407-4459-8bd9-2b389a7bc440(OCS.15).jpg "Compilazione della finestra di dialogo del nuovo alias CNAME.")

7.  Scegliere **OK** per salvare il CNAME e visualizzarlo in Gestore DNS.

## Verificare la connettività del database

Esistono diversi modi per verificare il funzionamento della connettività. Per assicurarsi che il database di SQL Server crei un'istanza di attesa sulla porta specificata con l'alias, è possibile procedere rapidamente con i comandi **netstat** e **telnet**.


> [!NOTE]
> Telnet Client è una funzionalità da installare inclusa in Windows Server. Per installare una funzionalità di Windows Server è necessario aprire Server Manager e selezionare Aggiungi ruoli e funzionalità nel menu di gestione.



**Utilizzare netstat e telnet per verificare la connettività del database**

1.  Selezionare **Start** e digitare **cmd** per aprire un prompt dei comandi.

2.  Digitare **netstat -a -f** e confermare che SQL Server viene eseguito con la porta corretta, come mostra l'immagine.
    
    ![Utilizzo di netstat per il controllo della porta.](images/Dn776290.4ff3a1b2-c5eb-4496-8be7-374c351fa027(OCS.15).jpg "Utilizzo di netstat per il controllo della porta.")

3.  Digitare **telnet \<nome alias\> \<numero di porta\>** per confermare la connessione all'istanza di SQL Server. Se la connessione va a buon fine, telnet si connetterà e non verranno visualizzati errori. Questo vuol dire che l'istanza di SQL Server sta creando un'istanza di attesa sulla porta corretta e con l'alias corretto. Se si verificano problemi di connessione al database di SQL Server, telnet visualizzerà un errore per segnalare che non è possibile stabilire la connessione. Dopo aver verificato la connettività del database sul server del database, è possibile ripetere l'operazione da Lync Server (in rete) per verificare che l'accesso non sia bloccato da nessun server.

## Conclusione

Al termine della configurazione dell'alias di SQL Server, è possibile utilizzarlo per creare una topologia Lync Server 2013 nello strumento Generatore di topologie. Per ulteriori informazioni sulle topologie, vedere [Definizione e configurazione della topologia in Lync Server 2013](lync-server-2013-defining-and-configuring-the-topology.md).

## Vedere anche

#### Concetti

[Microsoft Lync Server 2013](microsoft-lync-server-2013.md)  

#### Ulteriori risorse

[Pianificazione della sicurezza in Lync Server 2013](lync-server-2013-planning-for-security.md)  
[Definizione e configurazione della topologia in Lync Server 2013](lync-server-2013-defining-and-configuring-the-topology.md)  
[Distribuzione di Lync Server 2013](lync-server-2013-deploying-lync-server.md)

