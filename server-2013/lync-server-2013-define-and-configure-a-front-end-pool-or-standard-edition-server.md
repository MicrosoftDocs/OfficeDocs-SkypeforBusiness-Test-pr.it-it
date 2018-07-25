---
title: 'Lync Server 2013: Definire e configurare un pool Front End o un server Standard Edition'
TOCTitle: Definire e configurare un pool Front End o un server Standard Edition
ms:assetid: 713fc263-23dd-414a-b001-82932e4fe966
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398538(v=OCS.15)
ms:contentKeyID: 49300942
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definire e configurare un pool Front End o un server Standard Edition in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per eseguire questa procedura non è richiesta l'appartenenza a un gruppo di amministratori locale o a un gruppo di dominio con privilegi. È consigliabile eseguire l'accesso a un computer come utenti standard.

Se si distribuisce un server Enterprise, è necessario che sia in esecuzione, contemporaneamente, un numero minimo di Front End Server in un pool. I requisiti di versione sono riassunti nella tabella seguente.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Numero totale di Front End Server nel pool</th>
<th>Numero minimo di server attivi per il funzionamento del pool</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1-2</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>3-4</p></td>
<td><p>2</p></td>
</tr>
<tr class="odd">
<td><p>5-6</p></td>
<td><p>3</p></td>
</tr>
<tr class="even">
<td><p>7-8</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p>9-10</p></td>
<td><p>5</p></td>
</tr>
<tr class="even">
<td><p>11-12</p></td>
<td><p>6</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> In Lync Server 2013, tutte le volte che si aggiungono o rimuovono Front End Server dal pool, è necessario riavviare i servizi. La rimozione e l'aggiunta di server devono essere eseguite come operazioni separate. Ad esempio, se si ha bisogno di aggiungere due Front End Server e rimuovere due Front End Server, seguire questa procedura: 
> <OL>
> 
> 
> 
> <li>
> <P>Rimuovere i due Front End Server</P>
> 
> 
> 
> <li>
> <P>Pubblicare e riattivare la topologia.</P>
> 
> 
> 
> <li>
> <P>Riavviare i servizi.</P>
> 
> 
> 
> <li>
> <P>Aggiungere i due Front End Server</P>
> 
> 
> 
> <li>
> <P>Pubblicare e riattivare la topologia.</P>
> 
> 
> 
> <li>
> <P>Riavviare i servizi.</P></LI></OL>



Dopo avere stabilito la topologia, utilizzare la procedura seguente per definire un pool Front End per il sito. Per informazioni dettagliate sulla definizione della topologia, vedere [Definire e configurare una topologia in Generatore di topologie per Lync Server 2013](lync-server-2013-define-and-configure-a-topology-in-topology-builder.md).

## Per definire un pool Front End

1.  Nella pagina **Definire il nuovo pool Front End** della procedura guidata Definisci nuovo pool Front End fare clic su **Avanti** .

2.  Nella pagina **Definire l'FQDN del pool Front End** immettere un nome di dominio completo (FQDN) per il pool che si sta creando, fare clic su **Pool Enterprise Edition Front End** e quindi su **Avanti**.

3.  Nella pagina **Definire i computer nel pool corrente** immettere l'FQDN di un computer per il primo Front End Server nel pool e quindi fare clic su **Aggiungi**. Ripetere questo passaggio per tutti gli altri computer (fino a dodici) da aggiungere al pool e quindi fare clic su **Avanti**.

