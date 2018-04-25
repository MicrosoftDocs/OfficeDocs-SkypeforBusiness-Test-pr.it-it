---
title: 'Lync Server 2013: Pianificazione della resilienza vocale del sito centrale'
TOCTitle: Pianificazione della resilienza vocale del sito centrale
ms:assetid: 52dd0c3e-cd3c-44cf-bef5-8c49ff5e4c7a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398347(v=OCS.15)
ms:contentKeyID: 49300589
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione della resilienza vocale del sito centrale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Le aziende dispongono sempre più spesso di diversi siti sparsi in tutto il mondo. È pertanto fondamentale per qualsiasi soluzione di resilienza di VoIP aziendale mantenere i servizi di emergenza, poter accedere all'helpdesk e poter eseguire attività aziendali critiche quando un sito centrale è fuori servizio. Quando un sito centrale diventa non disponibile, devono essere soddisfatte le condizioni seguenti:

  - Deve essere predisposto il failover dei servizi vocali.

  - Gli utenti che normalmente si registrano nel pool Front End nel sito centrale devono essere in grado di registrarsi in un pool Front End alternativo. Per ottenere questo risultato è possibile creare più record DNS SRV, ognuno dei quali viene risolto in un pool di server Director o in un pool Front End in ognuno dei siti centrali. È possibile adattare priorità e pesi dei record SRV, in modo che gli utenti serviti da tale sito centrale ottengano il Server Director e pool Front End corrispondente prima di quelli in altri record SRV.

  - Le chiamate verso e da utenti in altri siti devono essere reindirizzate al PSTN.

Questo argomento descrive la soluzione consigliata per la protezione della resilienza dei servizi vocali del sito centrale.

## Architettura e topologia

Per pianificare la resilienza dei servizi vocali di un sito centrale è necessaria una comprensione di base del ruolo centrale svolto dalla funzione di registrazione di Lync Server 2013 nell'abilitazione del failover dei servizi vocali. La funzione di registrazione di Lync Server è un ruolo del server che consente la registrazione e l'autenticazione dei client, oltre a fornire servizi di routing. Tale ruolo risiede insieme ad altri componenti in un server Standard Edition, in un Front End Server, in un Server Director o in un Survivable Branch Appliance. Un pool di registrazione è costituito da servizi di registrazione eseguiti nel pool Front End e posizionati nello stesso sito. Il pool Front End deve essere a carico bilanciato. È consigliabile usare il bilanciamento del carico DNS, ma una soluzione di bilanciamento del carico hardware è comunque accettabile. Un client Lync individua il pool pool Front End tramite il meccanismo di individuazione seguente:

1.  Record SRV DNS

2.  Servizio Web di individuazione automatica (nuovo in Lync Server 2013)

3.  Opzione DHCP 120

Dopo che il client Lync si è connesso al pool Front End, viene indirizzato dal servizio di bilanciamento del carico verso uno dei Front End Server del pool. Questo Front End Server, a sua volta, reindirizza il client verso una funzione di registrazione preferita nel pool.

Ogni utente abilitato per VoIP aziendale viene assegnato a un particolare pool di registrazione, che diventa il pool di registrazione principale dell'utente. In ogni sito, un singolo pool di registrazione principale è solitamente condiviso da centinaia o migliaia di utenti. Per pianificare il consumo delle risorse del sito centrale da parte di eventuali utenti di siti di succursale che si basano sul sito centrale per i servizi di presenza, conferenza o failover, è consigliabile considerare ogni utente di sito di succursale come se fosse un utente registrato nel sito centrale. Non esistono attualmente limiti al numero di utenti di siti di succursale, inclusi gli utenti registrati in un Survivable Branch Appliance.

Per garantire la resilienza dei servizi vocali in caso di errore del sito centrale, per il pool di registrazione principale deve esistere un singolo pool di registrazione di backup designato in un altro sito. È possibile configurare il backup con le impostazioni di resilienza di Generatore di topologie. Presupponendo l'esistenza di un collegamento WAN resiliente tra due siti, gli utenti per cui non è più disponibile il pool di registrazione principale verranno reindirizzati automaticamente al pool di registrazione di backup.

I passaggi seguenti descrivono il processo di individuazione e registrazione dei client:

