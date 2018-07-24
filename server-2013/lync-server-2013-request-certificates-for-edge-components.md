---
title: 'Lync Server 2013: Richiedere i certificati per i componenti perimetrali'
TOCTitle: Richiedere i certificati per i componenti perimetrali
ms:assetid: 8c72b877-febc-428f-89dc-389e7a7ac849
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398708(v=OCS.15)
ms:contentKeyID: 49301267
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Richiedere i certificati per i componenti perimetrali in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-07_

I certificati necessari per supportare l'accesso utente esterno includono i certificati emessi da un'Autorità di certificazione (CA) pubblica e i certificati emessi da un'autorità di certificazione globale (enterprise) interna:

  - I certificati necessari per l'interfaccia esterna dei server perimetrale e il proxy inverso devono essere emessi da una CA pubblica.

  - I certificati necessari per l'interfaccia interna possono essere emessi da una CA pubblica o da una CA globale (enterprise) interna. È consigliabile utilizzare una CA interna di Windows Server 2008, Windows Server 2008 R2, Windows Server 2012 o Windows Server 2012 R2 per creare questi certificati, per risparmiare sui costi di utilizzo dei certificati pubblici.

> [!important]  
> L'elaborazione delle richieste di certificati può richiedere tempo, in particolare per le richiesta a CA pubbliche. È quindi consigliabile richiedere i certificati per i server perimetrali con sufficiente anticipo per assicurarsi che siano disponibili quando si inizia la distribuzione dei componenti dei server perimetrale. Per un riepilogo dei requisiti dei certificati per i server perimetrali, vedere <a href="lync-server-2013-certificate-requirements-for-external-user-access.md">Requisiti dei certificati per l'accesso utente esterno in Lync Server 2013</a>.

Anche se per il certificato del perimetro interno è possibile utilizzare un'autorità di certificazione (CA) pubblica, per ridurre al minimo i costi è consigliabile utilizzare una CA globale (enterprise). Per un riepilogo dei requisiti dei certificati per i server perimetrali, vedere [Requisiti dei certificati per l'accesso utente esterno in Lync Server 2013](lync-server-2013-certificate-requirements-for-external-user-access.md).


> [!NOTE]
> Il programma di installazione del server perimetrale include una procedura guidata di configurazione dei certificati che semplifica le attività di richiesta, assegnazione e installazione dei certificati, come illustrato nella sezione <A href="lync-server-2013-set-up-edge-certificates.md">Configurare i certificati perimetrali per Lync Server 2013</A>. Se si desidera richiedere i certificati prima di installare un server perimetrale, ad esempio per risparmiare tempo durante l'effettiva distribuzione dei componenti del server perimetrale, è possibile utilizzare a questo scopo i server interni, purché i certificati siano esportabili e contengano tutti i nomi alternativi del soggetto necessari. La presente documentazione non include le procedure per la richiesta dei certificati mediante i server interni.



## Richiedere certificati di una CA pubblica

La distribuzione di un server perimetrale richiede un singolo certificato pubblico per le interfacce esterne dei server perimetrali, che viene utilizzato per il servizio servizio Access Edge, il servizio servizio Web Conferencing Edge e per il servizio di autenticazione A/V. Tale certificato deve essere provvisto di una chiave privata esportabile, al fine di garantire che il servizio di autenticazione A/V utilizzi le stesse chiavi su tutti i server perimetrali di un pool. Anche il proxy inverso, che viene utilizzato con Microsoft Internet Security and Acceleration (ISA) Server 2006 o Microsoft Forefront Threat Management Gateway 2010, richiede un certificato pubblico.

## Richiedere certificati a una CA globale (enterprise) interna

I certificati necessari per l'interfaccia perimetrale interna possono essere rilasciati da un'Autorità di certificazione (CA) pubblica oppure interna. È possibile utilizzare una CA globale (enterprise) interna per ridurre al minimo il costo dei certificati. Se nell'organizzazione vi è una CA interna distribuita, i certificati per il perimetro interno devono essere rilasciati dalla CA interna. L'utilizzo di una CA globale (enterprise) interna per i certificati interni consente di ridurre il costo dei certificati.

Per un riepilogo dei requisiti dei certificati per i componenti perimetrali, vedere [Requisiti dei certificati per l'accesso utente esterno in Lync Server 2013](lync-server-2013-certificate-requirements-for-external-user-access.md). Per informazioni dettagliate sull'utilizzo di una CA pubblica per ottenere i certificati, vedere [Richiedere i certificati per i componenti perimetrali in Lync Server 2013](lync-server-2013-request-certificates-for-edge-components.md). Per informazioni dettagliate sulla richiesta, l'installazione e l'assegnazione di certificati, vedere [Configurare i certificati perimetrali per Lync Server 2013](lync-server-2013-set-up-edge-certificates.md).

