---
title: Migrazione della federazione di XMPP
TOCTitle: Migrazione della federazione di XMPP
ms:assetid: 7368ee8f-a201-4d3a-b4e8-68396b156d4d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688093(v=OCS.15)
ms:contentKeyID: 49887607
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Migrazione della federazione di XMPP

 

_**Ultima modifica dell'argomento:** 2012-10-16_

Le versioni precedenti di Office Communications Server offrono un gateway XMPP (Extensible Messaging and Presence Protocol) distribuibile come ruolo del server separato per consentire la federazione con le distribuzioni XMPP. In Lync Server 2013, la funzionalità XMPP può essere distribuita come funzionalità. La funzionalità XMPP è installata in due parti: come proxy XMPP eseguito sul server perimetrale di Lync Server 2013, e come gateway XMPP eseguito sul Front End Server di Lync Server 2013.

Da una prospettiva di migrazione, è possibile spostare un account utente di Office Communications Server 2007 R2 in un pool di Lync Server 2013 e continuare a utilizzare il gateway XMPP di Office Communications Server 2007 R2. Ciò risulta possibile sono quando il partner XMPP federato non è configurato in Lync Server 2013.

Riepilogando, se Office Communications Server è stato distribuito con il gateway XMPP di Office Communications Server 2007 R2 e la federazione XMPP è stata abilitata per gli utenti di Office Communications Server 2007 R2 legacy, per eseguire la migrazione della federazione XMPP in Lync Server 2013:

1.  Distribuire un pool di Lync Server 2013.

2.  Distribuire un server perimetrale di Lync Server 2013.

3.  Spostando tutti gli utenti al pool di Lync Server 2013.

4.  Creare criteri di accesso XMPP e certificati per il server perimetrale.

5.  Abilitare la federazione XMPP in Lync Server 2013. 

6.  Aggiornare le voci DNS in modo che puntino al gateway XMPP di Lync Server 2013.