1.  Un client individua Lync Server tramite record DNS SRV. In Lync Server 2013, i record DNS SRV possono essere configurati per restituire più di un FQDN alla query DNS SRV. Ad esempio, se l'azienda Contoso dispone di tre siti centrali (Nord America, Europa e Asia-Pacifico) e un pool di server Director in ogni sito centrale, i record DNS SRV possono puntare ai nomi FQDN del pool di server Director in ognuna delle tre posizioni. Fino a quando è disponibile il pool di server Director in una delle posizioni, il client può connettersi al primo hop di Lync Server.
    

    > [!NOTE]
    > L'uso di un pool di server Director è facoltativo. Come alternativa si può usare un pool Front End.



2.  Il pool di server Director fornisce informazioni al client Lync sul pool di registrazione principale e quello di backup dell'utente.

3.  Il client Lync tenta di connettersi prima di tutto al pool di registrazione principale dell'utente. Se è disponibile, la registrazione viene accettata. Se il pool di registrazione principale non è disponibile, il client Lync tenta la connessione al pool di backup. Se questo è disponibile e ha verificato la non disponibilità del pool principale (rilevando la mancanza di un heartbeat per un intervallo di failover specificato), il pool di registrazione di backup accetta la registrazione dell'utente. Quando il pool di backup rileva che il pool di registrazione principale è di nuovo disponibile, i client Lync di failover verranno reindirizzati al pool principale designato.

Nella figura seguente viene illustrata la topologia consigliata per garantire la resilienza del sito centrale. I due siti sono connessi tramite un collegamento WAN resiliente. Se il sito centrale diventa non disponibile, gli utenti assegnati a tale pool vengono indirizzati al sito di backup per la registrazione.

**Topologia consigliata per la resilienza dei servizi vocali del sito centrale**

![Topologia per la resilienza vocale del sito centrale](images/Gg398347.19ea3e74-8a5c-488c-a34e-fc180ab9a50a(OCS.15).jpg "Topologia per la resilienza vocale del sito centrale")

## Requisiti e raccomandazioni

I requisiti e le raccomandazioni seguenti per l'implementazione della resilienza dei servizi vocali del sito centrale sono appropriati per la maggior parte delle organizzazioni:

  - I siti in cui risiedono i pool di registrazione principale e di backup dovrebbero essere connessi tramite un collegamento WAN resiliente.

  - Ogni sito centrale deve contenere un pool di registrazione composto da una o più funzioni di registrazione.

  - Il carico di ogni pool di registrazione deve essere bilanciato tramite il bilanciamento del carico DNS, il bilanciamento del carico hardware o entrambi. Per informazioni dettagliate sulla pianificazione della configurazione del bilanciamento del carico, vedere [Requisiti per il bilanciamento del carico per Lync Server 2013](lync-server-2013-load-balancing-requirements.md).

  - Ogni utente deve essere assegnato a un pool di registrazione principale tramite il cmdlet di Lync Server Management Shell**set-CsUser** o il Pannello di controllo di Lync Server.

  - Per il pool di registrazione principale deve esistere un singolo pool di registrazione di backup posizionato in un diverso sito centrale.

  - Il pool di registrazione principale deve essere configurato per il failover sul pool di registrazione di backup. Per impostazione predefinita, il pool principale è impostato per eseguire il failover sul pool di back dopo un intervallo di 300 secondi. Questo intervallo può essere modificato tramite Generatore di topologie di Lync Server 2013.

  - Configurare una route di failover come descritto nell'argomento “ [Configurazione di una route di failover in Lync Server 2013](lync-server-2013-configuring-a-failover-route.md)” nella documentazione relativa alla pianificazione. Durante la configurazione della route specificare un gateway posizionato in un sito diverso da quello del gateway impostato nella route principale.

  - Se il sito centrale ospita il server di gestione principale ed è probabile che il sito rimanga inattivo per un lungo periodo, sarà necessario reinstallare gli strumenti di gestione nel sito di backup. In caso contrario, non sarà possibile apportare alcuna modifica alle impostazioni di gestione.

## Dipendenze

