---
title: 'Lync Server 2013: Configurare le interfacce di rete per i server perimetrali'
TOCTitle: Configurare le interfacce di rete per i server perimetrali
ms:assetid: b0aecdf6-4ae2-46f6-b9b6-948bfc3df11e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412847(v=OCS.15)
ms:contentKeyID: 49301680
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare le interfacce di rete per i server perimetrali in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-08_

Ogni Edge Server è un computer multihomed con interfacce rivolte verso l'esterno e verso l'interno. Le impostazioni DNS (Domain Name System ) della scheda dipendono dalla presenza di server DNS nella rete perimetrale. Se nel perimetro sono presenti server DNS, devono disporre di un'area contenente uno o più record A DNS per il server hop successivo o per il pool (ovvero un pool Director o un pool Front End designato) e per query esterne che per le ricerche dei nomi fanno riferimento ad altri server DNS pubblici. Se nel perimetro non sono presenti server DNS, il server o i server Edge Server utilizzeranno i server DNS esterni per risolvere le ricerche dei nomi Internet e ogni Edge Server utilizzerà un HOST per risolvere i nomi di server hop successivo in indirizzi IP.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398321.security(OCS.15).gif" title="security" alt="security" />SicurezzaNota:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Per motivi di protezione, è consigliabile non consentire agli Edge Server di accedere a un server DNS presente nella rete interna.</td>
</tr>
</tbody>
</table>

## Per configurare le interfacce con i server DNS nella rete perimetrale

1.  Installare due schede di rete per ogni Edge Server, una per l'interfaccia connessa alla rete interna e una per quella connessa alla rete esterna.
    
    > [!IMPORTANT]  
    > Le subnet interna ed esterna non devono essere vicendevolmente instradabili.

2.  Nell'interfaccia esterna configurare tre indirizzi IP statici nella subnet della rete perimetrale esterna, denominata anche DMZ o subnet schermata, e puntare il gateway predefinito all'interfaccia interna del firewall esterno. Configurare le impostazioni DNS della scheda in modo da puntare a una coppia di server DNS perimetrali.
    

    > [!NOTE]
    > È possibile utilizzare anche un solo indirizzo IP per questa interfaccia, ma a tale scopo sarà necessario modificare le assegnazioni delle porte con valori non standard. Definire la modalità da utilizzare quando si crea la topologia in Generatore di topologie.



3.  Nell'interfaccia interna, configurare un indirizzo IP statico nella subnet della rete perimetrale interna e non impostare un gateway predefinito. Configurare le impostazioni DNS della scheda in modo da puntare ad almeno un server DNS, preferibilmente una coppia di server DNS perimetrali.

4.  Creare route statiche persistenti nell'interfaccia interna a tutte le reti interne in cui risiedono client, Lync Server 2013 e server di messaggistica unificata di Exchange.

## Per configurare le interfacce senza server DNS nella rete perimetrale

1.  Installare due schede di rete per ogni Edge Server, una per l'interfaccia connessa alla rete interna e una per quella connessa alla rete esterna.
    
    > [!IMPORTANT]  
    > Le subnet interna ed esterna non devono essere vicendevolmente instradabili.

2.  Nell'interfaccia esterna configurare tre indirizzi IP statici nella subnet della rete perimetrale esterna. È inoltre possibile configurare il gateway predefinito nell'interfaccia esterna. Ad esempio, definire il router con connessione Internet o il firewall esterno come gateway predefinito. Configurare le impostazioni DNS in modo da puntare a un server DNS, preferibilmente a una coppia di server DNS esterni.
    

    > [!NOTE]
    > È possibile, ma non consigliabile, utilizzare anche un solo indirizzo IP per l'interfaccia esterna. A tale scopo, è necessario impostare le assegnazioni delle porte su valori non standard e lontani dalla porta predefinita 443 che in genere è appropriata per il firewall per la comunicazione client. Definire l'impostazione dell'indirizzo IP e le impostazioni delle porte quando si crea la topologia in Generatore di topologie.



3.  Nell'interfaccia interna, configurare un indirizzo IP statico nella subnet della rete perimetrale interna e non impostare un gateway predefinito. Lasciare le impostazioni DNS della scheda vuote.

4.  Creare route statiche persistenti nell'interfaccia interna a tutte le reti interne in cui risiedono client Lync o server che eseguono Lync Server 2013.

5.  Modificare il file HOST in ogni Edge Server in modo da contenere un record per il server dell'hop successivo o l'IP virtuale (VIP). Il record sarà il server Director, il server Standard Edition o un pool Front End configurato come indirizzo dell'hop successivo di Edge Server in Generatore di topologie. Se si utilizza il bilanciamento del carico DNS, includere una riga per ogni membro del pool dell'hop successivo.

