---
title: 'Lync Server 2013: Pianificazione della capacità del server Chat persistente'
TOCTitle: Pianificazione della capacità del server Chat persistente
ms:assetid: 7a850cd5-c789-4795-a8ff-083be21ae784
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615006(v=OCS.15)
ms:contentKeyID: 49301075
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione della capacità del server Chat persistente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il server Chat persistente consente di eseguire una chat multiutente in tempo reale e persistente, per recuperi e ricerche future. Diversamente dalla messaggistica istantanea di gruppo, che viene salvata nella cassetta postale di un utente se è configurata la cronologia delle conversazioni, una sessione del server Chat persistente resta aperta più a lungo, e il contenuto, così come i messaggi, i file, gli URL e gli altri dati della conversazione sono salvati su un server.

La pianificazione della capacità è un importante componente della preparazione della distribuzione di server Chat persistente. In questo argomento sono incluse informazioni dettagliate sulle topologie di server Chat persistente supportate e le tabelle di pianificazione della capacità che è possibile utilizzare per determinare la configurazione migliore per la distribuzione. Viene inoltre descritto come gestire al meglio le distribuzioni di server Chat persistente per cui è necessaria capacità maggiore nelle ore di punta.

Per scaricare server Chat persistente, vedere "Microsoft Lync Server 13 server Chat persistente" all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=209539](http://go.microsoft.com/fwlink/p/?linkid=209539).

Per informazioni dettagliate sull'installazione di server Chat persistente, vedere [Installazione del server Chat persistente in Lync Server 2013](lync-server-2013-installing-persistent-chat-server.md) e [Configurazione del server Chat persistente in Lync Server 2013](lync-server-2013-configuring-persistent-chat-server.md) nella documentazione relativa alla distribuzione.

Gli strumenti di supporto, tra cui lo Strumento di pianificazione di Lync Server, possono essere di aiuto nella pianificazione della capacità. Per informazioni dettagliate su Strumento di pianificazione, vedere [Inizio del processo di pianificazione per Lync Server 2013](lync-server-2013-beginning-the-planning-process.md) nella documentazione relativa alla pianificazione.

## Topologie supportate di server Chat persistente

È possibile distribuire server Chat persistente in pool di server singolo e di server multiplo, e in topologie a pool singolo e a pool multiplo.

Da ora è offerto il supporto per server Chat persistente su server Standard Edition per le nuove distribuzioni di Lync Server 2013. Tuttavia, prestazioni e scalabilità ne risentiranno, e dal momento che per questa nuova distribuzione non è prevista l'opzione di elevata disponibilità, è consigliabile utilizzare il supporto principalmente per installazioni di prova, valutazioni e così via.


> [!NOTE]
> Per ulteriori informazioni su entrambe le topologie, vedere <A href="lync-server-2013-planning-for-persistent-chat-server.md">Pianificazione del server Chat persistente in Lync Server 2013</A> in questa documentazione e <A href="lync-server-2013-deploying-persistent-chat-server.md">Distribuzione del server Chat persistente in Lync Server 2013</A> nella documentazione relativa alla distribuzione.



## Topologia a server singolo

La configurazione minima e la distribuzione più semplice di server Chat persistente prevede una topologia server Chat persistenteFront End Server a server singolo. In questa distribuzione è richiesto un singolo server che esegue server Chat persistente (ed esegue facoltativamente il servizio di conformità, se la conformità è abilitata), un server che ospita entrambi i database di SQL Server e, se è richiesta la conformità, il database di SQL Server per archiviare i dati di conformità.

> [!important]  
> Non è possibile aggiungere server aggiuntivi a un pool di server Chat persistente avviato come distribuzione a server singolo in Generatore di topologie. È consigliabile utilizzare la topologia del pool a server multiplo anche nei casi in cui si utilizza un server singolo, poiché in questo modo è possibile aggiungere più server in seguito, qualora se ne presentasse la necessità.

Nella figura seguente sono illustrati tutti i componenti obbligatori e facoltativi di una topologia per un singolo server Chat persistenteFront End Server con conformità.

**Singolo server di Chat persistente**

![Topologia a un solo server con Compliance Service](images/Gg398500.9168fa52-61e0-4d17-a14d-45fd32e81456(OCS.15).jpg "Topologia a un solo server con Compliance Service")

## Topologia a più server

Per offrire capacità e affidabilità maggiori, è possibile distribuire una topologia a più server, descritta in [Pianificazione del server Chat persistente in Lync Server 2013](lync-server-2013-planning-for-persistent-chat-server.md). La topologia a più server può includere fino a quattro computer attivi che eseguono server Chat persistente (le configurazioni per la disponibilità elevata e il ripristino di emergenza consentiranno fino a otto computer, ma solo quattro possono essere attivi e i rimanenti quattro saranno in standby). Ogni server può supportare fino a 20.000 utenti simultanei, per un totale di 80.000 utenti simultanei connessi a un pool di server Chat persistente con 4 server. Una topologia a più server è analoga a una topologia a server singolo, con la differenza che più server ospitano server Chat persistente e possono offrire maggiore scalabilità. Più computer che eseguono server Chat persistente devono risiedere nello stesso dominio di Servizi di dominio Active Directory di Lync Server e del servizio di conformità.

Nella figura seguente vengono illustrati tutti i componenti di una topologia a più server con più computer che eseguono server Chat persistente, il servizio di conformità facoltativo e un database di conformità distinto.

**Più server di Chat persistente**

![Topologia a più server](images/Gg398500.19aea898-28df-4d9b-903c-f72ef062d919(OCS.15).jpg "Topologia a più server")

In una distribuzione di server Chat persistente con quattro server, in cui 80.000 utenti possono essere simultaneamente connessi e utilizzare Chat persistente, il carico viene distribuito uniformemente con 20.000 utenti per ogni server. Se un server diventa non disponibile, gli utenti a esso connessi perdono il proprio accesso a server Chat persistente. Gli utenti disconnessi vengono automaticamente trasferiti ai server rimanenti fino a quando il server non disponibile non viene ripristinato. A seconda della quantità di traffico di Chat persistente nella rete, questo trasferimento può richiedere pochi minuti o più tempo. Poiché ciascuno dei server rimanenti può dover ospitare fino a 30.000 utenti, è consigliabile ripristinare il server non disponibile il più rapidamente possibile per evitare problemi di prestazioni. Altrimenti, è possibile rendere disponibile un altro server Chat persistente attraverso Generatore di topologie o il cmdlet Windows PowerShell, **set-CsPersistentChatActiveServer**.

## Pianificazione della capacità di server Chat persistente

La tabella seguente può semplificare la pianificazione della capacità per server Chat persistente. Nella tabella viene mostrato come la modifica di diverse impostazioni di server Chat persistente influisca sulle funzionalità di capacità.

## Pianificazione della capacità massima per server Chat persistente

Utilizzare la tabella di esempio seguente per determinare il numero di utenti che sarà possibile supportare.

### Esempio della capacità massima di pool di server Chat persistente

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Istanze attive del servizio Chat persistente</p></td>
<td><p><em>4</em></p></td>
</tr>
<tr class="even">
<td><p>Istanze del servizio Chat persistente</p></td>
<td><p><em>8 (4 must be inactive; only a maximum of 4 can be active)</em></p></td>
</tr>
<tr class="odd">
<td><p>Utenti attivi connessi</p></td>
<td><p><em>80,000</em></p></td>
</tr>
<tr class="even">
<td><p>Totale utenti serviti</p></td>
<td><p>150.000</p></td>
</tr>
<tr class="odd">
<td><p>Numero di endpoint</p></td>
<td><p>120.000</p></td>
</tr>
</tbody>
</table>


Nell'esempio precedente il piano prevede il supporto del numero massimo di utenti consentito da server Chat persistente: quattro server/istanze del servizio Chat persistente (è possibile avere ulteriori quattro server passivi che eseguono server Chat persistente per elevata disponibilità e ripristino di emergenza) e 20.000 utenti per ogni server, per un totale di 80.000 utenti attivi.

## Pianificazione della capacità per la gestione dell'accesso alle Chat persistente room

La tabella seguente può semplificare la pianificazione della gestione dell'accesso alle Chat persistente room in un pool di server Chat persistente.

### Esempio di gestione dell'accesso alle chat

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
<th>Chat di piccole dimensioni</th>
<th>Chat di medie dimensioni</th>
<th>Chat di grandi dimensioni</th>
<th>Totale</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dimensioni delle chat room (numero di utenti connessi)</p></td>
<td><p>30 utenti per chat</p></td>
<td><p>150 utenti per chat</p></td>
<td><p>16.000 utenti per chat</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Chat</p></td>
<td><p>32.000</p></td>
<td><p>1.067</p></td>
<td><p>10</p></td>
<td><p>33.077</p></td>
</tr>
<tr class="odd">
<td><p>% di chat che sono auditorium</p></td>
<td><p>1%</p></td>
<td><p>1%</p></td>
<td><p>50%</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>% di chat che sono aperte</p></td>
<td><p>3%</p></td>
<td><p>3%</p></td>
<td><p>50%</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Chat aperte (appartenenza non esplicita)</p></td>
<td><p>960</p></td>
<td><p>32</p></td>
<td><p>5</p></td>
<td><p>997</p></td>
</tr>
<tr class="even">
<td><p>Chat non aperte (chat regolari con appartenenza esplicita)</p></td>
<td><p>31.040</p></td>
<td><p>1,035</p></td>
<td><p>5</p></td>
<td><p>32.080</p></td>
</tr>
<tr class="odd">
<td><p>Sale auditorium (ingresso relatori aggiuntivi)</p></td>
<td><p>0</p></td>
<td><p>32</p></td>
<td><p>5</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Chat gestite per appartenenza diretta</p></td>
<td><p>50%</p></td>
<td><p>10%</p></td>
<td><p>0%</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Chat gestite per gruppi di utenti</p></td>
<td><p>50%</p></td>
<td><p>90%</p></td>
<td><p>100%</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gruppi di utenti in ogni elenco di membri di una chat per le chat aperte (non specificati esplicitamente)</p></td>
<td><p>0</p></td>
<td><p>0</p></td>
<td><p>0</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Utenti in ogni elenco di membri di una chat per le chat non aperte</p></td>
<td><p>30</p></td>
<td><p>150</p></td>
<td><p>16.000</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gruppi di utenti in ogni elenco di membri di una chat per le chat non aperte</p></td>
<td><p>3</p></td>
<td><p>5</p></td>
<td><p>10</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Utenti e gruppi di utenti in ogni elenco dei gestori delle chat (per chat aperte e non aperte)</p></td>
<td><p>6</p></td>
<td><p>6</p></td>
<td><p>6</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Utenti e gruppi di utenti in ogni elenco dei relatori delle sale auditorium (per chat aperte e non aperte)</p></td>
<td><p>6</p></td>
<td><p>6</p></td>
<td><p>6</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Entità di appartenenza basata sugli utenti in tutte le chat non aperte</p></td>
<td><p>465.600</p></td>
<td><p>15.520</p></td>
<td><p>-</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Entità di appartenenza basata sui gruppi di utenti in tutte le chat non aperte</p></td>
<td><p>46.560</p></td>
<td><p>4656</p></td>
<td><p>50</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Entità di appartenenza basata sui gruppi di utenti in tutte le sale auditorium</p></td>
<td><p>0</p></td>
<td><p>192</p></td>
<td><p>50</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Entità di gestione basata sui gruppi di utenti in tutte le chat per ogni elenco dei gestori</p></td>
<td><p>192.000</p></td>
<td><p>6.400</p></td>
<td><p>60</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Utenti attivi per chat</p></td>
<td><p><em>30</em></p></td>
<td><p><em>150</em></p></td>
<td><p><em>16,000</em></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Chat per utente</p></td>
<td><p><em>12</em></p></td>
<td><p><em>2</em></p></td>
<td><p><em>2</em></p></td>
<td><p><em>16</em></p></td>
</tr>
<tr class="odd">
<td><p>Gruppi di utenti in ogni elenco di membri di una chat</p></td>
<td><p><em>10</em></p></td>
<td><p><em>10</em></p></td>
<td><p><em>15</em></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Chat gestite per gruppi di utenti</p></td>
<td><p><em>50%</em></p></td>
<td><p><em>50%</em></p></td>
<td><p><em>50%</em></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Entità di appartenenza basata sui gruppi di utenti in tutte le chat</p></td>
<td><p>155.200</p></td>
<td><p>5173</p></td>
<td><p>68</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Entità di appartenenza basata sugli utenti in tutte le chat</p></td>
<td><p>465.600</p></td>
<td><p>77.600</p></td>
<td><p>72.000</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Utenti e gruppi di utenti in ogni elenco dei gestori delle chat, dei relatori delle chat e degli ambiti</p></td>
<td><p>6</p></td>
<td><p>6</p></td>
<td><p>6</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Utenti e gruppi in tutti gli elenchi dei gestori delle chat, dei relatori delle chat e degli ambiti</p></td>
<td><p>192.000</p></td>
<td><p>6400</p></td>
<td><p>60</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Voci di controllo di accesso</p></td>
<td><p>704.160</p></td>
<td><p>26.768</p></td>
<td><p>160</p></td>
<td><p>731.088</p></td>
</tr>
<tr class="even">
<td><p>Voci di controllo di accesso massime</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>2.000.000</p></td>
</tr>
</tbody>
</table>


Nell'esempio precedente i server server Chat persistente distribuiti in base alle linee guida consigliate possono gestire fino a 80.000 utenti in un pool di quattro server con la conformità abilitata.

In questo esempio vengono illustrate le chat suddivise in base alle categorie di chat di piccole dimensioni (30 utenti attivi in qualsiasi momento specificato), di medie dimensioni (150 utenti attivi) e di grandi dimensioni (16.000 utenti attivi). Il numero di chat di una determinata dimensione viene calcolato in base al numero totale di:

  - Utenti attivi nel sistema

  - Utenti attivi nelle chat delle dimensioni specificate

  - Chat delle dimensioni specificate cui partecipa ogni singole utente

Per ogni chat, la tabella di pianificazione della capacità precedente specifica il numero di voci di controllo di accesso associate, incluse le voci assegnate direttamente alla chat. È possibile controllare l'accesso a singole chat tramite elenchi di controllo di accesso. È inoltre possibile controllare l'accesso a livello di categoria. In un elenco di controllo di accesso una singola voce di controllo di accesso può corrispondere a un gruppo di utenti, ad esempio un gruppo di sicurezza, una lista di distribuzione o a un singolo utente. È possibile definire voci di controllo di accesso per gestori, relatori e membri delle chat.

> [!important]  
> Nel pianificare la strategia per la gestione delle chat, tenere presente che il numero totale di voci di controllo di accesso consentite è 2 milioni. Se le voci di controllo di accesso calcolate superano i 2 milioni, le prestazioni del server possono subire conseguenze negative significative. Per evitare questo problema, assicurarsi che le voci di controllo di accesso siano costituite, laddove possibile, da gruppi di utenti anziché da singoli utenti.

## Pianificazione della capacità per la gestione dell'accesso alle chat in base a invito

È possibile utilizzare la tabella di pianificazione della capacità seguente per calcolare il numero di inviti creati da server Chat persistente e archiviati nel database di Chat persistente quando è configurato per l'invio di inviti. È possibile gestire gli inviti nella categoria dalla pagina **Impostazioni categoria chat** in Pannello di controllo di Lync Server, o attraverso il cmdlet di Windows PowerShell**set-csPersistentChatCategory**. È possibile gestire gli inviti a una chat room (a seconda di quanto consentito dalla categoria), utilizzando la pagina **Gestione chat** avviata dal client Lync, oppure attraverso il cmdlet di Windows PowerShell**set-csPersistentChatRoom**.

I dati di esempio contenuti nella tabella seguente presuppongono che nella pagina **Impostazioni chat** per il 50% di tutte le chat l'opzione **Invitations** è impostata su **Sì** .

> [!important]  
> Se il valore calcolato per il numero di inviti generati dal server supera 1 milione, le prestazioni del server possono subire conseguenze negative significative. Per evitare questo problema, assicurarsi di ridurre al minimo il numero di chat configurate per l'invio di inviti o di limitare il numero di utenti che possono partecipare alle chat configurate per l'invio di inviti.

### Esempio di accesso alle chat in base a invito

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
<th>Chat di piccole dimensioni</th>
<th>Chat di medie dimensioni</th>
<th>Chat di grandi dimensioni</th>
<th>Totale</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utenti che possono accedere alla chat</p></td>
<td><p>30 utenti per chat</p></td>
<td><p>150 utenti per chat</p></td>
<td><p>16.000 utenti per chat</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Percentuale di chat configurate per l'invio di inviti</p></td>
<td><p>50%</p></td>
<td><p>50%</p></td>
<td><p>50%</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Chat configurate per l'invio di inviti</p></td>
<td><p><em>16,000</em></p></td>
<td><p><em>533</em></p></td>
<td><p><em>5</em></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Utenti che possono accedere alla chat</p></td>
<td><p><em>60</em></p></td>
<td><p><em>225</em></p></td>
<td><p><em>16,000</em></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Inviti generati da server Chat persistente</p></td>
<td><p>960.000</p></td>
<td><p>120.000</p></td>
<td><p>80.000</p></td>
<td><p>1.160.000</p></td>
</tr>
<tr class="even">
<td><p>Numero massimo consentito di inviti</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>2.000.000</p></td>
</tr>
<tr class="odd">
<td><p>Modello 1 - Iniziare con il numero stimato di messaggi giornalieri per chat</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Tasso per chat (giornaliero)</p></td>
<td><p>50</p></td>
<td><p>500</p></td>
<td><p>100</p></td>
<td><p>650</p></td>
</tr>
<tr class="odd">
<td><p>Tasso chat (per secondo), tutte le chat</p></td>
<td><p>55,56</p></td>
<td><p>18,52</p></td>
<td><p>0,03</p></td>
<td><p>74</p></td>
</tr>
<tr class="even">
<td><p>Modello 2 - Iniziare con il numero di messaggi inviati per utente, giornalmente</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Tasso chat per utente (giornaliero)</p></td>
<td><p>15</p></td>
<td><p>5</p></td>
<td><p>0,1</p></td>
<td><p>20</p></td>
</tr>
<tr class="even">
<td><p>Tasso per chat (giornaliero)</p></td>
<td><p>38</p></td>
<td><p>375</p></td>
<td><p>800</p></td>
<td><p>1.213</p></td>
</tr>
<tr class="odd">
<td><p>Tasso chat (per secondo), tutte le chat</p></td>
<td><p>41,67</p></td>
<td><p>13,89</p></td>
<td><p>0,28</p></td>
<td><p>56</p></td>
</tr>
</tbody>
</table>


## Modello utente delle prestazioni di server Chat persistente

Nella tabella seguente viene descritto il modello utente per server Chat persistente. Vengono forniti gli elementi di base per i requisiti di pianificazione della capacità e viene rappresentata una tipica organizzazione con 80.000 utenti simultanei su quattro server.

### Modello utente delle prestazioni di server Chat persistente

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Numero di utenti attivi connessi</p></td>
<td><p>80.000</p></td>
</tr>
<tr class="even">
<td><p>Numero di istanze del servizio server Chat persistente</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p>Numero di utenti di chat di piccole dimensioni</p></td>
<td><p>30 utenti</p></td>
</tr>
<tr class="even">
<td><p>Numero di utenti di chat di medie dimensioni</p></td>
<td><p>150 utenti</p></td>
</tr>
<tr class="odd">
<td><p>Numero di utenti di chat di grandi dimensioni</p></td>
<td><p>16.000 utenti</p></td>
</tr>
<tr class="even">
<td><p>Numero totale di chat</p></td>
<td><p>33.077</p></td>
</tr>
<tr class="odd">
<td><p>Numero di chat di piccole dimensioni</p></td>
<td><p>32.000</p></td>
</tr>
<tr class="even">
<td><p>Numero di chat di medie dimensioni</p></td>
<td><p>1.067</p></td>
</tr>
<tr class="odd">
<td><p>Numero di chat di grandi dimensioni</p></td>
<td><p>10</p></td>
</tr>
<tr class="even">
<td><p>Numero totale di chat per utente</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Numero di chat di piccole dimensioni per utente</p></td>
<td><p>12</p></td>
</tr>
<tr class="even">
<td><p>Numero di chat di medie dimensioni per utente</p></td>
<td><p>2</p></td>
</tr>
<tr class="odd">
<td><p>Numero di chat di grandi dimensioni per utente</p></td>
<td><p>2</p></td>
</tr>
<tr class="even">
<td><p>Numero di chat visitate per utente</p></td>
<td><p>24</p></td>
</tr>
<tr class="odd">
<td><p>Frequenza di partecipazione di punta</p></td>
<td><p>10/secondo</p></td>
</tr>
<tr class="even">
<td><p>Frequenza di chat totale</p></td>
<td><p>24/secondo</p></td>
</tr>
<tr class="odd">
<td><p>Frequenza di chat per chat di piccole dimensioni</p></td>
<td><p>22,22/secondo</p></td>
</tr>
<tr class="even">
<td><p>Frequenza di chat per chat di medie dimensioni</p></td>
<td><p>1,67/secondo</p></td>
</tr>
<tr class="odd">
<td><p>Frequenza di chat per chat di grandi dimensioni</p></td>
<td><p>circa 0,15/secondo</p></td>
</tr>
<tr class="even">
<td><p>Percentuale di chat configurate per l'invio di inviti</p></td>
<td><p>50%</p></td>
</tr>
<tr class="odd">
<td><p>Percentuale di appartenenza diretta</p></td>
<td><p>50%</p></td>
</tr>
<tr class="even">
<td><p>Percentuale di appartenenza a gruppi</p></td>
<td><p>50%</p></td>
</tr>
<tr class="odd">
<td><p>Numero medio di affiliazioni predecessori in Servizi di dominio Active Directory</p></td>
<td><p>100 - 200</p></td>
</tr>
<tr class="even">
<td><p>Numero di contatti sottoscritti per utente</p></td>
<td><p>80</p></td>
</tr>
<tr class="odd">
<td><p>Numero medio di endpoint per utente</p></td>
<td><p>1,5</p></td>
</tr>
<tr class="even">
<td><p>Numero medio di chat visibili per endpoint</p></td>
<td><p>1,5</p></td>
</tr>
<tr class="odd">
<td><p>Numero medio di chat visibili per utente</p></td>
<td><p>2,25 (50% per 1 chat e 50% per 2 chat); fino a 6 chat aperte, una per monitor</p></td>
</tr>
<tr class="even">
<td><p>Numero di partecipanti sottoposti a polling per intervallo</p></td>
<td><p>25 per ogni chat visibile</p></td>
</tr>
<tr class="odd">
<td><p>Durata dell'intervallo di polling</p></td>
<td><p>5 minuti</p></td>
</tr>
<tr class="even">
<td><p>Numero di partecipanti sottoposti a polling al secondo</p></td>
<td><p>15.000</p></td>
</tr>
<tr class="odd">
<td><p>Numero di modifiche delle informazioni sulla presenza all'ora per utente</p></td>
<td><p>6</p></td>
</tr>
<tr class="even">
<td><p>Numero di modifiche delle informazioni sulla presenza al secondo</p></td>
<td><p>133,33</p></td>
</tr>
</tbody>
</table>

