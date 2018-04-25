---
title: "Lync Server 2013: Esempio di raccolta dei requisiti dell'organizzazione per il controllo di ammissione di chiamata"
TOCTitle: "Esempio: raccolta dei requisiti dell'organizzazione per il controllo di ammissione di chiamata"
ms:assetid: 3363ac53-b7c4-4a59-aea1-b2f3ee016ae1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425827(v=OCS.15)
ms:contentKeyID: 49300120
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Esempio: raccolta dei requisiti dell'organizzazione per il controllo di ammissione di chiamata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questo esempio viene illustrato come pianificare e implementare il servizio Controllo di ammissione di chiamata (CAC). A livello generale, sono previste le attività seguenti:

1.  Identificare tutti gli hub e le backbone di rete (note come *aree di rete* ).

2.  Identificare il sito centrale di Lync Server che gestirà il servizio Controllo di ammissione di chiamata per ogni area di rete.

3.  Identificare e definire i *siti di rete* connessi a ogni area di rete.

4.  Per ogni sito di rete la cui connessione alla WAN è vincolata dalla larghezza di banda, descrivere la capacità della larghezza di banda della connessione WAN e gli eventuali limiti di larghezza di banda impostati dall'amministratore di rete per il traffico multimediale di Lync Server. Non è necessario includere siti con connessione alla WAN non soggetta a vincoli di larghezza di banda.

5.  Associare ogni subnet della rete a un sito di rete.

6.  Eseguire il mapping dei collegamenti tra le aree di rete. Per ogni collegamento, descrivere la capacità della larghezza di banda e gli eventuali limiti definiti dall'amministratore di rete per il traffico multimediale di Lync Server.

7.  Definire una route tra ogni coppia di aree di rete.

## Raccogliere le informazioni necessarie

Per la preparazione per il servizio Controllo di ammissione di chiamata, raccogliere le informazioni descritte nei passaggi seguenti:

1.  Identificare le aree di rete. Un'area di rete rappresenta una backbone o un hub di rete.
    
    Una backbone o un hub di rete è una parte dell'infrastruttura della rete del computer che interconnette diverse parti della rete, fornendo un percorso per lo scambio di informazioni tra diverse LAN o subnet. Una backbone può unire reti diverse, da una piccola postazione a un'area geografica estesa. La capacità della backbone è in genere superiore a quella delle reti a essa connesse.
    
    Nella topologia di esempio sono presenti tre aree di rete: Nord America, EMEA e APAC. In un'area di rete è contenuto un insieme di siti di rete. Consultarsi con l'amministratore di rete per definire le aree di rete dell'organizzazione.

2.  Identificare il sito centrale associato a ogni area di rete. Un sito centrale include almeno un Front End Server e rappresenta la distribuzione di Lync Server che gestirà il servizio Controllo di ammissione di chiamata per tutto il traffico multimediale che attraversa la connessione WAN dell'area di rete.
    
    **Rete aziendale di esempio divisa in tre aree di rete**
    
    ![Esempio di topologia di rete con tre aree di rete](images/Gg425827.08937347-250f-488f-ba5f-c256e6afcd8b(OCS.15).jpg "Esempio di topologia di rete con tre aree di rete")  
    

    > [!NOTE]
    > Una rete Multiprotocol Label Switching (MPLS) dovrebbe essere rappresentata come area di rete in cui a ogni posizione geografica corrisponde un sito di rete. Per informazioni dettagliate, vedere l'argomento " <A href="lync-server-2013-call-admission-control-on-an-mpls-network.md">Controllo di ammissione di chiamata in una rete MPLS con Lync Server 2013</A>" nella documentazione relativa alla pianificazione.

    
    Nella topologia di rete di esempio precedente sono presenti tre aree di rete, ognuna con un sito centrale di Lync Server che gestisce il servizio Controllo di ammissione di chiamata. Il sito centrale appropriato per un'area di rete viene scelto in base alla vicinanza geografica. Poiché il traffico multimediale sarà più intenso all'interno delle aree di rete, la proprietà per vicinanza geografica rende il traffico autonomo e ne garantisce il funzionamento anche in caso di non disponibilità degli altri siti centrali.
    
    In questo esempio una distribuzione di Lync Server denominata Chicago è il sito centrale dell'area Nord America.
    
    Tutti gli utenti di Lync del Nord America sono situati in server della distribuzione Chicago. Nella tabella seguente sono elencati i siti centrali per tutte e tre le aree di rete.
    
    ### Aree di rete e siti centrali associati
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Area di rete</th>
    <th>Sito Centrale</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Nord America</p></td>
    <td><p>Chicago</p></td>
    </tr>
    <tr class="even">
    <td><p>EMEA</p></td>
    <td><p>Londra</p></td>
    </tr>
    <tr class="odd">
    <td><p>APAC</p></td>
    <td><p>Pechino</p></td>
    </tr>
    </tbody>
    </table>
    

    > [!NOTE]
    > A seconda della topologia di Lync Server, è possibile assegnare lo stesso sito centrale a più aree di rete.



