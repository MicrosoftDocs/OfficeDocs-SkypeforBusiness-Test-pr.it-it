---
title: Migrazione della federazione di XMPP
TOCTitle: Migrazione della federazione di XMPP
ms:assetid: b8d2b4b9-d0ed-4b48-820a-2c257fbdd2fb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721861(v=OCS.15)
ms:contentKeyID: 49887721
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Migrazione della federazione di XMPP

 

_**Ultima modifica dell'argomento:** 2012-10-19_

Nelle versioni precedenti di Lync Server e Office Communications Server è disponibile un gateway XMPP (Extensible Messaging and Presence Protocol) che può essere distribuito come ruolo del server separato per consentire la federazione con distribuzioni XMPP. In Lync Server 2013 la funzionalità XMPP può essere distribuita come caratteristica. La funzionalità XMPP viene installata in due parti, ovvero come proxy XMPP eseguito nel server perimetrale di Lync Server 2013 e come gateway XMPP eseguito nel Front End Server di Lync Server 2013.

Dal punto di vista della migrazione, un account utente di Lync Server può essere spostato in un pool di Lync Server 2013 e continuare a utilizzare il gateway XMPP legacy. Questo è possibile solo quando il partner federato XMPP non è configurato in Lync Server 2013.

Riepilogando, se Lync Server 2010 è stato distribuito con il gateway XMPP di Office Communications Server 2007 R2 e la federazione XMPP è stata abilitata per gli utenti di Lync Server 2010 legacy, per eseguire la migrazione della federazione XMPP in Lync Server 2013:

1.  Distribuire un pool di Lync Server 2013.

2.  Distribuire un server perimetrale di Lync Server 2013.

3.  Spostare tutti gli utenti nel pool di Lync Server 2013.

4.  Creare criteri di accesso XMPP e certificati per il server perimetrale.

5.  Abilitare la federazione XMPP in Lync Server 2013. 

6.  Aggiornare le voci DNS in modo che puntino al gateway XMPP di Lync Server 2013.

