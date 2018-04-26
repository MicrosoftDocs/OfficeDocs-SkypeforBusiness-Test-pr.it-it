---
title: 'Lync Server 2013: Gestione delle posizioni per i gateway ELIN'
TOCTitle: Gestione delle posizioni per i gateway ELIN
ms:assetid: ced79c13-4e7e-4034-95cd-6fc913f4f222
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205288(v=OCS.15)
ms:contentKeyID: 49302008
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestione delle posizioni per i gateway ELIN in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per fare in modo che in Lync Server vengano fornite automaticamente le posizioni dei client di una rete, è necessario eseguire le attività seguenti:

  - Popolare il database del servizio Informazioni percorso con una mappa delle posizioni (wiremap) di rete e includere i numeri ELIN (Emergency Location Identification Number) nel campo CompanyName.

  - Pubblicare le posizioni in modo che siamo disponibili per i client nella rete.

  - Caricare i numeri ELIN nel database ALI (Automatic Location Identification) del gestore della rete PSTN (Public Switched Telephone Network).

Per informazioni dettagliate su come eseguire queste attività, vedere [Configurare il database delle posizioni in Lync Server 2013](lync-server-2013-configure-the-location-database.md) nella documentazione relativa alla distribuzione.


> [!NOTE]
> Le posizioni aggiunte al database delle posizioni centrale sono disponibili per il client solo dopo la pubblicazione tramite un comando di Lync Server Management Shell e vengono replicate negli archivi locali del pool. Per informazioni dettagliate, vedere <A href="lync-server-2013-publish-the-location-database.md">Pubblicare il database delle posizioni</A> nella documentazione relativa alla distribuzione.



In questa sezione vengono descritti gli aspetti da prendere in considerazione quando si pianificano l'aggiornamento e la gestione del database delle posizioni.

## Pianificazione delle posizioni di emergenza

Quando si utilizzano i gateway ELIN, si popola il database del servizio Informazioni percorso con l'indirizzo civico, l'indicazione specifica della posizione all'interno di un edificio e almeno un numero ELIN per ogni posizione. Durante la fase di pianificazione, è opportuno decidere come denominare le posizioni e come assegnare i numeri ELIN.

## Pianificazione dei nomi delle posizioni

Il campo **Location** del servizio Informazioni percorso, in cui è indicata la posizione specifica all'interno di un edificio, supporta una lunghezza massima di 20 caratteri, spazi inclusi. Tentare di includere gli elementi seguenti rispettando questi limiti di lunghezza:

  - Un nome di facile comprensione che identifichi la posizione del chiamante del servizio di emergenza (911), per consentire agli addetti del servizio di emergenza di trovare immediatamente la posizione specifica quando si recano all'indirizzo civico. Questo nome di posizione può includere il numero di edificio, l'indicazione della scala, il numero del piano, il numero di porta e così via. Evitare nomi alternativi noti solo ai dipendenti, altrimenti si rischia che gli addetti del servizio di emergenza si rechino nel luogo sbagliato.

  - Un identificatore di posizione che consenta agli utenti di verificare facilmente che il proprio client Lync abbia selezionato la posizione corretta. Il client Lync concatena e visualizza automaticamente i campi **Location** e **City** rilevati nell'intestazione. È consigliabile aggiungere l'indirizzo dell'edificio a ogni identificatore di posizione, ad esempio "1° piano \<indirizzo\>"). Se non viene specificato l'indirizzo, un identificatore di posizione generico come "1° piano" potrebbe riferirsi a qualsiasi edificio della città.

  - Se la posizione è approssimativa perché è determinata da un punto di accesso wireless, è consigliabile aggiungere la parola Near Near, ad esempio "Near 1° piano 1234".

## Pianificazione dei numeri ELIN

Dopo aver stabilito come suddividere lo spazio dell'edificio in posizioni, è necessario decidere quanti numeri ELIN assegnare a ogni posizione. In un edificio a più piani o con più occupanti ad esempio è possibile assegnare alle diverse aree dell'edificio diverse zone di emergenza. In genere, ogni piano di un edificio viene designato come posizione. A ogni posizione vengono quindi assegnati uno o più numeri ELIN, utilizzati come numeri chiamanti durante una chiamata di emergenza. Contattare il gestore PSTN per conoscere i numeri di telefono che è possibile utilizzare come numeri ELIN. Nella tabella seguente sono illustrati alcuni esempi di posizioni per un indirizzo specifico.