3.  Per ogni area di rete, identificare tutti i siti di rete (uffici o postazioni) le cui connessioni WAN non siano vincolate dalla larghezza di banda. Poiché questi siti non sono vincolati dalla larghezza di banda, non è necessario applicare criteri di larghezza di banda del servizio Controllo di ammissione di chiamata.
    
    Nell'esempio illustrato nella tabella seguente tre siti di rete non dispongono di collegamenti WAN con vincoli di larghezza di banda: New York, Chicago e Detroit.
    
    ### Siti di rete non vincolati dalla larghezza di banda della WAN
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Sito di rete</th>
    <th>Area di rete</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>New York</p></td>
    <td><p>Nord America</p></td>
    </tr>
    <tr class="even">
    <td><p>Chicago</p></td>
    <td><p>Nord America</p></td>
    </tr>
    <tr class="odd">
    <td><p>Detroit</p></td>
    <td><p>Nord America</p></td>
    </tr>
    </tbody>
    </table>


4.  Per ogni area di rete identificare tutti i siti di rete che si connettono all'area di rete mediante collegamenti WAN con vincoli di larghezza di banda.
    
    Per garantire la qualità audio e video, è consigliabile fare in modo che le WAN dei siti di rete con vincoli di larghezza di banda siano monitorate e applicare criteri di larghezza di banda del servizio Controllo di ammissione di chiamata che limitino il flusso del traffico multimediale (vocale o video) scambiato con l'area di rete.
    
    Nell'esempio illustrato nella tabella seguente sono presenti tre siti di rete vincolati dalla larghezza di banda della WAN: Portland, Reno e Albuquerque.
    
    ### Siti di rete vincolati dalla larghezza di banda della WAN
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Sito di rete</th>
    <th>Area di rete</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Albuquerque</p></td>
    <td><p>Nord America</p></td>
    </tr>
    <tr class="even">
    <td><p>Reno</p></td>
    <td><p>Nord America</p></td>
    </tr>
    <tr class="odd">
    <td><p>Portland</p></td>
    <td><p>Nord America</p></td>
    </tr>
    </tbody>
    </table>
    
    **Area di rete Nord America con servizio Controllo di ammissione di chiamata con tre siti di rete non vincolati dalla larghezza di banda (Chicago, New York e Detroit) e tre siti di rete vincolati dalla larghezza di banda della WAN (Portland, Reno e Albuquerque)**
    
    ![Siti di rete di esempio vincolati dalla larghezza di banda WAN](images/Gg425827.d9d1f231-db4d-4dd7-8fbc-eb0b6d1e705d(OCS.15).jpg "Siti di rete di esempio vincolati dalla larghezza di banda WAN")  

