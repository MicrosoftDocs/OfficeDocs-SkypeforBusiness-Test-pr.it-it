---
title: "Lync Server 2013: (Facolt.) Verifica. distribuzione del parcheggio"
TOCTitle: (Facoltativo) Verificare la distribuzione del parcheggio di chiamata
ms:assetid: fcfe0962-1a9c-4cbd-847c-fed40e3b1480
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413076(v=OCS.15)
ms:contentKeyID: 49302572
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# (Facoltativo) Verificare la distribuzione del parcheggio di chiamata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-11_

Dopo aver installato e configurato Parcheggio di chiamata, è necessario verificare la configurazione per accertarsi che il parcheggio e il recupero delle chiamate funzionino come previsto. Effettuare almeno le verifiche seguenti:

  - Chiamare un utente con la funzionalità Parcheggio di chiamata abilitata e chiedergli di parcheggiare la chiamata.
    

    > [!NOTE]
    > Se si abilita la funzionalità Parcheggio di chiamata nel criterio vocale immediatamente prima di eseguire questo test, l'utente che parcheggia la chiamata deve disconnettersi da Lync Server e accedere nuovamente per visualizzare l'opzione Parcheggio di chiamata nell'elenco di trasferimento delle chiamate.



  - Comporre il numero di orbit per recuperare la chiamata.

  - Parcheggiare un'altra chiamata, attendere il timeout della chiamata parcheggiata e non rispondere alla richiamata. Verificare che dopo il timeout la chiamata venga correttamente instradata alla destinazione di fallback specificata per **OnTimeoutURI** .

