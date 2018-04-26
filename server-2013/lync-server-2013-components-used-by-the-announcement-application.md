---
title: "Lync Server 2013: Componenti utilizzati dall'applicazione Annuncio"
TOCTitle: Componenti utilizzati dall'applicazione Annuncio
ms:assetid: 7b1a0281-cf31-459d-a734-5f10a129089c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398608(v=OCS.15)
ms:contentKeyID: 49301083
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Componenti utilizzati dall'applicazione Annuncio in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-13_

In Lync Server 2013, l' applicazione Annuncio è un componente dell' applicazione Response Group. Quando si distribuisce VoIP aziendale, l' applicazione Annuncio viene installata automaticamente e attivata insieme all' applicazione Response Group. In questa sezione vengono descritti i componenti che supportano l' applicazione Annuncio.

## Componenti dell'applicazione Annuncio

I componenti di Lync Server seguenti supportano l' applicazione Annuncio:

  - **Servizio applicazione**   L' Servizio applicazione fornisce una piattaforma per la distribuzione, l'hosting e la gestione delle applicazioni per comunicazioni unificate. L' Servizio applicazione viene installata automaticamente in ogni Front End Server in un pool Front End e in ogni server Standard Edition.

  - **applicazione Response Group**   L' applicazione Response Group è una delle applicazioni per comunicazioni unificate ospitate da Servizio applicazione. Quando per la distribuzione di un annuncio è configurato un intervallo di numeri non assegnati, l' applicazione Response Group è necessaria per instradare le chiamate al numero di telefono. L' applicazione Response Group non è necessaria se tutti gli intervalli sono configurati per l'instadamento alla messaggistica unificata di Exchange.

  - **File audio**   Per gli annunci vengono utilizzati file audio.

  - **Archivio file**   L' applicazione Annuncio utilizza l'archivio file per l'archiviazione dei file audio.

  - **Pannello di controllo di Lync Server**   È possibile utilizzare il Pannello di controllo di Lync Server per configurare la tabella dei numeri non assegnati.

  - **Lync Server Management Shell**   È possibile utilizzare i cmdlet di Lync Server Management Shell per configurare le impostazioni dell'applicazione Annuncio e la tabella dei numeri non assegnati.

