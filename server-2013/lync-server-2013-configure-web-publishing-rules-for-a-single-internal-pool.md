---
title: 'Lync Server 2013: Configurare le regole di pubblicazione Web per un singolo pool interno'
TOCTitle: Configurare le regole di pubblicazione Web per un singolo pool interno
ms:assetid: 86ff4b2a-1ba9-46a2-a175-8b19e00a49dd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429712(v=OCS.15)
ms:contentKeyID: 49301228
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare le regole di pubblicazione Web per un singolo pool interno in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-07-07_

In Microsoft Forefront Threat Management Gateway 2010 e in Application Request Routing di Internet Information Server (IIS ARR) vengono utilizzate le regole di pubblicazione Web per pubblicare risorse interne, ad esempio l'URL di una riunione, per gli utenti in Internet.

Oltre agli URL dei servizi Web per le directory virtuali, è anche necessario creare regole di pubblicazione per gli URL semplici, l'URL di LyncDiscover e il Server Office Web Apps. Per ogni URL semplice, è necessario creare una singola regola nel proxy inverso che punti a tale URL semplice.

Se si sta eseguendo la distribuzione per dispositivi mobili e si utilizza l'individuazione automatica, è necessario creare una regola di pubblicazione per l'URL esterno del servizio di individuazione automatica. Il servizio di individuazione automatica richiede anche regole di pubblicazione per l'URL esterno dei Servizi Web Lync Server per il pool di server Director e il pool Front End. Per informazioni dettagliate sulla creazione di regole di pubblicazione Web per l'individuazione automatica, vedere [Configurazione del proxy inverso per i dispositivi mobili in Lync Server 2013](lync-server-2013-configuring-the-reverse-proxy-for-mobility.md).

Per creare regole di pubblicazione Web, eseguire le procedure seguenti.


> [!NOTE]
> Per queste procedure si presuppone che sia stata installata la versione Standard Edition di Forefront Threat Management Gateway (TMG) 2010 o che sia stato installato e configurato Internet Information Server con l'estensione Application Request Routing (IIS ARR). È possibile utilizzare TMG o IIS ARR.



## Per creare una regola di pubblicazione del server Web nel computer che esegue TMG 2010

1.  Fare clic sul pulsante **Start** , selezionare **Programmi** , **Microsoft Forefront TMG** e quindi fare clic su **Gestione Forefront TMG** .

2.  Nel riquadro sinistro espandere **NomeServer** , fare clic con il pulsante destro del mouse su **Criterio firewall** , selezionare **Nuovo** e quindi fare clic su **Regola di pubblicazione sito Web** .

3.  Nella pagina **Nuova regola di pubblicazione Web** digitare un nome visualizzato per la regola di pubblicazione, ad esempio RegolaDownloadWebLyncServer.

4.  Nella pagina **Seleziona azione regola** selezionare **Consenti** .

5.  Nella pagina **Tipo di pubblicazione** selezionare **Pubblica un singolo sito Web o un sistema di bilanciamento del carico** .

6.  Nella pagina **Protezione connessione server** selezionare **Utilizzare SSL per connettersi al server Web pubblicato o alla server farm** .

7.  Nella pagina **Dettagli pubblicazione interna** digitare il nome di dominio completo (FQDN) della Web farm interna che ospita il contenuto delle riunioni e della Rubrica nella casella **Nome sito interno** .
    

    > [!NOTE]
    > Se il server interno è un server Standard Edition, il nome di dominio completo corrisponde al nome di dominio completo del server Standard Edition. Se il server interno è un pool Front End, il nome di dominio completo corrisponde a un indirizzo VIP (Virtual IP) del servizio di bilanciamento del carico hardware che si occupa del bilanciamento del carico dei server interni della Web farm. Il server TMG deve essere in grado di risolvere il nome di dominio completo nell'indirizzo IP del server Web interno. Se il server TMG non è in grado di risolvere il nome di dominio completo nell'indirizzo IP corretto, è possibile selezionare <STRONG>Utilizza nome computer o indirizzo IP per la connessione al server pubblicato</STRONG> e quindi nella casella <STRONG>Indirizzo IP o</STRONG> <STRONG>nome computer</STRONG> digitare l'indirizzo IP del server Web interno. In tal caso, è necessario verificare che la porta 53 sia aperta nel server TMG e che sia possibile raggiungere un server DNS che si trova nella rete perimetrale. È anche possibile utilizzare le voci nell'host locale per la risoluzione dei nomi.



