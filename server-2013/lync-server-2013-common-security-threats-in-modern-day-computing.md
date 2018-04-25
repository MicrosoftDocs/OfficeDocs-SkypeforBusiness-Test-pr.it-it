---
title: Minacce comuni per la sicurezza negli ambienti di elaborazione moderni
TOCTitle: Minacce comuni per la sicurezza negli ambienti di elaborazione moderni
ms:assetid: 56d22197-e8e2-46b8-b3a3-507bd663700e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn433220(v=OCS.15)
ms:contentKeyID: 56558962
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Minacce comuni per la sicurezza negli ambienti di elaborazione moderni

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Poiché Lync Server 2013 è un sistema di comunicazione di fascia enterprise, è importante conoscere gli attacchi più comuni alla sicurezza a cui possono essere soggette la sua infrastruttura e le comunicazioni.

## Attacco tramite chiave compromessa

Una chiave è un codice o numero segreto utilizzato per crittografare, decrittografare o convalidare informazioni segrete. Nell'infrastruttura a chiave pubblica (PKI) vengono utilizzare due chiavi riservate che è necessario tenere in considerazione:

  - La chiave privata di cui dispone ciascun detentore di certificato

  - La chiave di sessione utilizzata dopo un'identificazione corretta e uno scambio delle chiavi di sessione da parte dei partner in comunicazione

Un attacco tramite chiave compromessa si verifica quando l'autore dell'attacco determina la chiave privata o la chiave di sessione. Quando l'autore dell'attacco riesce a determinare la chiave, la può utilizzare per decrittografare i dati crittografati all'insaputa del mittente.

Lync Server 2013 usa le funzionalità PKI del sistema operativo Windows Server per proteggere i dati di chiave utilizzati per la crittografia per le connessioni TLS (Transport Layer Security). Le chiavi usate per la crittografia multimediale vengono scambiate su connessioni TLS.

## Attacco di tipo Denial of Service alla rete

L'attacco di tipo *Denial of Service* si verifica quando l'autore dell'attacco impedisce il normale funzionamento e uso della rete da parte degli utenti validi, sovraccaricando il servizio con richieste legittime che impediscono l'uso del servizio da parte degli utenti legittimi. L'autore di un attacco di tipo Denial of Service è in grado di:

  - Inviare dati non validi alle applicazioni e ai servizi in esecuzione nella rete sottoposta all'attacco per disturbarne il normale funzionamento.

  - Inviare una grande quantità di traffico, sovraccaricando il sistema finché non smette di rispondere o risponde lentamente a richieste legittime.

  - Nascondere la prova degli attacchi.

  - Impedire agli utenti di accedere alle risorse di rete.

## Eavesdropping (sniffing, snooping)

Un attacco *eavesdropping* può verificarsi quando l'autore dell'attacco ottiene l'accesso al percorso dati in una rete e ha la possibilità di monitorare e leggere il traffico. Questo tipo di attacco è detto anche *sniffing* o *snooping*. Se il traffico è in testo normale, l'autore dell'attacco può leggerlo quando ottiene l'accesso al percorso. Un esempio è un attacco eseguito controllando un router nel percorso dati.

L'impostazione predefinita e il suggerimento principale per il traffico all'interno di Microsoft Lync Server 2013 consiste nell'utilizzare MTLS (Mutual TLS) tra server trusted e TLS da client a server, in modo da rendere questo attacco difficile o addirittura impossibile da attuare nell'intervallo di tempo in cui si verifica una determinata conversazione. TLS autentica tutte le parti e crittografa tutto il traffico. Questo non impedisce l'attacco ma impedisce all'autore di leggere il traffico a meno che non venga inficiata la crittografia.

