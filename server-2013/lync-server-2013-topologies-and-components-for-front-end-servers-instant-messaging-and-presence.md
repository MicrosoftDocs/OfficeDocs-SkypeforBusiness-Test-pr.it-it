---
title: 'Lync Server 2013: Topologie e componenti per Front End Server, messaggistica istantanea e presenza'
TOCTitle: Topologie e componenti per Front End Server, messaggistica istantanea e presenza
ms:assetid: f08ce7a1-d14e-4a54-9771-a82c870658bf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412996(v=OCS.15)
ms:contentKeyID: 49302413
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Topologie e componenti per Front End Server, messaggistica istantanea e presenza in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-05-04_

Gli unici componenti necessari per la messaggistica istantanea e la presenza sono i seguenti:

  - I Front End Server o i server Standard Edition dell'organizzazione. Le funzionalità di messaggistica istantanea e presenza sono sempre abilitate in questi server.

  - Un servizio di bilanciamento del carico, se si dispone di un pool Front EndEnterprise Edition. Per ulteriori informazioni, vedere [Requisiti per il bilanciamento del carico per Lync Server 2013](lync-server-2013-load-balancing-requirements.md).

## Pianificazione per la distribuzione di pool Front End

In Lync Server 2013 l'architettura dei pool Front End è cambiata e le modifiche introdotte incidono sul modo in cui pianificare e mantenere i pool Front End.

È consigliabile che tutti i pool Front EndEnterprise Edition includano almeno tre Front End Server. In Lync Server l'architettura dei pool Front End utilizza un modello di sistema distribuito, in cui i dati di ogni utente vengono mantenuti in tre Front End Server nel pool. Per ulteriori informazioni su questa nuova architettura, vedere [Modifiche della topologia in Lync Server 2013](lync-server-2013-topology-changes.md).

Se non si desidera distribuire tre Front End ServerEnterprise Edition, ma si desidera disporre di ripristino di emergenza, è consigliabile utilizzare Lync ServerStandard Edition e creare due pool abbinati con una relazione di backup. Questo offre una soluzione di ripristino di emergenza con soli due server. Per ulteriori informazioni sulle topologie e le caratteristiche di disponibilità elevata e ripristino di emergenza, vedere [Pianificazione per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md).

## Pianificazione per la gestione di pool Front End

Per i pool Front End, seguire le linee guida contenute in questa sezione.

## Verificare il corretto funzionamento dei pool

Con il nuovo modello distribuito per i pool Front End, per il corretto funzionamento del pool è necessario che sia in esecuzione un determinato numero di server del pool. Per un pool sono previsti due modelli di perdita

  - La perdita del quorum a livello di gruppo di routing, causata da un numero insufficiente di server di replica per un determinato gruppo di routing. Un gruppo di routing consiste nell'aggregazione di un set di utenti ospitati nel pool. Ogni gruppo di routing dispone di tre repliche nel pool: una primaria e due secondarie.

  - La perdita del quorum a livello di pool, causata da un numero insufficiente di server di inizializzazione in esecuzione nel pool.

## Perdita del quorum a livello di gruppo di routing

Al primo avvio di un nuovo pool Front End, è fondamentale che l'85% dei server siano attivi e in esecuzione, come illustrato nella tabella seguente. Se il numero di server in esecuzione è inferiore, è possibile che i servizi rimangano bloccati allo stato di avvio e che il pool non venga avviato.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Numero totale di server nel pool</th>
<th>Numero minimo di server in esecuzione per il primo avvio del pool</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>2</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>3</p></td>
<td><p>3</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>3</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p>6</p></td>
<td><p>5</p></td>
</tr>
<tr class="even">
<td><p>7</p></td>
<td><p>5</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>6</p></td>
</tr>
<tr class="even">
<td><p>9</p></td>
<td><p>7</p></td>
</tr>
<tr class="odd">
<td><p>10</p></td>
<td><p>8</p></td>
</tr>
<tr class="even">
<td><p>11</p></td>
<td><p>9</p></td>
</tr>
<tr class="odd">
<td><p>12</p></td>
<td><p>10</p></td>
</tr>
</tbody>
</table>


A ogni avvio successivo del pool, sarà necessario l'avvio dell'85% dei server (come illustrato nella tabella precedente). Se non è possibile raggiungere questa soglia ma è comunque possibile avviare un numero di server sufficiente a non determinare la perdita del quorum a livello di pool, è possibile utilizzare il cmdlet **Reset-CsPoolRegistrarState –ResetType QuorumLossRecovery** per consentire al pool di eseguire il recupero dalla perdita del quorum a livello di gruppo di routing e proseguire. Per ulteriori informazioni sull'utilizzo del cmdlet, vedere [Reset-CsPoolRegistrarState](reset-cspoolregistrarstate.md).


> [!NOTE]
> Dal momento che Lync Server usa il database SQL primario come server di controllo, se si arresta il database primario e si passa alla copia mirror e quindi si arresta un numero di Front End Server tale da non soddisfare il numero minimo di server in esecuzione indicato dalla tabella precedente, verrà disattivato l'intero pool. Per ulteriori informazioni, vedere <A href="http://go.microsoft.com/fwlink/?linkid=393672">Server di controllo del mirroring del database</A>.



## Perdita del quorum a livello di pool

Il funzionamento di un pool Front End presuppone l'assenza di perdita del quorum a livello di pool. Se il numero di server in esecuzione scende al di sotto del livello funzionale (come illustrato nella tabella seguente), i server rimanenti nel pool arresteranno tutti i servizi Lync Server. I numeri nella tabella seguente presuppongono che i server back-end del pool siano in esecuzione.


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
<td><p>2</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>3-4</p></td>
<td><p>Ogni 2</p></td>
</tr>
<tr class="odd">
<td><p>5-6</p></td>
<td><p>Ogni 3</p></td>
</tr>
<tr class="even">
<td><p>7</p></td>
<td><p>Ogni 4</p></td>
</tr>
<tr class="odd">
<td><p>8-9</p></td>
<td><p>Ogni 4 dei primi 7 server</p></td>
</tr>
<tr class="even">
<td><p>10-12</p></td>
<td><p>Ogni 5 dei primi 9 server</p></td>
</tr>
</tbody>
</table>