8.  Nella casella **Percorso (facoltativo)** della pagina **Dettagli pubblicazione interna** digitare **/\*** come percorso della cartella da pubblicare.
    

    > [!NOTE]
    > Nella procedura guidata di pubblicazione del sito Web è possibile specificare solo un percorso. Per aggiungere altri percorsi, è necessario modificare le proprietà della regola.



9.  Nella pagina **Dettagli nome pubblico** verificare che sia selezionata l'opzione **Nome dominio** in **Accetta richieste per** e digitare il nome di dominio completo esterno dei Servizi Web nella casella **Nome pubblico** .

10. Nella pagina **Scegliere Listener Web** fare clic su **Nuovo** per aprire la Creazione guidata definizione listener Web.

11. Nella pagina **Creazione guidata listener Web** digitare un nome per il listener Web nella casella **Nome listener Web** , ad esempio ServerWebLyncServer.

12. Nella pagina **Protezione di connessione client** selezionare **Richiedi connessioni SSL protette con i client** .

13. Nella pagina **Indirizzi IP del listener Web** selezionare **Esterno** e quindi fare clic su **Seleziona indirizzi IP** .

14. Nella pagina **Selezione IP listener esterno** selezionare **Indirizzo IP specificato nel computer Forefront TMG nella rete selezionata** , selezionare l'indirizzo IP appropriato e fare clic su **Aggiungi** .

15. Nella pagina **Certificati SSL listener** selezionare **Assegna un certificato a ciascun indirizzo IP** , selezionare l'indirizzo IP associato al nome FQDN Web esterno e quindi fare clic su **Seleziona certificato** .

16. Nella pagina **Seleziona certificato** selezionare il certificato corrispondente ai nomi pubblici specificati al passaggio 9 e fare clic su **Seleziona** .

17. Nella pagina **Impostazione di autenticazione** selezionare **Nessuna autenticazione** .

18. Nella pagina **Impostazioni Single Sign-On** fare clic su **Avanti** .

19. Nella pagina **Completamento della Creazione guidata listener Web** verificare che le impostazioni specificate in **Listener Web** siano corrette e quindi fare clic su **Fine** .

20. Nella pagina **Delega autenticazione** selezionare **Nessuna delega, ma il client può eseguire l'autenticazione direttamente** .

21. Nella pagina **Gruppo di utenti** fare clic su **Avanti** .

22. Nella pagina **Completamento della Creazione guidata regola di pubblicazione Web** verificare che le impostazioni della regola di pubblicazione Web siano corrette e quindi fare clic su **Fine** .

23. Nel riquadro dei dettagli fare clic su **Applica** per salvare le modifiche e aggiornare la configurazione.

## Per creare una regola di pubblicazione del server Web nel computer che esegue IIS ARR

1.  Associare al protocollo HTTPS il certificato che verrà utilizzato per il proxy inverso. Fare clic sul pulsante **Start** , scegliere **Programmi** , **Strumenti di amministrazione** e quindi **Internet Information Services (IIS) Manager** .
    

    > [!NOTE]
    > Per ulteriori informazioni, schermate e istruzioni sulla distribuzione e la configurazione di IIS ARR vedere l'articolo relativo all' <A href="http://go.microsoft.com/fwlink/?linkid=293391">uso di IIS ARR come proxy inverso per Lync Server 2013</A> su NextHop.



2.  Se non è già stato fatto, importare il certificato che verrà utilizzato per il proxy inverso. In **Internet Information Services (IIS) Manager** fare clic sul nome del server proxy inverso nella parte sinistra della console. Nella parte centrale della console sotto **IIS** individuare **Server Certificates** . Fare clic con il pulsante destro del mouse su **Server Certificates** e quindi scegliere **Open feature** .

3.  Nella parte destra della console fare clic su **Import** . Digitare il percorso e il nome file del certificato con l'estensione oppure fare clic su **…** per cercare il certificato. Selezionare il certificato e fare clic su **Open** . Digitare la password utilizzata per proteggere la chiave privata (se ne è stata assegnata una durante l'esportazione del certificato e della chiave privata). Fare clic su **OK** . Se l'importazione riesce, il certificato sarà visualizzato nella parte centrale della console nell'elenco **Server Certificates** .