5.  Per ogni collegamento WAN con vincoli di larghezza di banda, determinare quanto segue:
    
      - Limite di larghezza di banda globale che si desidera impostare per tutte le sessioni audio simultanee. Se una nuova sessione audio comporta il superamento di questo limite, Lync Server ne impedisce l'avvio.
    
      - Limite di larghezza di banda che si desidera impostare per ogni singola sessione audio. Il limite di larghezza di banda predefinito per il servizio Controllo di ammissione di chiamata è 175 kbps, ma può essere modificato dall'amministratore.
    
      - Limite di larghezza di banda globale che si desidera impostare per tutte le sessioni video simultanee. Se una nuova sessione video comporta il superamento di questo limite, Lync Server ne impedisce l'avvio.
    
      - Limite di larghezza di banda che si desidera impostare per ogni singola sessione video. Il limite di larghezza di banda predefinito per il servizio Controllo di ammissione di chiamata è 700 kbps, ma può essere modificato dall'amministratore.
    
    ### Siti di rete con informazioni sui vincoli della larghezza di banda della WAN (larghezza di banda in kbps)
    
    <table style="width:100%;">
    <colgroup>
    <col style="width: 14%" />
    <col style="width: 14%" />
    <col style="width: 14%" />
    <col style="width: 14%" />
    <col style="width: 14%" />
    <col style="width: 14%" />
    <col style="width: 14%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Sito di rete</th>
    <th>Area di rete</th>
    <th>Limite di larghezza di banda</th>
    <th>Limite audio</th>
    <th>Limite sessione audio</th>
    <th>Limite video</th>
    <th>Limite sessione video</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Albuquerque</p></td>
    <td><p>Nord America</p></td>
    <td><p>5.000</p></td>
    <td><p>2.000</p></td>
    <td><p>175</p></td>
    <td><p>1.400</p></td>
    <td><p>700</p></td>
    </tr>
    <tr class="even">
    <td><p>Reno</p></td>
    <td><p>Nord America</p></td>
    <td><p>10.000</p></td>
    <td><p>4.000</p></td>
    <td><p>175</p></td>
    <td><p>2.800</p></td>
    <td><p>700</p></td>
    </tr>
    <tr class="odd">
    <td><p>Portland</p></td>
    <td><p>Nord America</p></td>
    <td><p>5.000</p></td>
    <td><p>4.000</p></td>
    <td><p>175</p></td>
    <td><p>2.800</p></td>
    <td><p>700</p></td>
    </tr>
    <tr class="even">
    <td><p>New York</p></td>
    <td><p>Nord America</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    </tr>
    <tr class="odd">
    <td><p>Chicago</p></td>
    <td><p>Nord America</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    </tr>
    <tr class="even">
    <td><p>Detroit</p></td>
    <td><p>Nord America</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    </tr>
    </tbody>
    </table>


