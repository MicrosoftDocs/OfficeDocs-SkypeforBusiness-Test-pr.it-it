---
title: Componenti utilizzati dalla risposta alle chiamate di gruppo
TOCTitle: Componenti utilizzati dalla risposta alle chiamate di gruppo
ms:assetid: 45db2f23-d486-4b20-a8cf-7b48a1f9fd3a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945625(v=OCS.15)
ms:contentKeyID: 52062139
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Componenti utilizzati dalla risposta alle chiamate di gruppo

 

_**Ultima modifica dell'argomento:** 2013-01-30_

La funzionalità di risposta alle chiamate di gruppo viene distribuita automaticamente insieme a VoIP aziendale e all'applicazione Parcheggio di chiamata. Per abilitare la risposta alle chiamate di gruppo, è necessario configurare la tabella di codici orbit del Parcheggio di chiamata con intervalli separati di numeri designati come numeri per la risposta alle chiamate di gruppo. I componenti seguenti di Lync Server supportano la funzionalità di risposta alle chiamate di gruppo:

  - **Servizio applicazione**   Il Servizio applicazione offre una piattaforma per la distribuzione, l'hosting e la gestione delle applicazioni per le comunicazioni unificate, come l'applicazione Parcheggio di chiamata. Il Servizio applicazione viene installato automaticamente in ogni Front End Server di un pool Front End e in ogni server Standard Edition.

  - **applicazione Parcheggio di chiamata**   L'applicazione Parcheggio di chiamata è una delle applicazioni per le comunicazioni unificate ospitate dal Servizio applicazione. La funzionalità di risposta alle chiamate di gruppo si basa sull'applicazione Parcheggio di chiamata.

  - **Lync Server Management Shell**   Si utilizza Lync Server Management Shell per gestire i gruppi per la risposta alle chiamate di gruppo.

  - **Strumento del Resource Kit SEFAUtil**   Si utilizza l'utilità SEFAUtil (Secondary Extension Feature Activation Utility) per assegnare gli utenti a un gruppo per la risposta alle chiamate di gruppo e per abilitare o disabilitare la possibilità di rispondere alle chiamate per gli utenti.