4.  Assegnare il certificato che verrà utilizzato da HTTPS. Nella parte sinistra della console selezionare l'impostazione **Default Web Site** per il server IIS. Nella parte destra fare clic su **Bindings** . Nella finestra di dialogo **Site Bindings** fare clic su **Add** . Nella finestra di dialogo **Add Site Binding** selezionare **https** in **Type** . Questa opzione consentirà di selezionare il certificato da utilizzare per https. In **SSL certificate** selezionare il certificato importato per il proxy inverso. Fare clic su **OK** . Fare quindi clic su **Chiudi** . Il certificato è ora associato al proxy inverso per SSL (Secure Socket Layer) e TLS (Transport Layer Security).
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Se quando si chiude la finestra di dialogo Bindings viene visualizzato un avviso per informare che mancano i certificati intermedi, è necessario individuare e importare il certificato autorità radice dell'autorità di certificazione pubblica ed eventuali certificati intermedi dell'autorità di certificazione. Fare riferimento alle istruzioni disponibili presso l'autorità di certificazione pubblica a cui è stato richiesto il certificato e attenersi a quelle relative alla richiesta e all'importazione di una catena di certificati. Se il certificato è stato importato dal server perimetrale, è possibile esportare il certificato dell'autorità di certificazione radice ed eventuali certificati intermedi dell'autorità di certificazione associati al server perimetrale. Importare il certificato radice dell'autorità di certificazione nell'archivio Autorità di certificazione radice disponibile nell'elenco locale del computer (da non confondere con l'archivio utenti) e i certificati intermedi nell'archivio Autorità di certificazione intermedie del computer.</td>
    </tr>
    </tbody>
    </table>


5.  Nella parte sinistra della console sotto il nome del server IIS, fare clic con il pulsante destro del mouse su **Server Farms** e quindi fare clic su **Create Server Farm** .
    

    > [!NOTE]
    > Se il nodo <STRONG>Server Farms</STRONG> non è visualizzato, è necessario installare Application Request Routing. Per informazioni dettagliate, vedere <A href="lync-server-2013-setting-up-reverse-proxy-servers.md">Configurare server proxy inversi per Lync Server 2013</A>.

    
    Nella finestra di dialogo **Crea Server Farm** digitare in **Server farm name** un nome per il primo URL. Per facilitare l'identificazione tale nome può essere descrittivo. Fare clic su **Next** .

6.  Nella finestra di dialogo **Add Server** digitare in **Server Address** il nome di dominio completo (FQDN) dei servizi Web esterni in Front End Server. I nomi utilizzati in questo articolo a titolo esemplificativo sono gli stessi che vengono utilizzati nella sezione [Riepilogo dei certificati - proxy inverso in Lync Server 2013](lync-server-2013-certificate-summary-reverse-proxy.md) relativa alla pianificazione per il proxy inverso. Facendo riferimento alla pianificazione del proxy inverso digitare il nome di dominio completo `webext.contoso.com`. Verificare che la casella di controllo accanto a **Online** sia selezionata. Fare clic su **Add** per aggiungere il server al pool di server Web per questa configurazione.
    

    > [!WARNING]
    > Lync Server utilizza servizi di bilanciamento del carico hardware per definire il pool del Server Director e dei Front End Server per il traffico HTTP e HTTPS. Quando si aggiunge un server alla server farm IIS ARR, è necessario specificare un solo nome di dominio completo. Tale nome corrisponderà a Front End Server o a Server Director nelle configurazioni server non in pool oppure al nome di dominio completo del servizio di bilanciamento del carico hardware configurato per i pool di server. L'unico metodo supportato per bilanciare il carico del traffico HTTP e HTTPS consiste nell'utilizzare servizi di bilanciamento del traffico hardware.



7.  Nella finestra di dialogo **Add Server** fare clic su **Advanced settings** . Verrà aperta una finestra di dialogo in cui definire Application Request Routing per le richieste al nome di dominio completo configurato. Lo scopo è di ridefinire la porta utilizzata quando la richiesta viene elaborata da IIS ARR.
    
    Per impostazione predefinita, la porta HTTP di destinazione deve essere impostata su 8080. Fare clic accanto al valore **httpPort 80** corrente e impostarlo su **8080** . Fare clic accanto al valore **httpsPort 443** corrente e impostarlo su **4443** . Lasciare impostato su 100 il parametro **weight** . Se necessario, è possibile ridefinire i pesi per una data regola una volta disponibili le statistiche iniziali. Fare clic su **Finish** per completare questa parte della configurazione delle regole.

