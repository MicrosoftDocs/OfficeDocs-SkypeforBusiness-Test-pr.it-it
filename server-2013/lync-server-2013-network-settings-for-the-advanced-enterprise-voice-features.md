---
title: "Lync Server 2013: Impostazioni di rete per funzioni VoIP aziendale avanzate"
TOCTitle: Impostazioni di rete per le funzionalità di VoIP aziendale avanzate
ms:assetid: 7f6de9e4-c8a4-44e4-8d14-21fe8c45283a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398637(v=OCS.15)
ms:contentKeyID: 49301122
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Impostazioni di rete per le funzionalità di VoIP aziendale avanzate in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-10_

In Lync Server sono disponibili tre caratteristiche avanzate di VoIP aziendale: il servizio Controllo di ammissione di chiamata, i servizi di emergenza (E9-1-1) e la possibilità di ignorare Mediation Server (Media Bypass). Queste caratteristiche condividono alcuni requisiti di configurazione per le aree di rete, i siti di rete e l'associazione di ogni subnet nella topologia di Lync Server con un sito di rete. Per informazioni dettagliate sulla pianificazione della distribuzione di queste caratteristiche, vedere:

  - [Pianificazione del servizio Controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-planning-for-call-admission-control.md)

  - [Pianificazione per i servizi di emergenza (E9-1-1) in Lync Server 2013](lync-server-2013-planning-for-emergency-services-e9-1-1.md)

  - [Pianificazione del bypass multimediale in Lync Server 2013](lync-server-2013-planning-for-media-bypass.md)

Per informazioni dettagliate sulla distribuzione di ognuna di queste caratteristiche, vedere [Distribuzione delle funzionalità di VoIP aziendale avanzate in Lync Server 2013](lync-server-2013-deploying-advanced-enterprise-voice-features.md) nella documentazione relativa alla distribuzione.

In questo argomento viene fornita una panoramica dei requisiti di configurazione comuni a tutti e tre le caratteristiche avanzate di VoIP aziendale.

## Aree di rete

Un'area di rete è un hub o un backbone di rete utilizzato solo nella configurazione dei servizi Controllo di ammissione di chiamata, E9-1-1 e Media Bypass.


> [!NOTE]
> Le aree di rete non corrispondono alle aree di conferenza telefonica con accesso esterno di Lync Server, che sono necessarie per associare i numeri di accesso alla conferenza telefonica con accesso esterno con uno o più dial plan di Lync Server. Per ulteriori informazioni sulle aree di conferenza telefonica con accesso esterno, vedere <A href="lync-server-2013-dial-in-conferencing-requirements.md">Requisiti delle conferenze telefoniche con accesso esterno in Lync Server 2013</A> nella documentazione relativa alla pianificazione.



Il servizio Controllo di ammissione di chiamata richiede che a ogni area di rete sia associato un sito centrale di Lync Server, che gestisce il traffico multimediale all'interno dell'area (ovvero prende decisioni in base ai criteri configurati per consentire o meno di stabilire una sessione audio o video in tempo reale). I siti centrali di Lync Server non rappresentano posizioni geografiche, ma piuttosto gruppi logici di server configurati come un pool o un insieme di pool. Per ulteriori informazioni sui siti centrali, vedere [Topologie di riferimento in Lync Server 2013](lync-server-2013-reference-topologies.md) nella documentazione relativa alla pianificazione. Vedere inoltre [Topologie supportate in Lync Server 2013](lync-server-2013-supported-topologies.md) nella documentazione relativa al supporto.

Per configurare un'area di rete, è possibile utilizzare la scheda **Aree** della sezione **Configurazione di rete** del Pannello di controllo di Lync Server, oppure eseguire il cmdlet **New-CsNetworkRegion** o **Set-CsNetworkRegion**Lync Server Management Shell. Per informazioni, vedere [Creare o modificare un'area di rete in Lync Server 2013](lync-server-2013-create-or-modify-a-network-region.md) nella documentazione relativa alla distribuzione oppure fare riferimento alla documentazione di Lync Server Management Shell.

Le stesse definizioni di area di rete sono condivise da tutte e tre le caratteristiche avanzate di VoIP aziendale. Se sono già state create aree di rete per una caratteristica, non è necessario creare nuove aree di rete per le altre caratteristiche. Potrebbe tuttavia essere necessario modificare una definizione di area di rete esistente per applicare impostazioni specifiche della caratteristica. Se, ad esempio, sono state create aree di rete per il servizio E9-1-1 (che non richiede un sito centrale associato) e successivamente si distribuisce il servizio Controllo di ammissione di chiamata, è necessario modificare ognuna delle definizioni di area di rete per specificare un sito centrale.

Per associare un sito centrale di Lync Server a un'area di rete, è necessario specificare il nome del sito centrale, utilizzando la sezione **Configurazione di rete** del Pannello di controllo di Lync Server, o eseguendo il cmdlet **New-CsNetworkRegion** o **Set-CsNetworkRegion**Lync Server Management Shell. Per informazioni, vedere [Creare o modificare un'area di rete in Lync Server 2013](lync-server-2013-create-or-modify-a-network-region.md) nella documentazione relativa alla distribuzione oppure fare riferimento alla documentazione di Lync Server Management Shell.