6.  Per ogni subnet della rete, specificare il sito di rete associato.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Ogni subnet della rete deve essere associata a un sito di rete, anche se non vincolato dalla larghezza di banda, poiché il servizio Controllo di ammissione di chiamata utilizza le informazioni delle subnet per determinate il sito di rete in cui è posizionato un endpoint. Dopo che sono state determinate le posizioni in entrambe le parti della sessione, il servizio Controllo di ammissione di chiamata può determinare se la larghezza di banda è sufficiente per stabilire una chiamata. Quando viene stabilita una sessione su un collegamento senza limiti di larghezza di banda, viene generato un avviso.<br />
    Se si distribuiscono Audio/Video Edge Server, gli indirizzi IP pubblici di ognuno di questi server deve essere associato al sito di rete in cui è distribuito il server. Ogni indirizzo IP pubblico dell'A/V Edge Server deve essere aggiunto alle impostazioni di configurazione di rete come subnet con subnet mask 32. Se ad esempio si distribuiscono A/V Edge Server nel sito di Chicago, creare per ogni indirizzo IP esterno di tali server una subnet con subnet mask 32 e associare il sito di rete Chicago a tali subnet. Per informazioni dettagliate sugli indirizzi IP pubblici, vedere <a href="lync-server-2013-determine-external-a-v-firewall-and-port-requirements.md">Determinare i requisiti di porte e firewall A/V esterni per Lync Server 2013</a> nella documentazione relativa alla pianificazione.</td>
    </tr>
    </tbody>
    </table>
    

    > [!NOTE]
    > Viene generato un avviso Key Health Indicator (KHI) in cui viene specificato un elenco di indirizzi IP presenti nella rete che non sono associati a una subnet oppure la cui subnet non è associata a un sito di rete. Questo avviso viene generato una sola volta ogni 8 ore. Di seguito vengono riportati un esempio e le informazioni rilevanti dell'avviso:<BR><STRONG>Origine :</STRONG> Servizio criteri larghezza di banda CS (Core)<BR><STRONG>Numero evento :</STRONG> 36034<BR><STRONG>Livello :</STRONG> 2<BR><STRONG>Descrizione :</STRONG> le subnet per gli indirizzi IP seguenti: &lt;Elenco di indirizzi IP&gt; non sono configurate oppure non sono associate a un sito di rete.<BR><STRONG>Causa :</STRONG> le subnet per gli indirizzi IP corrispondenti non sono presenti nelle impostazioni della configurazione di rete oppure non sono associate a un sito di rete.<BR><STRONG>Soluzione :</STRONG> aggiungere le subnet per gli indirizzi IP corrispondenti alle impostazioni della configurazione di rete e associare ogni subnet a un sito di rete.<BR>Se ad esempio nell'elenco di indirizzi IP nell'avviso sono specificati sia 10.121.248.226 che 10.121.249.20, questi indirizzi IP non sono associati a una subnet oppure la subnet a cui sono associati non appartiene a un sito di rete. Se 10.121.248.0/24 e 10.121.249.0/24 sono le subnet corrispondenti per questi indirizzi, è possibile risolvere il problema in questo modo: 
    > <OL>
    > <LI>
    > <P>Verificare che l'indirizzo IP 10.121.248.226 sia associato alla subnet 10.121.248.0/24 e che l'indirizzo IP 10.121.249.20 sia associato alla subnet 10.121.249.0/24.</P>
    > <LI>
    > <P>Verificare che le subnet 10.121.248.0/24 e 10.121.249.0/24 siano associate ognuna a un sito di rete.</P></LI></OL>

    
    ### Siti di rete e subnet associate (larghezza di banda in kbps)
    
    <table>
    <colgroup>
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Sito di rete</th>
    <th>Area di rete</th>
    <th>Limite di larghezza di banda</th>
    <th>Limite audio</th>
    <th>Limite sessione audio</th>
    <th>Limite video</th>
    <th>Limite sessione video</th>
    <th>Subnet</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Albuquerque</p></td>
    <td><p>Nord America</p></td>
    <td><p>5.000</p></td>
    <td><p>2.000</p></td>
    <td><p>175</p></td>
    <td><p>1.400</p></td>
    <td><p>700</p></td>
    <td><p>172.29.79.0/23, 157.57.215.0/25, 172.29.90.0/23, 172.29.80.0/24</p></td>
    </tr>
    <tr class="even">
    <td><p>Reno</p></td>
    <td><p>Nord America</p></td>
    <td><p>10.000</p></td>
    <td><p>4.000</p></td>
    <td><p>175</p></td>
    <td><p>2.800</p></td>
    <td><p>700</p></td>
    <td><p>157.57.210.0/23, 172.28.151.128/25</p></td>
    </tr>
    <tr class="odd">
    <td><p>Portland</p></td>
    <td><p>Nord America</p></td>
    <td><p>5.000</p></td>
    <td><p>4.000</p></td>
    <td><p>175</p></td>
    <td><p>2.800</p></td>
    <td><p>700</p></td>
    <td><p>172.29.77.0/24 10.71.108.0/24, 157.57.208.0/23</p></td>
    </tr>
    <tr class="even">
    <td><p>New York</p></td>
    <td><p>Nord America</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>172.29.80.0/23, 157.57.216.0/25, 172.29.91.0/23, 172.29.81.0/24</p></td>
    </tr>
    <tr class="odd">
    <td><p>Chicago</p></td>
    <td><p>Nord America</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>157.57.211.0/23, 172.28.152.128/25</p></td>
    </tr>
    <tr class="even">
    <td><p>Detroit</p></td>
    <td><p>Nord America</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>(nessun limite)</p></td>
    <td><p>172.29.78.0/24 10.71.109.0/24, 157.57.209.0/23</p></td>
    </tr>
    </tbody>
    </table>