Per assicurare la resilienza dei servizi vocali, Lync Server dipende dall'infrastruttura e dai componenti software seguenti:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Componente</strong></p></td>
<td><p><strong>Funzione</strong></p></td>
</tr>
<tr class="even">
<td><p>DNS</p></td>
<td><p>Risoluzione dei record SRV e A per la connettività tra server e tra server e client</p></td>
</tr>
<tr class="odd">
<td><p>Exchange e Servizi Web Exchange</p></td>
<td><p>Archiviazione dei contatti; dati del calendario</p></td>
</tr>
<tr class="even">
<td><p>Messaggistica unificata di Exchange e Servizi Web Exchange</p></td>
<td><p>Registri chiamate, segreteria telefonica e messaggi di segreteria telefonica</p></td>
</tr>
<tr class="odd">
<td><p>Opzione DHCP 120</p></td>
<td><p>Se non sono disponibili record DNS SRV, il client tenterà di utilizzare l'opzione DHCP 120 per individuare la funzione di registrazione. Questo meccanismo funziona solo se è configurato un server DHCP oppure se è abilitato il componente DHCP di Lync Server 2013. Per informazioni dettagliate, vedere i requisiti hardware e software per la resilienza dei siti di succursale nella sezione <a href="lync-server-2013-branch-site-resiliency-requirements.md">Requisiti di resilienza dei siti di succursale per Lync Server 2013</a>.</p></td>
</tr>
</tbody>
</table>


## Funzionalità vocali disponibili

Se si implementano i requisiti e le raccomandazioni precedenti, il pool di registrazione di backup renderà disponibili le funzionalità vocali seguenti:

  - Chiamate PSTN in uscita

  - Chiamate PSTN in entrata, se il provider di servizi di telefonia supporta il failover su un sito di backup.

  - Chiamate Enterprise tra utenti dello stesso sito e di due siti diversi

  - Gestione di base delle chiamate inclusi la messa in attesa, il recupero e il trasferimento

  - Messaggistica istantanea tra due parti e condivisione di audio e video tra utenti nello stesso sito

  - Inoltro di chiamata, squillo simultaneo degli endpoint, delega delle chiamate e servizi di intercettazione team, ma solo se entrambe le parti della delega, oppure tutti i membri del team, sono configurati nello stesso sito

  - I telefoni ei client esistenti continuano a funzionare.

  - Registrazione dettagli chiamata (CDR)

  - Autenticazione e autorizzazione

A seconda della modalità di configurazione, le funzionalità vocali seguenti potrebbero o meno funzionare quando un sito centrale principale è fuori servizio:

  - Recapito e recupero di messaggi di segreteria telefonica
    
    Se si desidera rendere disponibile la messaggistica unificata di Exchange quando il sito centrale principale è fuori servizio, è necessario eseguire una delle operazioni seguenti:
    
      - Modificare i record DNS SRV in modo che i server di messaggistica unificata di Exchange nel sito centrale puntino ai server di messaggistica unificata di Exchange di backup in un altro sito.
    
      - Configurare il dial plan di Messaggistica unificata di Exchange per ogni utente in modo che includa i server di Messaggistica unificata di Exchange sia nel sito centrale che nel sito di backup, ma designare i server di Messaggistica unificata di Exchange di backup come disabilitati. Se il sito principale diventa non disponibile, l'amministratore di Exchange dovrà contrassegnare come abilitati i server di Messaggistica unificata di Exchange nel sito di backup.
    
    Se nessuna delle soluzioni precedenti è praticabile, la Messaggistica unificata di Exchange non sarà disponibile nel caso il sito centrale diventi non disponibile.

  - Conferenze di tutti i tipi
    
    Un utente reindirizzato su un sito di backup per il failover può partecipare a una conferenza creata e ospitata da un organizzatore assegnato a un pool disponibile, ma non può creare o ospitare una conferenza nel suo pool principale, che non è più disponibile. In modo analogo, altri utenti non potranno partecipare alle conferenze ospitate nel pool principale dell'utente interessato dal problema.

Le funzionalità vocali seguenti non sono disponibili quando un sito centrale principale è fuori servizio:

  - Operatore Conferenza

  - Routing basato su DNS e basato sulla presenza

  - Aggiornamento delle impostazioni di inoltro di chiamata.

  - Response Group Service e parcheggio di chiamata

  - Provisioning di nuovi telefoni e client

  - Ricerca Web nella Rubrica

## Vedere anche

#### Ulteriori risorse

[Pianificazione della resilienza vocale del sito di succursale in Lync Server 2013](lync-server-2013-planning-for-branch-site-voice-resiliency.md)