Nella tabella precedente per “primi server” si intendono i server visualizzati per primi, in ordine cronologico, al primo avvio del pool. Per individuare questi server, è possibile utilizzare il cmdlet **Get-CsComputer** con l'opzione **–PoolFqdn**. Il cmdlet visualizzerà i server nell'ordine in cui compaiono nella topologia. I server in cima all'elenco sono i primi server.

## Pool Front End con due Front End Server

Non è consigliabile distribuire un pool Front End contenente due soli Front End Server. Se fosse necessario distribuire questo tipo di pool, seguire queste indicazioni:

  - Se uno dei due Front End Server si arresta, riattivarlo al più presto. Analogamente, se occorre aggiornare uno dei due server, riportarlo online subito dopo l'aggiornamento.

  - Se per qualche ragione si rende necessario arrestare entrambi i server contemporaneamente, al termine dell'intervento procedere come segue:
    
      - La procedura consigliata consiste nel riavviare entrambi i Front End Server contemporaneamente.
    
      - Se non è possibile riavviare entrambi i server contemporaneamente, riattivarli in ordine inverso rispetto a quello di arresto.
    
      - Se non è possibile riattivarli nell'ordine consigliato, prima di riattivare il pool, utilizzare il cmdlet seguente:
        
            Reset-CsPoolRegistrarState -ResetType QuorumLossRecovery -PoolFQDN <FQDN>

## Passaggi aggiuntivi per verificare il corretto funzionamento dei pool

Per assicurarsi che i pool Front End continuino a funzionare, è necessario tenere in considerazione qualche altro fattore.

  - Quando si spostano gli utenti nel pool per la prima volta, assicurarsi che siano in esecuzione almeno tre Front End Server.

  - Se si stabilisce una relazione di abbinamento tra questo pool e un altro pool ai fini del ripristino di emergenza, dopo aver stabilito la relazione è necessario verificare che in un determinato momento questo pool disponga di tre Front End Server in esecuzione simultanea per sincronizzare correttamente i dati con il pool di backup. Per ulteriori informazioni sulle funzionalità di abbinamento dei pool e di ripristino di emergenza, vedere [Pianificazione per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md).

## Miglioramento dell'affidabilità degli aggiornamenti del pool

Per aggiornare o applicare la patch ai server di un pool Front End, è necessario seguire il flusso di lavoro visualizzato in [Eseguire l'aggiornamento dei Front End Server in Lync Server 2013](lync-server-2013-upgrade-or-update-front-end-servers.md) e le linee guida seguenti:

  - Durante lo spostamento da un dominio di aggiornamento all'altro (seguendo il flusso di lavoro disponibile qui [Eseguire l'aggiornamento dei Front End Server in Lync Server 2013](lync-server-2013-upgrade-or-update-front-end-servers.md)), è necessario utilizzare il cmdlet **Get-CsPoolUpgradeReadinessState** e individuare lo stato "Ready". Aggiungendo un'attesa di 20 minuti tra un dominio di aggiornamento e l'altro al raggiungimento dello stato "Ready", l'affidabilità degli aggiornamenti sarà maggiore. Se nell'arco dei 20 minuti lo stato diventa **Not Ready**, riavviare il timer dei 20 minuti. Prima e dopo l'inizio dell'intervallo di 20 minuti è inoltre possibile eseguire il cmdlet **Get-CsPoolFabricState** per verificare che non siano state apportate modifiche alle istanze primarie e secondarie dei gruppi di routing.

  - Non passare al dominio di aggiornamento successivo se uno dei server nell'ultimo dominio di aggiornamento a cui è stata applicata la patch è bloccato o non è stato riavviato. Lo stesso vale se non è possibile avviare uno dei server di un aggiornamento. Eseguire **Get-CsPoolFabricState** per verificare che tutti i gruppi di routing dispongano di un'istanza primaria e almeno di un'istanza secondaria. In questo modo sarà possibile accertarsi che tutti gli utenti dispongano del servizio.

  - Se alcuni utenti dispongono del servizio e altri no, eseguire **Get-CsPoolFabricState** con l'opzione –Verbose per individuare i gruppi di routing con repliche mancanti. Non riavviare l'intero pool come primo tentativo di risoluzione del problema. Per ulteriori informazioni sul cmdlet, vedere [Get-CsPoolFabricState](get-cspoolfabricstate.md).

  - Verificare che tutte le istanze delle finestre di Visualizzatore eventi o Performance Monitor vengano chiuse per le installazioni e disinstallazioni di Windows Fabric.

## Modifica della configurazione di un pool Front End

Quando si aggiungono o si rimuovono Front End Server da un pool e quindi si pubblica la nuova topologia, seguire queste linee guida:

  - Dopo la pubblicazione della nuova topologia, è necessario riavviare ogni Front End Server del pool. Riavviarli uno alla volta.

  - Se durante le modifiche della configurazione è stato arrestato l'intero pool, dopo la pubblicazione della topologia eseguire il cmdlet seguente:
    
        Reset-CsPoolRegistrarState -PoolFQDN <PoolFQDN> -ResetType ServiceReset

Se un Front End Server si guasta e si prevede che non verrà sostituito entro pochi giorni, rimuovere il server dalla topologia. Aggiungere il nuovo Front End Server alla topologia quando sarà disponibile.