4. Nella pagina **Selezionare funzionalità** selezionare le caselle di controllo corrispondenti alle caratteristiche desiderate per il pool Front End. Se si è scelto di distribuire solo le caratteristiche di messaggistica istantanea e presenza, ad esempio, è necessario selezionare la casella di controllo **Servizio di conferenza** per consentire la messaggistica istantanea con più partecipanti, ma non le caselle di controllo **Servizi di conferenza telefonica con accesso esterno (PSTN)**, **VoIP aziendale** e **Controllo di ammissione di chiamata** perché corrispondono a funzionalità vocali, video e di conferenza per la collaborazione.
    
      - **Servizio di conferenza :** questa opzione consente un ricco insieme di caratteristiche, tra le quali:
        
          - Messaggistica istantanea con più di due partecipanti in una sessione
        
          - Servizio di conferenza, che include la collaborazione sui documenti, la condivisione di applicazioni e la condivisione del desktop
        
          - A/V Conferencing, tramite cui gli utenti possono partecipare a conferenze audio/video in tempo reale senza che siano necessari servizi esterni come il servizio Live Meeting o un bridge audio di terze parti
    
      - **Servizi di conferenza telefonica con accesso esterno (PSTN) :** consente agli utenti di partecipare alla parte audio di una conferenza di Lync Server 2013 tramite un telefono PSTN senza dover utilizzare un provider di servizi di audioconferenza.
    
      - **VoIP aziendale :** soluzione Voice over IP (VoIP) inclusa in Lync Server 2013 che consente agli utenti di effettuare e ricevere chiamate telefoniche. È consigliabile distribuire questa caratteristica se si prevede di utilizzare Lync Server 2013 per le chiamate vocali, la segreteria telefonica e altre funzioni che utilizzano un dispositivo hardware o un client software.
    
      - **Controllo di ammissione di chiamata :** il servizio Controllo di ammissione di chiamata determina, in base alla larghezza di banda di rete disponibile, se consentire sessioni di comunicazione in tempo reale, ad esempio chiamate audio o video. Se sono state distribuite solo le caratteristiche di messaggistica istantanea e presenza, il servizio Controllo di ammissione di chiamata non è necessario, perché non viene utilizzato da queste due caratteristiche.
    
      - **Archiviazione**   La funzione di archiviazione consente di archiviare il contenuto di messaggistica istantanea, il contenuto delle conferenze (riunioni) o entrambi i contenuti inviati attraverso Lync Server 2013.
    
      - **Monitoraggio**   Server di monitoraggio consente di raccogliere dati numerici che descrivono la qualità multimediale nella rete e negli endpoint, informazioni di utilizzo relative alle chiamate VoIP (Voice over IP), messaggi istantanei, conversazioni audio/video (A/V), riunioni, la condivisione applicazioni e trasferimenti di file, nonché informazioni sugli errori relativi alle chiamate e la risoluzione dei problemi per le chiamate non riuscite.
    

    > [!NOTE]
    > Se si desidera abilitare il servizio Controllo di ammissione di chiamata nella distribuzione, è necessario abilitarlo esattamente in un pool per ogni sito centrale. È consigliabile abilitare questo servizio quando si distribuiscono caratteristiche vocali o conferenze audio/video.

    
    Nella tabella seguente vengono indicate le caratteristiche disponibili (in alto) e le funzioni offerte agli utenti (a sinistra). Le selezioni indicate nella tabella corrispondono alle opzioni che è necessario selezionare per abilitare queste caratteristiche per l'organizzazione.
    
    
    <table>
    <colgroup>
    <col style="width: 20%" />
    <col style="width: 20%" />
    <col style="width: 20%" />
    <col style="width: 20%" />
    <col style="width: 20%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th></th>
    <th>Servizi di conferenza</th>
    <th>Conferenze telefoniche con accesso esterno</th>
    <th>VoIP aziendale</th>
    <th>Controllo di ammissione di chiamata</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Presenza e messaggistica istantanea</p></td>
    <td><p>X</p></td>
    <td><p></p></td>
    <td><p></p></td>
    <td><p></p></td>
    </tr>
    <tr class="even">
    <td><p>Servizi di conferenza</p></td>
    <td><p>X</p></td>
    <td><p>X</p></td>
    <td><p></p></td>
    <td><p></p></td>
    </tr>
    <tr class="odd">
    <td><p>Conferenze audio/video</p></td>
    <td><p>X</p></td>
    <td><p>X</p></td>
    <td><p></p></td>
    <td><p>X</p></td>
    </tr>
    <tr class="even">
    <td><p>VoIP aziendale</p></td>
    <td><p></p></td>
    <td><p></p></td>
    <td><p>X</p></td>
    <td><p>X</p></td>
    </tr>
    </tbody>
    </table>


5.  Nella pagina **Selezionare ruoli server collocati** è possibile collocare Mediation Server nel Front End Server o distribuirlo come server autonomo.
    
    È possibile distribuire Mediation Server nella stessa posizione nel pool Front End.
    
      - Se si intende distribuire Mediation Server nel pool pool Front End Enterprise Edition, verificare che la casella di controllo sia selezionata. I ruoli del server verranno distribuiti nei server del pool.
    
      - Se si intende distribuire Mediation Server come server autonomo, deselezionare la casella di controllo appropriata. Mediation Server verrà distribuito in un passaggio di distribuzione distinto al termine della distribuzione completa di Front End Server.
    

    > [!NOTE]
    > È consigliabile aggiungere Mediation Server nella stessa posizione, se possibile. Per informazioni dettagliate sul supporto per server Mediation Server distribuiti nella stessa posizione o come server autonomi, vedere <A href="lync-server-2013-components-and-topologies-for-mediation-server.md">Componenti e topologie per Mediation Server in Lync Server 2013</A> nella documentazione relativa alla pianificazione.