8.  È possibile che venga visualizzata una finestra di dialogo in cui si informa che IIS Manager è in grado di creare una regola di URL Rewrite per instradare automaticamente tutte le richieste in arrivo alla server farm. Fare clic su **Yes** . In questo modo verrà impostata la configurazione iniziale delle regole che potranno essere modificate manualmente.

9.  Fare clic sul nome della server farm appena creata. In **Server Farm** in Features View di IIS Manager fare doppio clic su **Caching** . Deselezionare **Enable disk cache** . Fare clic su **Apply** nella parte destra.

10. Fare clic sul nome della server farm. In **Server farm** in Visualizzazione funzionalità di Gestione IIS fare doppio clic su **Proxy**. Nella pagina delle impostazioni del proxy modificare il valore di **Timeout (secondi)** e impostare un valore appropriato per la distribuzione. Fare clic su **Applica** per salvare la modifica.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Il valore di timeout del proxy è un numero che varia a seconda della distribuzione. È consigliabile monitorare la distribuzione e modificare il valore in modo da offrire un'esperienza ottimale ai client. Si potrebbe riuscire a impostare un valore basso come 200. Se si supportano client mobili Lync nel'ambiente, il valore deve essere impostato su 960 per consentire il timeout delle notifiche push da Office 365 per le quali è impostato il valore di timeout 900. È molto probabile che sia necessario incrementarlo per evitare la disconnessione dei client quando il valore è troppo basso oppure ridurlo se le connessioni tramite il proxy non vengono disconnesse e chiuse molto tempo dopo la disconnessione del client. Il monitoraggio e la definizione dei valori di base normali per l'ambiente corrente costituiscono l'unico modo per determinare con precisione l'impostazione più adatta per questo valore.</td>
    </tr>
    </tbody>
    </table>


11. Fare clic sul nome della server farm. In **Server Farm** in Features View di IIS Manager fare doppio clic su **Routing Rules** . Nella finestra di dialogo Routing Rules deselezionare la casella di controllo accanto a Enable SSL offloading in Routing. Se non è possibile deselezionare la casella di controllo, selezionare la casella **Use URL Rewrite to inspect incoming requests** . Fare clic su **Apply** per salvare le modifiche.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ205186.Caution(OCS.15).gif" title="Caution" alt="Caution" />Attenzione:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>La ripartizione del carico di lavoro SSL tramite il proxy inverso non è supportata.</td>
    </tr>
    </tbody>
    </table>


12. Ripetere i passaggi da 5 a 11 per ogni URL che deve attraversare il proxy server. Un elenco comune è simile al seguente:
    
      - Servizi Web esterni del Front End Server: webext.contoso.com (già configurato nella procedura dettagliata iniziale)
    
      - Servizi Web esterni del Server Director per Server Director: webdirext.contoso.com (facoltativo se è distribuito un Server Director)
    
      - Meet URL semplici: meet.contoso.com
    
      - Dialin URL semplici: dialin.contoso.com
    
      - URL di individuazione automatica di Lync: lyncdiscover.contoso.com
    
      - URL di Office Web Apps Server: officewebapps01.contoso.com
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Per l'URL di Server Office Web Apps verrà utilizzato un indirizzo httpsPort diverso. Al passaggio 7 impostare <strong>httpsPort</strong> su <strong>443</strong> e <strong>httpPort</strong> su <strong>80</strong> . Tutte le altre impostazioni di configurazione rimangono invariate.</td>
        </tr>
        </tbody>
        </table>


13. Nella parte sinistra della console fare clic sul nome del server IIS. Nella parte centrale della console individuare **URL Rewrite** in **IIS** . Fare doppio clic su URL Rewrite per aprire la configurazione delle regole di URL Rewrite. Dovrebbero essere visualizzate le regole per ogni server farm creata nei passaggi precedenti. In caso contrario, verificare di aver fatto clic sul nome del **server IIS** immediatamente sotto il nodo **Start Page** della console di Internet Information Server Manager.

