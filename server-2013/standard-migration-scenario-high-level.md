---
title: Scenario di migrazione standard - informazioni generali
TOCTitle: Scenario di migrazione standard - informazioni generali
ms:assetid: e768a7ca-44e3-4969-a6d9-7ed3e7029c5c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205354(v=OCS.15)
ms:contentKeyID: 49302296
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Scenario di migrazione standard - informazioni generali

 

_**Ultima modifica dell'argomento:** 2013-01-30_

Utilizzare gli elementi seguenti come punto di partenza per la migrazione di Lync Server 2010, Group Chat o Office Communications Server 2007 R2Group Chat al server Chat persistente di Lync Server 2013. Il percorso di migrazione standard per Lync Server 2013 è il seguente:

  - L'organizzazione ha distribuito in precedenza Lync Server 2010, Group Chat o Office Communications Server 2007 R2Group Chat e desidera distribuire il server Chat persistente di Lync Server 2013.

  - Distribuire Lync Server 2013 e quindi distribuire pool di server Chat persistente.

  - Preparare e pianificare la migrazione delle chat room di Chat persistente e determinare il momento appropriato per disattivare il sistema per la migrazione.

  - Eseguire i cmdlet di Windows PowerShell per la migrazione (**Export-CsPersistentChatData** e **Import-CsPersistentChatData**) per spostare il contenuto nel server Chat persistente.

  - Verificare la corretta esecuzione della migrazione.

  - Rimuovere la distribuzione legacy,

  - Configurare server Chat persistente in modo che i client legacy possano connettersi al server Chat persistente di Lync Server 2013. Ciò è necessario perché la distribuzione dei nuovi client richiede tempo e si desidera consentire agli utenti esistenti con client legacy di poter accedere alle loro chat room il prima possibile.

  - Distribuire nuovi client pur continuando ad assicurarsi che gli utenti con client Group Chat legacy possano accedere alle loro chat room.

