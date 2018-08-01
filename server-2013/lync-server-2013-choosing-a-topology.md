---
title: 'Lync Server 2013: Scelta di una topologia'
TOCTitle: Scelta di una topologia
ms:assetid: 23f2aeb6-fed9-4349-8fba-dcbf18ee4b04
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425716(v=OCS.15)
ms:contentKeyID: 49299938
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Scelta di una topologia in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Quando si sceglie una topologia, è possibile utilizzare una delle opzioni di topologie supportate seguenti:


> [!NOTE]
> Se non diversamente specificato, chi ha esperienza in Microsoft Lync Server 2010 noterà che qui le linee guida sono in gran parte invariate.



  - [Singola topologia perimetrale consolidata con indirizzi IP privati e NAT in Lync Server 2013](lync-server-2013-single-consolidated-edge-with-private-ip-addresses-and-nat.md)

  - [Singola topologia perimetrale consolidata con indirizzi IP pubblici in Lync Server 2013](lync-server-2013-single-consolidated-edge-with-public-ip-addresses.md)

  - [Topologia perimetrale consolidata con scalabilità implementata, bilanciamento del carico DNS con indirizzi IP privati tramite NAT in Lync Server 2013](lync-server-2013-scaled-consolidated-edge-dns-load-balancing-with-private-ip-addresses-using-nat.md)

  - [Topologia perimetrale consolidata con scalabilità implementata, bilanciamento del carico DNS con indirizzi IP pubblici in Lync Server 2013](lync-server-2013-scaled-consolidated-edge-dns-load-balancing-with-public-ip-addresses.md)

  - [Topologia perimetrale consolidata con scalabilità implementata e servizi di bilanciamento del carico hardware in Lync Server 2013](lync-server-2013-scaled-consolidated-edge-with-hardware-load-balancers.md)

> [!IMPORTANT]  
> Per l'interfaccia perimetrale interna e per quella esterna è necessario utilizzare lo stesso tipo di bilanciamento del carico. Non è possibile utilizzare il bilanciamento del carico DNS in un'interfaccia perimetrale e il bilanciamento del carico hardware nell'altra.

Nella tabella riportata di seguito vengono riepilogate le funzionalità disponibili con le topologie di Microsoft Lync Server 2013 supportate. Le intestazioni di colonna indicano la funzionalità disponibile per una determinata opzione di configurazione di server perimetrale. Utilizzando come esempio l'opzione di server perimetrale con scalabilità implementata e con bilanciamento del carico DNS, è possibile osservare che supporta la disponibilità elevata, può utilizzare indirizzi IP privati non instradabili (con NAT) o indirizzi IP pubblici instradabili assegnati alle interfacce esterne perimetrali e comporta una riduzione dei costi perché non è necessario un dispositivo di bilanciamento del carico hardware.

Gli scenari di failover perimetrale supportati con il bilanciamento del carico DNS sono sessioni point-to-point da Lync a Lync, sessioni di conferenza di Lync e sessioni da Lync a PSTN e Office 365. Gli scenari di failover perimetrale che non usufruiscono del bilanciamento del carico DNS sono scenari di failover per Messaggistica unificata di Exchange dell'utente remoto (prima di Exchange 2010 SP1), la connettività per messaggistica istantanea pubblica e la federazione con server che eseguono Office Communications Server.

### Riepilogo delle opzioni di topologia di server perimetrali

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
<th>Topologia</th>
<th>Disponibilità elevata</th>
<th>Record A DNS aggiuntivi necessario per il server perimetrale esterno del pool di server perimetrali</th>
<th>Failover perimetrale per sessioni di federazione da Lync a Lync</th>
<th>Failover perimetrale per sessioni di federazione EUM/PIC/OCS da Lync a Lync</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Singolo perimetro con NAT</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Singolo perimetro con indirizzi IP pubblici</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Perimetro in scala (bilanciamento del carico DNS) con NAT</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>*</p></td>
</tr>
<tr class="even">
<td><p>Perimetro in scala (bilanciamento del carico DNS) con IP pubblico</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>*</p></td>
</tr>
<tr class="odd">
<td><p>Hardware perimetrale in scala (con bilanciamento del carico)</p></td>
<td><p>Sì</p></td>
<td><p>No (un record A DNS per IP virtuale)</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
</tbody>
</table>


**\*** Il failover per la connettività della messaggistica istantanea pubblica e la federazione con server che eseguono Office Communications Server non sono disponibili con il bilanciamento del carico DNS. Il failover di Messaggistica unificata di Exchange (utente remoto) con bilanciamento del carico DNS richiede Exchange Server 2010 SP1 o versione successiva.


> [!NOTE]
> Le topologie perimetrale singola e perimetrale in scala (con bilanciamento del carico DNS) possono utilizzare:<ul><li><p>Indirizzi IP pubblici instradabili</p></li><li><p>Indirizzo IP privato non instradabile se viene utilizzato il processo NAT (Network Address Translation) simmetrico</p>
>
> [!NOTE]
> Se si utilizza un indirizzo IP pubblico o un indirizzo IP privato con NAT, verrà utilizzato lo stesso numero di indirizzi IP in base alla configurazione scelta in Generatore di topologie. È possibile configurare il server perimetrale per utilizzare un unico indirizzo IP con porte distinte per servizio o utilizzare indirizzi IP distinti per servizio, ma utilizzare la stessa porta (per impostazione predefinita, TCP 443).
>
> </li></ul>
> Se si decide di utilizzare indirizzi IP privati non instradabili con NAT:<ul><li><p>È necessario utilizzare gli indirizzi IP privati instradabili in tutte e tre le interfacce esterne</p></li><li><p>È necessario configurare NAT simmetrico per il traffico in arrivo e in uscita</p></li></ul>
> La topologia perimetrale in scala (con bilanciamento del carico hardware) deve utilizzare indirizzi IP pubblici.


