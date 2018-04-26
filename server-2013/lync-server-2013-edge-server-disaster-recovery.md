---
title: 'Lync Server 2013: Ripristino di emergenza dei server perimetrali'
TOCTitle: Ripristino di emergenza dei server perimetrali
ms:assetid: 05ec8d26-d167-4a6f-a966-a1f8873cf974
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ687960(v=OCS.15)
ms:contentKeyID: 49887432
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ripristino di emergenza dei server perimetrali in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-03-12_

Come per gli altri ruoli del server, il modo migliore per garantire la disponibilità elevata dei server perimetrali consiste nel distribuire più server perimetrali in pool in ogni sito. In caso di blocco di un server perimetrale, i servizi Edge verranno forniti dagli altri server del pool.

Per abilitare le procedure di ripristino di emergenza è necessario distribuire pool di server perimetrali distinti in siti separati. Non è necessario accoppiare esplicitamente i pool di server perimetrali come nel caso dei pool Front End, poiché la semplice presenza di più pool di server perimetrali consente di proseguire il lavoro anche in caso di blocco di un intero pool di server perimetrali. Nelle sezioni seguenti sono disponibili informazioni dettagliate sul ripristino di emergenza per le varie funzioni dei server perimetrali.

## Accesso remoto

Se sono presenti più siti, ognuno dei quali dispone di un pool di server perimetrali, e un intero pool di server perimetrali è in errore, i servizi di accesso remoto continueranno a funzionare senza bisogno di intervento da parte dell'amministratore. Quando si creano pool di server perimetrali in siti diversi, non è possibile usare lo stesso FQDN. A ogni pool di server perimetrali devono essere assegnati FQDN univoci (interni ed esterni). Per comunicare con i server Front End, i pool di server perimetrali non usano le regole di pubblicazione del proxy inverso. Quando il client esegue nuovamente la query relativa ai record del servizio DNS di accesso remoto e gli utenti remoti vengono instradati ai server perimetrali in un altro sito, si verifica il failover automatico. Il client prova a usare ogni FQDN di server perimetrale esterno in base alla priorità dei record SRV DNS.


> [!NOTE]
> Per garantire il corretto funzionamento del failover, assicurarsi che il firewall consenta ai server Front End di ogni pool di comunicare con tutti i server perimetrali.



## Federazione

Per le relazioni di federazione con altre organizzazioni che eseguono Lync Server, le richieste di federazione in ingresso continueranno a funzionare a patto che ogni pool di server perimetrali sia stato configurato con una priorità diversa nei record SRV. Verrà eseguito il failback di qualsiasi richiesta di federazione inviata a un pool di server perimetrali inattivo, che verrà quindi connessa a un pool di server perimetrali in esecuzione.

La federazione in uscita viene sempre configurata attraverso un server perimetrale o un pool di server perimetrali pubblicato nell'organizzazione. Se tale pool è inattivo, è necessario utilizzare il Generatore di topologie per modificare la route di federazione in ingresso in modo che venga utilizzato un pool di server perimetrali ancora in esecuzione. Per informazioni dettagliate, vedere [Failover del pool di server perimetrali utilizzato per la federazione di Lync Server in Lync Server 2013](lync-server-2013-failing-over-the-edge-pool-used-for-lync-server-federation.md)

## Federazione XMPP

Per la federazione XMPP, in caso di blocco del pool di server perimetrali designato come gateway XMPP si verificherà un errore sia nel traffico in ingresso che in quello in uscita. Per ripristinare il funzionamento della federazione XMPP è necessario modificarla in modo che venga utilizzato un pool di server perimetrali diverso. Per informazioni dettagliate, vedere [Failover del pool di server perimetrali utilizzato per la federazione di XMPP in Lync Server 2013](lync-server-2013-failing-over-the-edge-pool-used-for-xmpp-federation.md).

## Il pool di server perimetrali è in errore, ma il pool Front End è ancora in esecuzione

Se un pool di server perimetrali di un sito è in errore, ma il pool Front End dello stesso sito è ancora in esecuzione, sarà necessario modificare il pool Front End in modo che durante il periodo di non disponibilità del primo pool venga utilizzato un pool di server perimetrali diverso presso un altro sito. Per ulteriori informazioni, vedere [Modifica del pool di server perimetrali associato a un pool Front End in Lync Server 2013](lync-server-2013-changing-the-edge-pool-associated-with-a-front-end-pool.md).