6.  La pagina **Associare ruoli server al pool Front End** consente di definire e associare ruoli del server al pool Front End. È disponibile il seguente ruolo:
    
    **Abilita pool di server perimetrali:** consente di definire e associare un singolo pool server perimetrale o un pool di server perimetrali. Un server server perimetrale semplifica la comunicazione e la collaborazione tra utenti all'interno dell'organizzazione e persone al suo esterno, inclusi gli utenti federati.
    
    Esistono due possibili scenari che è possibile utilizzare per distribuire e associare i ruoli del server:
    
    Per il primo scenario, è necessario definire una nuova topologia per una nuova installazione. È possibile eseguire l'installazione scegliendo tra due metodi diversi:
    
      - Lasciare deselezionata la casella di controllo e continuare con la definizione della topologia. Dopo aver pubblicato, configurato e testato i ruoli Front End Server e server di back-end, è possibile eseguire nuovamente Generatore di topologie per aggiungere i ruoli del server alla topologia. Questa strategia consentirà di testare il pool Front End e il server che esegue SQL Server senza ulteriori complicazioni derivanti da altri ruoli. Dopo aver completato i test iniziali, è possibile eseguire nuovamente Generatore di topologie per selezionare i ruoli che è necessario distribuire.
    
      - Selezionare i ruoli che è necessario installare e quindi configurare l'hardware per gestire i ruoli selezionati.
    
    Nel secondo scenario si dispone di una distribuzione esistente e l'infrastruttura è pronta per i nuovi ruoli oppure è necessario associare ruoli esistenti a un nuovo Front End Server:
    
      - In questo caso, sarà necessario selezionare i ruoli che si intende distribuire o associare al nuovo Front End Server. In entrambi i casi, sarà necessario procedere con la definizione dei ruoli, la configurazione dell'hardware necessario e l'installazione.

7.  Nella pagina **Definire archivio SQL** eseguire una delle operazioni seguenti:
    
      - Per utilizzare un archivio di SQL Server esistente già definito nella topologia, selezionare **Archivio SQL** .
    
      - Per definire una nuova istanza di SQL Server per archiviare le informazioni del pool, fare clic su **Nuovo** e specificare l' **FQDN SQL Server** nella finestra di dialogo **Definisci nuovo archivio SQL** .
    
      - Per specificare il nome di un'istanza di SQL Server, selezionare **Istanza denominata** e quindi specificare il nome dell'istanza.
    
      - Per utilizzare l'istanza predefinita, fare clic su **Istanza predefinita** .
    
      - Per utilizzare il mirroring SQL, selezionare **Abilita mirroring SQL** e selezionare un'istanza esistente, o creare una nuova istanza.

8.  Nella pagina **Definire condivisione file** eseguire una delle operazioni seguenti:
    
      - Per utilizzare una condivisione file già definita nella topologia, selezionare **Utilizza condivisione file definita in precedenza** .
    
      - Per definire una nuova condivisione file, selezionare **Definisci nuova condivisione file** , nella casella **FQDN file server** immettere l'FQDN del file server esistente in cui deve trovarsi la condivisione file e quindi immettere un nome per la condivisione nella casella **Condivisione file** .
    
    > [!important]  
    > La condivisione file per Lync Server 2013 non può trovarsi nel server Front End Server. Si noti che in questo esempio la condivisione file è stata posizionata nel server Back End Server basato su SQL Server. Questa posizione può non risultare ottimale per i requisiti dell'organizzazione e un file server può rappresentare una scelta migliore. È possibile definire la condivisione file senza che questa sia stata creata. Sarà necessario creare la condivisione file nella posizione definita prima di pubblicare la topologia.