Lync Server 2013 supporta il posizionamento di interfacce esterne Access Edge, Web Conferencing Edge e A/V Edge dietro un router o un firewall che esegue NAT (Network Address Translation) per le topologie di server perimetrale consolidato sia singolo che con scalabilità implementata.

L'utilizzo di NAT per tutte le interfacce esterne perimetrali richiede l'utilizzo del bilanciamento del carico DNS. In confronto all'utilizzo di un dispositivo di bilanciamento del carico hardware, il bilanciamento del carico DNS senza NAT consente di ridurre il numero di indirizzi IP pubblici per server perimetrale in un pool di server perimetrali, come descritto nell'elenco seguente:

  - La topologia di server perimetrale consolidato con scalabilità implementata Lync Server 2013 (con bilanciamento del carico DNS) richiede tre indirizzi IP pubblici per ogni server perimetrale di un pool di server perimetrali.

  - La topologia di server perimetrale consolidato con scalabilità implementata Lync Server 2013 (con bilanciamento del carico hardware) richiede tre indirizzi IP pubblici per gli indirizzi IP virtuali di bilanciamento del carico (requisito applicato una sola volta che non viene riapplicato con l'aggiunta di server perimetrali nel pool) e tre indirizzi IP pubblici per server perimetrale in un pool.

### Requisiti di indirizzi IP per topologie di server perimetrali consolidati con scalabilità implementata (indirizzo IP per ruolo)

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Numero di server perimetrali per pool</th>
<th>Numero di indirizzi IP obbligatori Lync Server 2013 (con bilanciamento del carico DNS)</th>
<th>Numero di indirizzi IP obbligatori Lync Server 2013 (con bilanciamento del carico hardware)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>2</p></td>
<td><p>6</p></td>
<td><p>3 (1 per IP virtuale) + 6</p></td>
</tr>
<tr class="even">
<td><p>3</p></td>
<td><p>9</p></td>
<td><p>3 (1 per IP virtuale) + 6</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>3 (1 per IP virtuale) + 6</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p>15</p></td>
<td><p>3 (1 per IP virtuale) + 6</p></td>
</tr>
</tbody>
</table>


### Requisiti di indirizzi IP per topologie di server perimetrali consolidati con scalabilità implementata (singolo indirizzo IP per tutti i ruoli)

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Numero di server perimetrali per pool</th>
<th>Numero di indirizzi IP obbligatori Lync Server 2013 (con bilanciamento del carico DNS)</th>
<th>Numero di indirizzi IP obbligatori Lync Server 2013 (con bilanciamento del carico hardware)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>2</p></td>
<td><p>2</p></td>
<td><p>2 (1 per IP virtuale) + 6</p></td>
</tr>
<tr class="even">
<td><p>3</p></td>
<td><p>3</p></td>
<td><p>3 (1 per IP virtuale) + 6</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>4</p></td>
<td><p>4 (1 per IP virtuale) + 6</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p>5</p></td>
<td><p>5 (1 per IP virtuale) + 6</p></td>
</tr>
</tbody>
</table>


Gli aspetti principali di cui tenere conto per la scelta della topologia sono la disponibilità elevata e il bilanciamento del carico. Il requisito di disponibilità elevata può influire sulla scelta del bilanciamento del carico.

  - **Disponibilità elevata**   Se si desidera una disponibilità elevata, distribuire almeno due server perimetrali in un pool. Un singolo pool di server perimetrali supporterà fino a dodici server perimetrali. Se è necessaria ulteriore capacità, è possibile distribuire più pool di server perimetrali. Come regola generale, il 10% del numero totale di utenti necessiterà dell'accesso esterno.
    
    > [!IMPORTANT]  
    > Generatore di topologie consentirà di configurare fino a venti server perimetrali in un unico pool di server perimetrali. Il numero massimo verificato di server perimetrali in un pool è dodici e il Generatore di topologie che consente un numero superiore a dodici non deve essere interpretato come supporto implicito per più di dodici server perimetrali in un unico pool di server perimetrali.

  - **Bilanciamento del carico hardware**   Il bilanciamento del carico hardware è supportato per il bilanciamento del carico di server perimetrali  Lync Server 2013 quando si utilizzano indirizzi IP pubblicamente instradabili per le interfacce esterne perimetrali. Utilizzare ad esempio questo approccio in situazioni in cui è necessario il failover per le applicazioni seguenti:
    
      - Connettività per messaggistica istantanea pubblica
    
      - Federazione con società che utilizzano Microsoft Office Communications Server 2007 o Microsoft Office Communications Server 2007 R2
    
      - Accesso esterno a Messaggistica unificata di Exchange 2007 o di Exchange 2010
        
        > [!IMPORTANT]  
        > Il bilanciamento del carico DNS per Exchange 2010 SP1 e versioni successive è supportato per Messaggistica unificata di Exchange.    
    Queste tre applicazioni continueranno a funzionare, ma non supportano il bilanciamento del carico DNS e si connetteranno solo al primo server perimetrale del pool. Se il server non è disponibile, la connessione avrà esito negativo. Se ad esempio vengono distribuiti più server perimetrali in un pool per gestire il carico del traffico federato, solo un proxy di accesso riceverà effettivamente il traffico, mentre gli altri resteranno inattivi.

> [!IMPORTANT]  
> L'utilizzo del bilanciamento del carico DNS è consigliato se si attua una federazione con società che utilizzano Lync Server 2010 e Microsoft Office 365. Considerare che gli effetti sulle prestazioni saranno significativi se la maggior parte dei partner federati utilizza Office Communications Server 2007 oppure Office Communications Server 2007 R2.
