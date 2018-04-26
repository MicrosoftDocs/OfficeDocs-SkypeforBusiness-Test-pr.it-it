---
title: 'Lync Server 2013: Componenti utilizzati dal parcheggio di chiamata'
TOCTitle: Componenti utilizzati dal parcheggio di chiamata
ms:assetid: c7ffbee3-0ce1-48c0-bb56-af098b41d6d6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398824(v=OCS.15)
ms:contentKeyID: 49301922
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Componenti utilizzati dal parcheggio di chiamata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-13_

L' applicazione Parcheggio di chiamata viene installata automaticamente quando si distribuisce VoIP aziendale. Per abilitare Parcheggio di chiamata, configurare i criteri vocali. I componenti di Lync Server 2013 seguenti supportano l' applicazione Parcheggio di chiamata:

  - **Servizio applicazione**   Il Servizio applicazione offre una piattaforma per la distribuzione, l'hosting e la gestione delle applicazioni di comunicazione unificate, come l' applicazione Parcheggio di chiamata. Il Servizio applicazione viene installato automaticamente in ogni Front End Server di un pool Front End e in ogni server Standard Edition.

  - **applicazione Parcheggio di chiamata**   L' applicazione Parcheggio di chiamata è una delle applicazioni di comunicazione unificate ospitate dal Servizio applicazione. Viene inclusa automaticamente quando si distribuisce VoIP aziendale. Parcheggio di chiamata parcheggia e recupera le chiamate e gestisce i codici orbit di parcheggio di chiamata.

  - **File per la musica di attesa**   Se la musica è abilitata, il file musicale viene riprodotto mentre una chiamata è parcheggiata. Durante l'installazione dell' applicazione Parcheggio di chiamata viene incluso un file musicale predefinito.

  - **Archivio file**   L' applicazione Parcheggio di chiamata utilizza l'archivio file per conservare i file audio personalizzati.

  - **Pannello di controllo di Lync Server**   È possibile utilizzare il Pannello di controllo di Lync Server per configurare la tabella di codici orbit di parcheggio di chiamata e per abilitare Parcheggio di chiamata per gli utenti.

  - **Lync Server Management Shell**   È possibile eseguire tutte le operazioni di configurazione dell' applicazione Parcheggio di chiamata utilizzando i cmdlet della Lync Server Management Shell.

