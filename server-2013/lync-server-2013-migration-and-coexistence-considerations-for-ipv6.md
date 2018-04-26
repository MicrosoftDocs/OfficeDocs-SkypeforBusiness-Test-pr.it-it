---
title: 'Lync Server 2013: Considerazioni sulla migrazione e la coesistenza per IPv6'
TOCTitle: Considerazioni sulla migrazione e la coesistenza per IPv6
ms:assetid: 8c769c4f-c8a9-4cbf-9080-beee3be9848a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205068(v=OCS.15)
ms:contentKeyID: 49301258
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Considerazioni sulla migrazione e la coesistenza per IPv6 in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-06-14_

IPv6 (IP versione 6) non è supportato su Lync Server 2010 o Office Communications Server. Per progetti pilota è possibile testare la coesistenza del dual stack di Lync Server 2010 e Lync Server 2013. È consigliabile che tutti i pool di un determinato sito centrale vengano aggiornati a Lync Server 2013 prima di abilitare IPv6 (rete dual stack) per tutti i pool. Se è necessario configurare un pool solo per IPv6, è consigliabile configurare un pool solo IPv6 nell'ambiente di prova a fini di test.

Durante la migrazione e in caso di coesistenza sono supportati gli scenari seguenti:

  - Pool di Lync Server 2013, Lync Server 2010 e Office Communications Server 2007 R2 in modalità IPv4 coesistenti con Lync Server 2013 in modalità dual stack.

  - Pool di Lync Server 2013 in modalità solo IPv6, se isolato.

