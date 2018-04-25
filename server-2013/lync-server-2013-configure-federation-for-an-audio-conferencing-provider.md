---
title: 'Lync Server 2013: Configurare la federazione per un provider di audioconferenze'
TOCTitle: Configurare la federazione per un provider di audioconferenze
ms:assetid: 08dedcce-0d3f-45da-8282-cf2634a41665
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn510996(v=OCS.15)
ms:contentKeyID: 59954063
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare la federazione per un provider di audioconferenze in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-07-24_

Se si desidera utilizzare un provider di servizi di audioconferenza nella distribuzione ibrida (Lync Server in locale con Lync Online), è necessario configurare la federazione tra la distribuzione di Lync in locale e il partner provider di servizi di audioconferenza come server partner consentito. È possibile configurare la federazione aggiungendo il dominio del partner provider di servizi di audioconferenza e il server perimetrale (definito anche proxy di accesso) all'elenco dei domini federati per la distribuzione locale. Il partner provider di servizi di audioconferenza richiederà dunque di aggiungere l'FQDN del pool di server perimetrali locale al proprio elenco di domini federati consentiti. Per ulteriori dettagli contattare il provider di servizi di audioconferenza.

  - **Aggiunta del dominio del provider di servizi di audioconferenza e del server perimetrale come dominio federato consentito**
    
    Per aggiungere il dominio del provider di servizi di audioconferenza come server partner consentito (dominio federato consentito), seguire i passaggi indicati in [Configurare il supporto per i domini esterni consentiti in Lync Server 2013](lync-server-2013-configure-support-for-allowed-external-domains.md). Per il server perimetrale, aggiungere l'FQDN del server perimetrale del partner provider di servizi di audioconferenza. Potrebbe essere necessario contattare il partner provider di servizi di audioconferenza per ottenere l'FQDN del relativo server perimetrale, che potrebbe essere definito anche proxy di accesso dal partner.

  - **Fornire l'FQDN del pool di server perimetrali al partner provider di servizi di audioconferenza**
    
    È necessario che il partner provider di servizi di audioconferenza configuri la federazione per aggiungere il dominio locale dell'utente come server partner consentito aggiungendo l'FQDN del pool di server perimetrali come dominio federato consentito.

