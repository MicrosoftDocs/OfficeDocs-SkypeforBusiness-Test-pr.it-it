---
title: 'Lync Server 2013: Schema del database di Chat persistente'
TOCTitle: Schema del database di Chat persistente
ms:assetid: 58d7d94f-42f5-4c3e-8fe5-901fbe92152e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558653(v=OCS.15)
ms:contentKeyID: 49300617
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Schema del database di Chat persistente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-18_

In questo argomento viene documentato lo schema del database di Chat persistente nel software di comunicazione  Lync Server 2013.

Il database Chat persistente fa riferimento al database corrispondente ai ruoli Back End Server di Lync Server 2013**PersistentChatStore** (corrispondente al database mgc) e **PersistentChatComplianceStore** (corrispondente al database mgccomp). L'obiettivo della pubblicazione di questo schema è di consentire la creazione di query per comprendere meglio come generare rapporti efficaci relativi all'uso della chat, alle chat attive, agli autori di post più attivi e così via.

> [!important]  
> Ci riserviamo il diritto di modificare questo schema. Microsoft non garantisce di poter mantenere la completa compatibilità di questo schema pubblicato con le versioni precedenti.

Tenere presenti queste procedure consigliate:

  - Non sono supportate istruzioni SELECT\* // perché l'elenco di colonne può crescere.

  - Non sono supportate modifiche allo schema generate dall'utente.

  - Non sono supportate operazioni di scrittura

  - Testare le query create con database di dimensioni rappresentative, per assicurarsi che le prestazioni soddisfino le esigenze.

## Argomenti della sezione

  - [Elenco delle tabelle del server Chat persistente in Lync Server 2013](lync-server-2013-list-of-persistent-chat-server-tables.md)

  - [Elenco delle tabelle di conformità del server Chat persistente in Lync Server 2013](lync-server-2013-list-of-persistent-chat-server-compliance-tables.md)

  - [Dettagli sulle tabelle del server Chat persistente in Lync Server 2013](lync-server-2013-persistent-chat-server-table-details.md)

  - [Query del database di Chat persistente di esempio per Lync Server 2013](lync-server-2013-sample-persistent-chat-database-queries.md)