7.  Nel servizio Controllo di ammissione di chiamata di Lync Server le connessioni tra aree di rete sono denominate *collegamenti aree* . Come per i siti di rete, determinare per ogni collegamento area gli aspetti seguenti:
    
      - Limite di larghezza di banda globale che si desidera impostare per tutte le sessioni audio simultanee. Se una nuova sessione audio comporta il superamento di questo limite, Lync Server ne impedisce l'avvio.
    
      - Limite di larghezza di banda che si desidera impostare per ogni singola sessione audio. Il limite di larghezza di banda predefinito per il servizio Controllo di ammissione di chiamata è 175 kbps, ma può essere modificato dall'amministratore.
    
      - Limite di larghezza di banda globale che si desidera impostare per tutte le sessioni video simultanee. Se una nuova sessione video comporta il superamento di questo limite, Lync Server ne impedisce l'avvio.
    
      - Limite di larghezza di banda che si desidera impostare per ogni singola sessione video. Il limite di larghezza di banda predefinito per il servizio Controllo di ammissione di chiamata è 700 kbps, ma può essere modificato dall'amministratore.
    
    **Collegamenti aree di rete con limiti di larghezza di banda associati**
    
    ![Esempio di limitazioni fra tre aree](images/Gg425827.25259afa-ee7c-4d26-bc41-92ba9cb56dec(OCS.15).jpg "Esempio di limitazioni fra tre aree")  
    
    ### Informazioni sulla larghezza di banda dei collegamenti aree (larghezza di banda in kbps)
    
    <table>
    <colgroup>
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Nome collegamento area</th>
    <th>Prima area</th>
    <th>Seconda area</th>
    <th>Limite di larghezza di banda</th>
    <th>Limite audio</th>
    <th>Limite sessione audio</th>
    <th>Limite video</th>
    <th>Limite sessione video</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>COLLEGAMENTO-NA-EMEA</p></td>
    <td><p>Nord America</p></td>
    <td><p>EMEA</p></td>
    <td><p>50.000</p></td>
    <td><p>20.000</p></td>
    <td><p>175</p></td>
    <td><p>14.000</p></td>
    <td><p>700</p></td>
    </tr>
    <tr class="even">
    <td><p>COLLEGAMENTO-EMEA-APAC</p></td>
    <td><p>EMEA</p></td>
    <td><p>APAC</p></td>
    <td><p>25.000</p></td>
    <td><p>10.000</p></td>
    <td><p>175</p></td>
    <td><p>7.000</p></td>
    <td><p>700</p></td>
    </tr>
    </tbody>
    </table>


