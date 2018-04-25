---
title: Problemi con il test dell'ambiente
TOCTitle: Problemi con il test dell'ambiente
ms:assetid: ff1fe0d3-35b2-41ef-87e7-6a61e9e1d2ca
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205421(v=OCS.15)
ms:contentKeyID: 49302587
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Problemi con il test dell'ambiente

 

_**Ultima modifica dell'argomento:** 2012-09-21_

Best Practices Analyzer consente di verificare che l'ambiente di Lync Server 2013 sia una configurazione supportata. Best Practices Analyzer fa parte dei controlli di Servizi di dominio Active Directory ed esegue le operazioni seguenti:

  - Verifica la preparazione della foresta e dello schema di Servizi di dominio Active Directory.

  - Identifica il numero di siti e domini di Servizi di dominio Active Directory nella distribuzione.

  - Controlla i livelli di foresta e dominio.

  - Controlla la versione del controller di dominio.

  - Identifica il dominio, la configurazione e il contesto di denominazione dello schema.

  - Identifica il numero degli utenti abilitati.

  - Controlla dove sono archiviate le impostazioni globali di Servizi di dominio Active Directory.

  - Controlla i punti di connessione del servizio (SCP, Service Connection Point) per Lync Server.

  - Identifica la versione del database.

## Risoluzione dei problemi con l'ambiente

Se il test dell'ambiente rileva problemi con l'ambiente, questi potrebbero essere causati da problemi relativi alla configurazione di Active Directory o al livello di software in esecuzione in server specifici. Ad esempio, se Best Practices Analyzer identifica nell'ambiente dei controller di dominio in cui è in esecuzione Windows Server 2000, verrà visualizzato un avviso e sarà necessario aggiornare i controller di dominio alla versione supportata di Windows Server.