14. Nella finestra di dialogo **URL Rewrite** , utilizzando come esempio webext.contoso.com, il nome completo della regola visualizzata sarà **ARR\_webext.contoso.com\_loadbalance\_SSL** .
    
      - Fare doppio clic sulla regola per aprire la finestra di dialogo **Edit Inbound Rule** .
    
      - Fare clic su **Add** nella finestra di dialogo **Conditions** .
    
      - Nel campo **Condition input** di **Add Condition** digitare **{HTTP\_HOST}** . Mentre si digita viene visualizzata una finestra di dialogo che consente di selezionare la condizione. In **Check if input string** selezionare **Matches the Pattern** . In **Pattern input** digitare **\*** . **Ignore case** deve essere selezionato. Fare clic su **OK** .
    
      - Scorrere verso il basso nella finestra di dialogo **Edit Inbound Rule** per individuare la finestra di dialogo **Action** . **Action Type** deve essere impostato su **Route to Server Farm** , **Scheme** su **https://** , **Server farm** sull'URL al quale applicare la regola. Per questo esempio deve essere impostato su **webext.contoso.com** . **Path** viene impostato su **/{R:0}**
    
      - Fare clic su **Apply** per salvare le modifiche. Fare clic su **Back to Rules** per tornare alle regole di URL Rewrite.

15. Ripetere la procedura definita al passaggio 14 per ogni regola di SSL Rewrite definita, una per ogni URL di server farm.
    

    > [!WARNING]
    > Per impostazione predefinita, vengono create anche regole HTTP, contraddistinte da nomi simili a quelli delle regole SSL. Per l'esempio corrente il nome della regola HTTP è <STRONG>ARR_webext.contoso.com_loadbalance</STRONG> . Queste regole non richiedono alcuna modifica e possono essere ignorate.



## Per modificare le proprietà della regola di pubblicazione Web in TMG 2010

1.  Fare clic sul pulsante **Start** , selezionare **Programmi** , **Microsoft Forefront TMG** e quindi fare clic su **Gestione Forefront TMG** .

2.  Nel riquadro sinistro espandere **NomeServer** e quindi fare clic su **Criterio firewall** .

3.  Nel riquadro dei dettagli fare clic con il pulsante destro del mouse sulla regola di pubblicazione server Web creata nella procedura precedente, ad esempio RegolaEsternaLyncServer e quindi scegliere **Proprietà** .

4.  Nella scheda **Da** della pagina **Proprietà** eseguire le operazioni seguenti:
    
      - Nell'elenco **Questa regola si applica al traffico prodotto dalle seguenti origini** fare clic su **Ovunque** e quindi su **Rimuovi** .
    
      - Fare clic su **Aggiungi** .
    
      - In **Aggiungi entità di rete** espandere **Reti** , fare clic su **Esterno** , **Aggiungi** e quindi su **Chiudi** .

5.  Nella scheda **Per** verificare che la casella di controllo **Inoltra l'intestazione host originale e non quella effettiva** sia selezionata.

6.  Nella scheda **Bridging** selezionare la casella di controllo **Reindirizza richiesta a porta SSL** e quindi specificare la porta **4443** .

7.  Nella scheda **Nome pubblico** aggiungere gli URL semplici, ad esempio meet.contoso.com e dialin.contoso.com.

8.  Fare clic su **Applica** per salvare le modifiche e quindi su **OK** .

9.  Nel riquadro dei dettagli fare clic su **Applica** per salvare le modifiche e aggiornare la configurazione.

## Per modificare le proprietà della regola di pubblicazione Web in IIS ARR

1.  Fare clic sul pulsante **Start** , scegliere **Programmi** , **Strumenti di amministrazione** e quindi **Internet Information Services (IIS) Manager** .

2.  Nella parte sinistra della console fare clic sul nome del server IIS.

3.  Nella parte centrale della console individuare **URL Rewrite** in **IIS** . Fare doppio clic su URL Rewrite per aprire la configurazione delle regole di URL Rewrite.

4.  Fare doppio clic sulla regola da modificare. Apportare le modifiche necessarie in **Match URL** , **Conditions** , **Server Variables** o **Action** .

5.  Fare clic su **Apply** per eseguire il commit delle modifiche. Fare clic su **Back to Rules** per modificare altre regole oppure chiudere la console di **IIS Manager** se non sono necessarie altre modifiche.