### Posizioni e assegnazioni di numeri ELIN di esempio

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Area dell'edificio</th>
<th>Posizione</th>
<th>ELIN</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Primo piano</p></td>
<td><p>1</p></td>
<td><p>012 34 56 78</p></td>
</tr>
<tr class="even">
<td><p>Secondo piano</p></td>
<td><p>2</p></td>
<td><p>012 34 56 79</p></td>
</tr>
<tr class="odd">
<td><p>Terzo piano</p></td>
<td><p>3</p></td>
<td><p>012 34 56 80</p></td>
</tr>
</tbody>
</table>


Le posizioni definite devono soddisfare i requisiti seguenti:

  - Essere conformi alle disposizioni locali e nazionali/regionali in termini di area massima per posizione e numero di posizioni per indirizzo.

  - Essere sufficientemente specifiche da consentire di individuare senza difficoltà la persona che effettua la chiamata di emergenza.

## Popolamento del database delle posizioni

Le considerazioni seguenti possono essere utili per determinare come verrà popolato il database delle posizioni.

  - **Valutare quale processo verrà utilizzato per popolare il database delle posizioni.**  
    Esaminare dove si trovano i dati e quali operazioni è necessario eseguire per convertirli nel formato richiesto dal database delle posizioni. Considerare inoltre se le posizioni verranno aggiunte singolarmente o in gruppo tramite un file CSV.

<!-- end list -->

  - **Valutare se si dispone di un database di terze parti contenente già un mapping di posizioni.**  
    Utilizzando l'opzione del servizio Informazioni percorso secondario di Lync Server per connettersi a un database di terze parti, è possibile raggruppare e gestire le posizioni mediante una piattaforma offline. Uno dei vantaggi di questo approccio è che le posizioni possono essere associate non solo a identificatori di rete, ma anche a un utente. Questo significa che il servizio Informazioni percorso può restituire più indirizzi, derivanti dal servizio Informazioni percorso secondario, a un client Lync Server. L'utente può quindi scegliere la posizione più appropriata.
    
    Per l'integrazione con il servizio Informazioni percorso, il database di terze parti deve seguire lo schema di richiesta/risposta di posizione di Lync Server. Per informazioni dettagliate, vedere la pagina all'indirizzo <http://go.microsoft.com/fwlink/p/?linkid=213819>. Per informazioni dettagliate sulla distribuzione di un servizio Informazioni percorso secondario, vedere [Configurare un servizio Informazioni percorso secondario](lync-server-2013-configure-a-secondary-location-information-service.md) nella documentazione relativa alla distribuzione.

Per informazioni dettagliate su come popolare il database delle posizioni, vedere [Configurare il database delle posizioni in Lync Server 2013](lync-server-2013-configure-the-location-database.md) nella documentazione relativa alla distribuzione.

## Gestione del database delle posizioni

Dopo aver popolato il database delle posizioni, è necessario sviluppare una strategia per aggiornarlo in base alle modifiche di configurazione della rete. Le considerazioni seguenti possono essere utili per determinare come verrà gestito il database delle posizioni.

  - **Valutare come verrà aggiornato il database delle posizioni.**  
    Esistono diversi scenari che richiedono un aggiornamento del database delle posizioni, tra cui l'aggiunta di punti di accesso wireless, il ricablaggio degli uffici (con assegnazioni diverse dei commutatori) e l'espansione delle subnet. Considerare se si prevede di aggiornare direttamente ogni singola posizione o di eseguire un aggiornamento in blocco delle posizioni mediante un file CSV.

<!-- end list -->

  - **Considerare se verrà utilizzata un'applicazione SNMP per creare una corrispondenza tra gli indirizzi MAC dei client Lync e gli identificatori di porte e commutatori,**  
    Se si utilizza un'applicazione SNMP, è necessario sviluppare un processo manuale per mantenere la coerenza a livello di informazioni su porte e chassis dei commutatori tra l'applicazione SNMP e il database delle posizioni. Se l'applicazione SNMP restituisce un indirizzo IP o un ID porta di chassis non incluso nel database, il servizio Informazioni percorso non sarà in grado di restituire una posizione al client.

