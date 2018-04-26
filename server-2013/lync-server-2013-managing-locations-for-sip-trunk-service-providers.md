---
title: 'Lync Server 2013: Gestione delle posizioni per i provider di servizi trunk SIP'
TOCTitle: Gestione delle posizioni per i provider di servizi trunk SIP
ms:assetid: d9b33b56-66c2-4dee-b056-faaf98925bf2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398959(v=OCS.15)
ms:contentKeyID: 49302164
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestione delle posizioni per i provider di servizi trunk SIP in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-02_

Per configurare Lync Server in modo da individuare automaticamente i client in una rete, è necessario popolare il database del servizio Informazioni percorso con una mappa delle posizioni (wiremap) di rete e pubblicare le posizioni oppure definire un collegamento a un database esterno già contenente i mapping corretti. Come parte di questo processo, è necessario convalidare gli indirizzi civici delle posizioni con il provider di servizi di emergenza (E9-1-1). Per informazioni dettagliate, vedere [Configurare il database delle posizioni in Lync Server 2013](lync-server-2013-configure-the-location-database.md) nella documentazione relativa alla distribuzione.

Il database del servizio Informazioni percorso viene popolato con informazioni ERL (Emergency Response Location), costituite da un indirizzo civico e dalla posizione specifica all'interno di un edificio. Il campo **Location** del servizio Informazioni percorso, in cui è indicata la posizione specifica all'interno di un edificio, supporta una lunghezza massima di 20 caratteri, spazi inclusi. Tentare di includere gli elementi seguenti rispettando questi limiti di lunghezza:

  - Un nome di facile comprensione che identifichi la posizione del chiamante del servizio di emergenza (911), per consentire agli addetti del servizio di emergenza di trovare immediatamente la posizione specifica quando si recano all'indirizzo civico. Questo nome di posizione può includere il numero di edificio, l'indicazione della scala, il numero del piano, il numero di porta e così via. Evitare nomi alternativi noti solo ai dipendenti, altrimenti si rischia che gli addetti del servizio di emergenza si rechino nel luogo sbagliato.

  - Un identificatore di posizione che consenta agli utenti di verificare facilmente che il proprio client Lync abbia selezionato la posizione corretta. Il client Lync concatena e visualizza automaticamente i campi **Location** e **City** rilevati nell'intestazione. È consigliabile aggiungere l'indirizzo dell'edificio a ogni identificatore di posizione, ad esempio "1° piano \<indirizzo\>"). Se non viene specificato l'indirizzo, un identificatore di posizione generico come "1° piano" potrebbe riferirsi a qualsiasi edificio della città.

  - Se la posizione è approssimativa perché è determinata da un punto di accesso wireless, è possibile aggiungere la parola Near Near, ad esempio "Near 1° piano 1234".


> [!NOTE]
> Le posizioni aggiunte al database delle posizioni centrale sono disponibili per il client solo dopo la pubblicazione tramite un comando di Lync Server Management Shell e vengono replicate negli archivi locali del pool. Per informazioni dettagliate, vedere <A href="lync-server-2013-publish-the-location-database.md">Pubblicare il database delle posizioni</A> nella documentazione relativa alla distribuzione.



Nelle sezioni seguenti vengono riportate alcune considerazioni da tenere presenti per popolare e gestire il database delle posizioni.

## Popolamento del database delle posizioni

Le considerazioni seguenti possono essere utili per determinare come verrà popolato il database delle posizioni.

  - **Valutare quale processo verrà utilizzato per popolare il database delle posizioni.**  
    Esaminare dove si trovano i dati e quali operazioni è necessario eseguire per convertirli nel formato richiesto dal database delle posizioni. Considerare inoltre se le posizioni verranno aggiunte singolarmente o in gruppo tramite un file CSV.

<!-- end list -->

  - **Valutare se si dispone di un database di terze parti contenente già un mapping di posizioni.**  
    Utilizzando l'opzione del servizio Informazioni percorso secondario di Lync Server per connettersi a un database di terze parti, è possibile raggruppare e gestire le posizioni mediante una piattaforma offline. Uno dei vantaggi di questo approccio è che le posizioni possono essere associate non solo a identificatori di rete, ma anche a un utente. Questo significa che il servizio Informazioni percorso può restituire più indirizzi, derivanti dal servizio Informazioni percorso secondario, a un client Lync Server. L'utente può quindi scegliere la posizione più appropriata.
    
    Per l'integrazione con il servizio Informazioni percorso, il database di terze parti deve seguire lo schema di richiesta/risposta di posizione di Lync Server. Per informazioni dettagliate, vedere "\[MS-E911WS\]: servizio Web per la specifica del protocollo di supporto E911" all'indirizzo <http://go.microsoft.com/fwlink/p/?linkid=213819>. Per informazioni dettagliate sulla distribuzione di un servizio Informazioni percorso secondario, vedere [Configurare un servizio Informazioni percorso secondario](lync-server-2013-configure-a-secondary-location-information-service.md) nella documentazione relativa alla distribuzione.

Per informazioni dettagliate su come popolare il database delle posizioni, vedere [Configurare il database delle posizioni in Lync Server 2013](lync-server-2013-configure-the-location-database.md) nella documentazione relativa alla distribuzione.

## Gestione del database delle posizioni

Dopo aver popolato il database delle posizioni, è necessario sviluppare una strategia per aggiornarlo in base alle modifiche di configurazione della rete. Le considerazioni seguenti possono essere utili per determinare come verrà gestito il database delle posizioni.

  - **Valutare come verrà aggiornato il database delle posizioni.**  
    Esistono diversi scenari che richiedono un aggiornamento del database delle posizioni, tra cui l'aggiunta di punti di accesso wireless, il ricablaggio degli uffici (con assegnazioni diverse dei commutatori) e l'espansione delle subnet. Considerare se si prevede di aggiornare direttamente ogni singola posizione o di eseguire un aggiornamento in blocco delle posizioni mediante un file CSV.

<!-- end list -->

  - **Considerare se verrà utilizzata un'applicazione SNMP per creare una corrispondenza tra gli indirizzi MAC dei client Lync e gli identificatori di porte e commutatori,**  
    Se si utilizza un'applicazione SNMP, è necessario sviluppare un processo manuale per mantenere la coerenza a livello di informazioni su porte e chassis dei commutatori tra l'applicazione SNMP e il database delle posizioni. Se l'applicazione SNMP restituisce un indirizzo IP o un ID porta di chassis non incluso nel database, il servizio Informazioni percorso non sarà in grado di restituire una posizione al client.