9.  Nella pagina **Specificare l'URL dei servizi Web** eseguire una o entrambe le operazioni seguenti:
    
    > [!important]  
    > L'URL di base è l'identità dei servizi Web per l'URL, senza https://. Se, ad esempio, l'URL completo per i servizi Web del pool è https://pool01.contoso.net, l'URL di base sarà pool01.contoso.net.    

    > [!WARNING]
    > Se si hanno più pool Front End o Front End Server, l'FQDN dei servizi Web esterni deve essere univoco. Ad esempio, se si definisce l'FQDN dei servizi Web esterni di un Front End Server come <STRONG>pool01.contoso.com</STRONG>, non sarà possibile utilizzare <STRONG>pool01.contoso.com</STRONG> per un altro pool Front End o Front End Server.

    
    1.  Se si intende configurare il bilanciamento del carico DNS, selezionare la casella di controllo **Sostituisci FQDN pool servizi Web interno** e immettere l'URL di base interno (che deve essere diverso dall'FQDN del pool e che potrebbe essere, ad esempio, internal-\<URL di base\>) in **URL di base interno** .
        

        > [!WARNING]
        > Se si decide di utilizzare un FQDN personalizzato per i servizi Web interni, ogni FQDN deve diverso da quello di tutti gli altri pool Front End, Server Director o pool di server Director. <STRONG>Usare solo i caratteri standard</STRONG> (A-Z, a-z, 0-9 e i trattini) per la definizione di URL o nomi di dominio completi. Non usare caratteri Unicode o caratteri di sottolineatura. I caratteri non standard in un URL o in un nome di dominio completo spesso non sono supportati dal sistema DNS esterno e dalle CA pubbliche, ovvero, quando l'URL o il nome di dominio completo deve essere assegnato al nome del soggetto o al nome alternativo del soggetto nel certificato.

    
    2.  È anche possibile immettere l'URL di base esterno in **URL di base esterno** . Immettere l'URL di base esterno per distinguerlo dai nomi di dominio interni. Si supponga, ad esempio, che il dominio interno sia contoso.net, ma che il nome di dominio esterno sia contoso.com. In questo caso, sarebbe necessario definire l'URL utilizzando il nome di dominio contoso.com. Questo aspetto è importante nel caso di un proxy inverso, in cui il nome di dominio dell'URL di base esterno sarebbe lo stesso del nome di dominio dell'FQDN del proxy inverso. Per la messaggistica istantanea e la presenza non è necessario l'accesso HTTP al pool Front End.
    

    > [!NOTE]
    > Per utilizzare il bilanciamento del carico DNS, è necessario creare i record DNS appropriati. Per informazioni dettagliate, vedere <A href="lync-server-2013-configure-dns-for-load-balancing.md">Configurare DNS per il bilanciamento del carico in Lync Server 2013</A>.



10. Se nella pagina **Selezione funzionalità** p stato selezionato **Servizi di conferenza** , selezionare **Associa il pool a un server Office Web Apps** nella pagina **Selezionare un server Office Web Apps** e fare clic su **Nuovo** (o selezionare un Server Office Web Apps esistente dal menu a discesa).

11. Nella finestra di dialogo **Definisci nuovo server Office Web Apps** , digitare il nome completo di dominio (FQDN) del computer Server Office Web Apps nella casella **FQDN Server Office Web Apps** . A questo punto, l'URL di individuazione di Server Office Web Apps dovrebbe comparire automaticamente nella casella **URL di individuazione server Office Web Apps:** .
    
    Se Server Office Web Apps è installato localmente e nella stessa area di rete di Lync Server 2013, l'opzione **Il server Office Web Apps è distribuito in una rete esterna (perimetro/Internet)** non deve essere selezionata.
    
    Se Server Office Web Apps è installato all'esterno del firewall interno, selezionare l'opzione **Il server Office Web Apps è distribuito in una rete esterna (perimetro/Internet)** .
    

    > [!NOTE]
    > Per informazioni dettagliate, vedere <A href="lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md">Configurazione dell'integrazione con Office Web Apps Server e Lync Server 2013</A>.



12. Nella pagina **Definire l'archivio SQL Server per l'archiviazione** , selezionare un'istanza SQL Server esistente, o definire una nuova istanza per l'archiviazione dei dati associati ai dati di archiviazione.

13. Nella pagina **Definire l'archivio SQL Server per il monitoraggio** , selezionare un'istanza SQL Server esistente, o definire una nuova istanza per l'archiviazione dei dati associati ai dati di monitoraggio.

14. Fare clic su **Avanti**. Se sono stati definiti altri ruoli del server nella pagina **Associare ruoli server al pool Front End**, verranno visualizzate pagine distinte della configurazione guidata dei ruoli per consentire di configurare i vari ruoli. Per ulteriori dettagli, vedere:
    
    [Distribuzione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-deploying-external-user-access.md)

15. Se non sono stati selezionati altri ruoli del server da configurare e distribuire oppure al termine della configurazione dei ruoli del server aggiuntivi, fare clic su **Fine** .