## Siti di rete

Un sito di rete rappresenta una posizione geografica, ad esempio una succursale, una filiale o la sede principale. Ogni sito di rete deve essere associato a un'area di rete specifica.


> [!NOTE]
> I siti di rete vengono utilizzati solo dalle caratteristiche avanzate di VoIP aziendale. Non corrispondono ai siti derivati che è possibile configurare nella topologia di Lync Server. Per informazioni dettagliate sui siti derivati, vedere <A href="lync-server-2013-reference-topologies.md">Topologie di riferimento in Lync Server 2013</A> nella documentazione relativa alla pianificazione. Vedere inoltre <A href="lync-server-2013-supported-topologies.md">Topologie supportate in Lync Server 2013</A> nella documentazione relativa al supporto.



Per configurare un sito di rete e associarlo a un'area di rete, è possibile utilizzare la sezione **Configurazione di rete** del Pannello di controllo di Lync Server, oppure eseguire il cmdlet Lync Server Management Shell**New-CsNetworkSite** o **Set-CsNetworkSite**. Per informazioni, vedere [Creare o modificare un sito di rete in Lync Server 2013](lync-server-2013-create-or-modify-a-network-site.md) nella documentazione relativa alla distribuzione oppure fare riferimento alla documentazione di Lync Server Management Shell.

## Identificare le subnet IP

Per ogni sito di rete sarà necessario collaborare con l'amministratore di rete per stabilire quali subnet IP sono assegnate a ogni sito di rete. Se l'amministratore di rete ha già organizzato le subnet IP in aree di rete e siti di rete, il lavoro risulterà notevolmente semplificato.

In questo esempio, al sito New York nell'area Nord America sono assegnate le subnet IP seguenti: 172.29.80.0/23, 157.57.216.0/25, 172.29.91.0/23, 172.29.81.0/24. Si supponga che Bob, che di solito lavora a Detroit, si sposti nell'ufficio di New York per un corso di formazione. Quando accende il suo computer e si connette alla rete, al computer verrà assegnato un indirizzo IP in uno dei quattro intervalli allocati a New York, ad esempio 172.29.80.103.


> [!WARNING]
> Le subnet IP specificate durante la configurazione della rete nel server devono corrispondere al formato specificato dai computer client per poter essere utilizzate correttamente per Media Bypass. Un client Lync accetta l'indirizzo IP locale e lo maschera con la subnet mask associata. Durante la determinazione dell'ID bypass associato a ogni client, tramite la funzione di registrazione viene confrontato l'elenco delle subnet IP associate a ogni sito di rete con la subnet fornita dal client per individuare una corrispondenza esatta. Per questo motivo, è importante che le subnet immesse durante la configurazione della rete nel server siano subnet effettive, anziché virtuali. Se si implementa il servizio Controllo di ammissione di chiamata ma non Media Bypass, il servizio Controllo di ammissione di chiamata funzionerà in modo corretto anche se si configurano subnet virtuali.<BR>Se un client di Lync accede a un computer con indirizzo IP 172.29.81.57 e una subnet mask IP 255.255.255.0, ad esempio, richiederà l'ID bypass associato alla subnet 172.29.81.0. Se la subnet è definita come 172.29.0.0/16, anche se il client appartiene alla subnet virtuale, la funzione di registrazione non la considererà una corrispondenza esatta perché cerca nello specifico la subnet 172.29.81.0. È pertanto importante che l'amministratore immetta le subnet esattamente come vengono fornite dai client di Lync, per i quali il provisioning delle subnet viene eseguito durante la configurazione della rete in modo statico o tramite DHCP.)



## Associazione di subnet a siti di rete

Ogni subnet della rete aziendale deve essere associata a un sito di rete (ovvero ogni subnet deve essere associata a una posizione geografica). Questa associazione di subnet consente alle caratteristiche avanzate di VoIP aziendale di individuare geograficamente gli endpoint in modo efficace. L'individuazione degli endpoint consente, ad esempio, al servizio Controllo di ammissione di chiamata di regolare il flusso di dati audio e video in tempo reale da e verso il sito di rete.

Per associare le subnet ai siti di rete, è possibile utilizzare la sezione **Configurazione di rete** del Pannello di controllo di Lync Server oppure eseguire il Lync Server Management Shell. Per informazioni, vedere [Associare una subnet a un sito di rete in Lync Server 2013](lync-server-2013-associate-a-subnet-with-a-network-site.md) nella documentazione relativa alla distribuzione oppure fare riferimento alla documentazione di Lync Server Management Shell.

## Vedere anche

#### Ulteriori risorse

[Pianificazione del servizio Controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-planning-for-call-admission-control.md)  
[Pianificazione per i servizi di emergenza (E9-1-1) in Lync Server 2013](lync-server-2013-planning-for-emergency-services-e9-1-1.md)  
[Pianificazione del bypass multimediale in Lync Server 2013](lync-server-2013-planning-for-media-bypass.md)

