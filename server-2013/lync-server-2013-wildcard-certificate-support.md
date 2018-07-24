---
title: 'Lync Server 2013: Supporto dei certificati con caratteri jolly'
TOCTitle: Supporto dei certificati con caratteri jolly
ms:assetid: 0bae2aa8-b6dc-46f5-a3be-3fe7581809d4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh202161(v=OCS.15)
ms:contentKeyID: 49299649
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supporto dei certificati con caratteri jolly in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-03-21_

Lync Server 2013 utilizza i certificati per garantire la crittografia delle comunicazioni e l'autenticazione dell'identità del server. In alcuni casi, ad esempio per la pubblicazione Web tramite il proxy inverso, non è necessaria la corrispondenza esatta tra la voce di nome alternativo del soggetto e il nome di dominio completo (FQDN) del server che presenta il servizio. In questi casi è possibile utilizzare certificati con voci di nome alternativo del soggetto con caratteri jolly, comunemente noti come "certificati con caratteri jolly", per ridurre il costo di un certificato richiesto a un'autorità di certificazione pubblica e per semplificare il processo di pianificazione per i certificati.


> [!WARNING]
> Per mantenere la funzionalità dei dispositivi per le comunicazioni unificate, quali ad esempio i telefoni da tavolo, è necessario verificare attentamente il certificato distribuito per assicurarsi che i dispositivi funzionino correttamente dopo l'implementazione di un certificato con caratteri jolly.



Non viene fornito il supporto per una voce con caratteri jolly come nome soggetto, ovvero come nome comune o CN, per alcun ruolo. Quando si utilizzano voci con caratteri jolly nel nome alternativo del soggetto, sono supportati i ruoli del server seguenti:

   **Proxy inverso.**   La voce SAN con caratteri jolly è supportata per il certificato di pubblicazione con un URL semplice (Meet e Dialin).  

   **Proxy inverso.**   La voce SAN con caratteri jolly è supportata per le voci SAN per LyncDiscover nel certificato di pubblicazione.  

   **Director.**   La voce SAN con caratteri jolly è supportata per gli URL semplici (Meet e Dialin) e per le voci SAN per LyncDiscover e LyncDiscoverInternal nei componenti Web di Director.  

   **Front End Server ( Standard Edition) e pool Front End ( Enterprise Edition).** La voce SAN con caratteri jolly è supportata per gli URL semplici (Meet e Dialin) e per le voci SAN per LyncDiscover e LyncDiscoverInternal nei componenti Web Front End.  

   **Messaggistica unificata di Exchange.**   Il server non utilizza voci di nome alternativo del soggetto quando viene distribuito come server autonomo.  

   **Server Accesso client di Microsoft Exchange Server.**   Le voci con caratteri jolly nel nome SAN sono supportate per i client interni ed esterni.  

   **Messaggistica unificata di Exchange e server Accesso client di Microsoft Exchange Server nello stesso server.**   Le voci di nome alternativo del soggetto con caratteri jolly sono supportate.  

In questo argomento non vengono trattati i ruoli del server seguenti:

  - Ruoli del server interni, inclusi in via esemplificativa Mediation Server, Server di archiviazione e Monitoring Server, Survivable Branch Appliance o Survivable Branch Server

  - Interfacce dei server perimetrali ( server perimetrale) esterni

  - Server perimetrale ( server perimetrale) interno
    

    > [!NOTE]
    > Per l'interfaccia del server perimetrale ( server perimetrale) interno, una voce con caratteri jolly può essere assegnata al nome alternativo del soggetto ed è supportata. Il nome alternativo del soggetto nel server perimetrale ( server perimetrale) interno non viene sottoposto a query e una voce di nome alternativo del soggetto con caratteri jolly ha un valore limitato.



Per informazioni dettagliate sulle configurazioni dei certificati, compreso l'uso dei caratteri jolly nei certificati, vedere gli argomenti seguenti:

  - [Requisiti dei certificati per i server interni in Lync Server 2013](lync-server-2013-certificate-requirements-for-internal-servers.md)

  - [Requisiti dei certificati per l'accesso utente esterno in Lync Server 2013](lync-server-2013-certificate-requirements-for-external-user-access.md)

  - [Riepilogo dei certificati - bilanciamento del carico DNS e bilanciamento del carico hardware in Lync Server 2013](lync-server-2013-certificate-summary-dns-and-hlb-load-balanced.md)

  - [Riepilogo dei certificati - singolo server Director in Lync Server 2013](lync-server-2013-certificate-summary-single-director.md)

  - [Riepilogo dei certificati - pool di server Director con scalabilità implementata, servizio di bilanciamento del carico hardware in Lync Server 2013](lync-server-2013-certificate-summary-scaled-director-pool-hardware-load-balancer.md)

  - [Riepilogo dei certificati - proxy inverso in Lync Server 2013](lync-server-2013-certificate-summary-reverse-proxy.md)

  - [Linee guida per l'integrazione della messaggistica unificata locale con Lync Server 2013](lync-server-2013-guidelines-for-integrating-on-premises-unified-messaging.md)

Per informazioni dettagliate sulla configurazione dei certificati per Exchange, compreso l'uso dei caratteri jolly, vedere la documento del prodotto Exchange 2013.