Il protocollo Traversal Using Relay NAT (TURN) non impone la crittografia del traffico e le informazioni inviate sono protette dall'integrità del messaggio. Sebbene sia soggetto ad attacchi eavesdropping, le informazioni inviate, ovvero indirizzo IP e porta, possono essere estratte direttamente, semplicemente esaminando gli indirizzi di origine e di destinazione dei pacchetti. L'A/V Edge Server verifica che i dati siano validi controllando l'integrità del messaggio tramite la chiave derivata da alcuni elementi, tra cui una password TURN, che non viene mai inviata in testo non crittografato. Se viene usato il protocollo SRTP (Secure Real Time Protocol), viene crittografato anche il traffico multimediale.

## Spoofing di identità (spoofing dell'indirizzo IP)

Lo *spoofing* si verifica quando l'autore di un attacco determina e utilizza l'indirizzo IP di una rete, di un computer o di un componente di rete senza averne l'autorizzazione. Se l'autore riesce a portare a termine l'attacco, può operare come se fosse l'entità normalmente identificata dall'indirizzo IP. Nel contesto di Microsoft Lync Server 2013, questa situazione ha luogo solo se un amministratore ha eseguito entrambe le operazioni seguenti:

  - Ha configurato connessioni che supportano solo TCP (Transmission Control Protocol). Questa operazione è sconsigliata perché le comunicazioni TCP non vengono crittografate.

  - Ha contrassegnato gli indirizzi IP di tali connessioni come host trusted.

Questo rappresenta un problema di minore rilevanza per le connessioni TLS (Transport Layer Security), poiché TLS autentica tutte le parti e crittografa tutto il traffico. L'uso di TLS impedisce all'autore di un attacco di eseguire lo spoofing degli indirizzi IP in una connessione specifica, ad esempio una connessione MTLS, ma non impedisce di effettuare lo spoofing dell'indirizzo del server DNS utilizzato da Lync Server 2013. Tuttavia, dato che l'autenticazione in Lync avviene mediante certificati, l'autore di un attacco non disporrebbe di un certificato valido necessario per eseguire lo spoofing di una delle parti della comunicazione.

## Attacco di tipo man-in-the-middle

Un attacco man-in-the-middle si verifica quando l'autore di un attacco reinstrada la comunicazione tra due utenti attraverso il proprio computer senza che i due utenti che stanno comunicando ne siano a conoscenza. L'autore dell'attacco può monitorare e leggere il traffico prima di inviarlo al destinatario previsto. Ogni utente della comunicazione invia e riceve il traffico dall'autore dell'attacco a propria insaputa, pensando di comunicare solo con l'utente previsto. Questa situazione può verificarsi se l'autore dell'attacco è in grado di modificare Servizi di dominio Active Directory per aggiungere il proprio server come server trusted o modificare DNS (Domain Name System) per fare in modo che i client si connettano all'autore dell'attacco lungo il tragitto verso il server. Un attacco man-in-the-middle può verificarsi anche con il traffico multimediale tra due client, ma nella condivisione point-to-point di audio, video e applicazioni di Microsoft Lync Server 2013 i flussi vengono crittografati con SRTP tramite chiavi di crittografia negoziate tra i peer che utilizzano SIP (Session Initiation Protocol) su TLS. I server come Group Chat utilizzano HTTPS per proteggere il traffico Web.

## Attacco di tipo replay RTP

Un *attacco di tipo replay* si verifica quando una trasmissione multimediale valida tra due parti viene intercettata e ritrasmessa per finalità dannose. SRTP utilizzato insieme a un protocollo di segnalazione sicuro protegge le trasmissioni da attacchi di tipo replay consentendo al destinatario di mantenere un indice dei pacchetti RTP già ricevuti e di confrontare ogni nuovo pacchetto con quelli già elencati nell'indice.

## Messaggi istantanei indesiderati