8.  Definire una route tra ogni coppia di aree di rete.
    

    > [!NOTE]
    > Sono necessari due collegamenti per la route tra le aree Nord America e APAC poiché non sono connesse direttamente tramite un collegamento area.

    
    ### Route aree
    
    <table>
    <colgroup>
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Nome route area</th>
    <th>Prima area</th>
    <th>Seconda area</th>
    <th>Collegamenti aree</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>ROUTE-NA-EMEA</p></td>
    <td><p>Nord America</p></td>
    <td><p>EMEA</p></td>
    <td><p>COLLEGAMENTO-NA-EMEA</p></td>
    </tr>
    <tr class="even">
    <td><p>ROUTE-EMEA-APAC</p></td>
    <td><p>EMEA</p></td>
    <td><p>APAC</p></td>
    <td><p>COLLEGAMENTO-EMEA-APAC</p></td>
    </tr>
    <tr class="odd">
    <td><p>ROUTE-NA-APAC</p></td>
    <td><p>Nord America</p></td>
    <td><p>APAC</p></td>
    <td><p>COLLEGAMENTO-NA-EMEA, COLLEGAMENTO-EMEA-APAC</p></td>
    </tr>
    </tbody>
    </table>


9.  Per ogni coppia di siti di rete direttamente connessi tramite un collegamento singolo, denominato collegamento *tra siti* , determinare quanto segue:
    
      - Limite di larghezza di banda globale che si desidera impostare per tutte le sessioni audio simultanee. Se una nuova sessione audio comporta il superamento di questo limite, Lync Server ne impedisce l'avvio.
    
      - Limite di larghezza di banda che si desidera impostare per ogni singola sessione audio. Il limite di larghezza di banda predefinito per il servizio Controllo di ammissione di chiamata è 175 kbps, ma può essere modificato dall'amministratore.
    
      - Limite di larghezza di banda globale che si desidera impostare per tutte le sessioni video simultanee. Se una nuova sessione video comporta il superamento di questo limite, Lync Server ne impedisce l'avvio.
    
      - Limite di larghezza di banda che si desidera impostare per ogni singola sessione video. Il limite di larghezza di banda predefinito per il servizio Controllo di ammissione di chiamata è 700 kbps, ma può essere modificato dall'amministratore.
    
    **Area di rete Nord America con servizio Controllo di ammissione di chiamata in cui vengono indicate le capacità di larghezza di banda e i limiti di larghezza di banda per il collegamento tra siti tra Reno e Albuquerque**
    
    ![Esempio di siti di rete vincolati dalla larghezza di banda WAN](images/Gg425827.063e5e1d-b6c8-4e8c-98db-c227c78f671d(OCS.15).jpg "Esempio di siti di rete vincolati dalla larghezza di banda WAN")  
    
    ### Informazioni sulla larghezza di banda per un collegamento tra siti tra due siti di rete (larghezza di banda in kbps)
    
    <table>
    <colgroup>
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Nome collegamento tra siti</th>
    <th>Primo sito</th>
    <th>Secondo sito</th>
    <th>Limite di larghezza di banda</th>
    <th>Limite audio</th>
    <th>Limite sessione audio</th>
    <th>Limite video</th>
    <th>Limite sessione video</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Collegamento-TraSiti-Reno-Albu</p></td>
    <td><p>Reno</p></td>
    <td><p>Albuquerque</p></td>
    <td><p>20.000</p></td>
    <td><p>12.000</p></td>
    <td><p>175</p></td>
    <td><p>5.000</p></td>
    <td><p>700</p></td>
    </tr>
    </tbody>
    </table>


## Operazioni successive

Dopo aver raccolto le informazioni necessarie, è possibile eseguire la distribuzione del servizio Controllo di ammissione di chiamata utilizzando Lync Server Management Shell o il Pannello di controllo di Lync Server.


> [!NOTE]
> Benché sia possibile eseguire la maggior parte delle operazioni di configurazione di rete usando Pannello di controllo di Lync Server, per creare le subnet e i collegamenti tra siti, è necessario usare Lync Server Management Shell. Per informazioni dettagliate, vedere la documentazione relativa a Lync Server Management Shell per il cmdlet <STRONG>New-CsNetworkSubnet</STRONG> e il cmdlet <STRONG>New-CsNetworkIntersitePolicy</STRONG>.


