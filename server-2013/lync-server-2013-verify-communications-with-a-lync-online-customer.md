---
title: Verificare le comunicazioni con un cliente di Lync Online
TOCTitle: Verificare le comunicazioni con un cliente di Lync Online
ms:assetid: c8287b15-e1bb-4b26-8354-0ec90b2fcfe7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh202189(v=OCS.15)
ms:contentKeyID: 49301924
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verificare le comunicazioni con un cliente di Lync Online

 

_**Ultima modifica dell'argomento:** 2012-10-08_

Per consentire agli utenti di Lync nell'organizzazione di comunicare con gli utenti di un cliente di Microsoft Lync Online 2010, è necessario aver eseguito i passaggi seguenti:

  - Tutti i prerequisiti sono stati soddisfatti, inclusa la distribuzione dei server interni e perimetrali, l'abilitazione del supporto della federazione per l'organizzazione e l'impostazione degli account utente. Per informazioni dettagliate, vedere [Prerequisiti per la federazione con un cliente di Lync Online](lync-server-2013-prerequisites-for-federating-with-a-lync-online-customer.md).

  - Il supporto per l'accesso al dominio è stato configurato nella distribuzione interna. Questo prerequisito include la creazione di una voce per il provider host e la configurazione della distribuzione per consentire l'accesso dal dominio del cliente di Lync Online. Per informazioni dettagliate, vedere [Configurare il supporto della federazione per un dominio di Lync Online](lync-server-2013-configure-federation-support-for-a-lync-online-domain.md).

  - Gli account utente sono stati configurati per il supporto della federazione. Per informazioni dettagliate, vedere [Configurare l'accesso utente per la federazione con un cliente di Lync Online](lync-server-2013-configure-user-access-for-federation-with-a-lync-online-customer.md).

Al termine di tutti questi passaggi e dopo che l'amministratore del cliente di Lync Online 2010 ha eseguito tutte le operazioni di configurazione dei servizi online per il supporto della federazione con l'organizzazione, verificare le comunicazioni effettuando un test delle comunicazioni tra un utente interno all'organizzazione e un utente del cliente di Lync Online. Se la comunicazione non riesce, utilizzare lo strumento di registrazione del server perimetrale per acquisire i file di log e di traccia per la risoluzione del problema. Per informazioni dettagliate sull'utilizzo dello strumento di registrazione, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md) nella documentazione relativa alle operazioni. Per informazioni dettagliate sullo strumento di registrazione, vedere la documentazione relativa allo strumento di registrazione di Lync Server 2010 nella Libreria TechNet all'indirizzo [http://go.microsoft.com/fwlink/?linkid=199265\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=199265%26clcid=0x410).

