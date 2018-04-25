---
title: 'Lync Server 2013: Supporto di Active Directory'
TOCTitle: Supporto di Active Directory
ms:assetid: 28ed9ac4-586d-4803-ad45-99c4fa793f54
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425756(v=OCS.15)
ms:contentKeyID: 49299998
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supporto di Active Directory in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-12-04_

Le topologie locali dei Servizi di dominio Active Directory supportate da Lync Server 2013 sono:

  - Foresta singola con singolo dominio

  - Foresta singola con albero singolo e più domini

  - Foresta singola con più alberi e spazi dei nomi disgiunti

  - Più foreste in una topologia di foreste centralizzate

  - Più foreste in una topologia di foresta di risorse


> [!NOTE]
> Lync Server 2013 non supporta domini con etichetta singola. Ad esempio è supportata una foresta con un dominio radice denominato <STRONG>contoso.local</STRONG>, ma non è supportato un dominio radice con etichetta singola denominato <STRONG>local</STRONG>. Per informazioni dettagliate, vedere l'articolo 300684 della Microsoft Knowledge Base "Informazioni sulla configurazione di Windows per domini con nomi DNS con etichetta singola", all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=143752">http://go.microsoft.com/fwlink/p/?linkId=143752</A>.




> [!NOTE]
> Lync Server 2013 non supporta la ridenominazione dei domini. Per rinominare un dominio in cui è distribuito Lync Server, è innanzitutto necessario disinstallare Lync Server, quindi rinominare il dominio e infine reinstallare Lync Server.



Per informazioni dettagliate sulle topologie supportate e sui requisiti per le distribuzioni locali, vedere [Requisiti, supporto e topologie di Servizi di dominio Active Directory in Lync Server 2013](lync-server-2013-active-directory-domain-services-requirements-support-and-topologies.md) nella documentazione relativa alla pianificazione.