I *messaggi istantanei indesiderati* sono costituiti da messaggi commerciali non desiderati o da richieste di sottoscrizione di presenza. Sebbene non costituiscano di per sé una violazione della rete, sono quanto meno fastidiosi, possono ridurre la produttività e la disponibilità delle risorse e provocare una violazione della rete. Un esempio è l'invio di richieste indesiderate da un utente a un altro. Ogni utente può bloccare gli altri per evitare questo problema, ma con la federazione, se viene perpetrato un attacco coordinato con invio di messaggi immediati indesiderati, può risultare difficile respingerlo a meno che non si disabiliti la federazione per il partner.

## Virus e worm

Un *virus* è un'unità di codice il cui scopo è quello di riprodurre altre unità di codice analoghe. Per funzionare, un virus necessita di un host, ad esempio un file, un messaggio di posta elettronica o un programma. Un *worm* è un'unità di codice il cui scopo è quello di riprodurre altre unità di codice analoghe, ma non necessita di un host. I virus e i worm si manifestano prevalentemente durante i trasferimenti di file tra client o quando vengono inviati URL da altri utenti. Un virus presente in un computer può, ad esempio, utilizzare l'identità dell'utente e inviare messaggi immediati per conto dell'utente.

## Informazioni personali

Microsoft Lync Server 2013 consente di divulgare informazioni in una rete pubblica che potrebbero essere collegate a una persona. È possibile distinguere due categorie specifiche di tipi di informazione:

  - **Dati sulla presenza avanzata:** i dati sulla presenza avanzata sono informazioni che un utente può decidere di condividere o non condividere in un collegamento a un partner federato o con i contatti all'interno di un'organizzazione. Questi dati non vengono condivisi con gli utenti di una rete di messaggistica istantanea pubblica. Con Criteri di gruppo e alcune impostazioni di configurazione client è possibile affidare una parte del controllo all'amministratore di sistema. In Lync Server 2013 è possibile configurare la modalità privacy della presenza avanzata per un singolo utente per impedire agli utenti Lync non presenti nell'elenco Contatti di visualizzare le informazioni sulla presenza dell'utente. La modalità privacy della presenza avanzata non impedisce agli utenti di Microsoft Office Communicator 2007 e Microsoft Office Communicator 2007 R2 di visualizzare le informazioni sulla presenza di un utente. Per informazioni dettagliate, vedere [Novità per i client in Lync Server 2013](lync-server-2013-what-s-new-for-clients.md) nella documentazione introduttiva e [Configurazione della modalità privacy della presenza avanzata](lync-server-2013-configuring-enhanced-presence-privacy-mode.md) nella documentazione relativa alla distribuzione.

  - **Dati obbligatori:** i dati obbligatori sono dati necessari per il corretto funzionamento del server o del client e NON sono sotto il controllo del client o dell'amministrazione di sistema. Si tratta di informazioni necessarie a livello di server o di rete ai fini del routing, del mantenimento dello stato e della segnalazione.

Nelle tabelle seguenti vengono elencati i dati esposti su una rete pubblica.

### Dati sulla presenza avanzata

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Dati esposti</th>
<th>Possibili impostazioni</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dati personali</p></td>
<td><p>Nome, posizione, società, indirizzo di posta elettronica, fuso orario</p></td>
</tr>
<tr class="even">
<td><p>Numero di telefono</p></td>
<td><p>Ufficio, cellulare, abitazione</p></td>
</tr>
<tr class="odd">
<td><p>Informazioni del calendario</p></td>
<td><p>Disponibilità, avviso di assenza, dettagli della riunione (per chi ha accesso al calendario dell'utente)</p></td>
</tr>
<tr class="even">
<td><p>Stato presenza</p></td>
<td><p>Non al computer, Disponibile, Occupato, Non disturbare, Offline</p></td>
</tr>
</tbody>
</table>


### Dati obbligatori

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Dati esposti</th>
<th>Informazioni di esempio</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Indirizzo IP</p></td>
<td><p>Indirizzo effettivo del computer o indirizzo NAT</p></td>
</tr>
<tr class="even">
<td><p>URI SIP</p></td>
<td><p>jeremylos@litwareinc.com</p></td>
</tr>
</tbody>
</table>

