---
title: Pubblicare il database delle posizioni
TOCTitle: Pubblicare il database delle posizioni
ms:assetid: dd032b5b-df0e-4017-ac46-e17570c1ab1e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398974(v=OCS.15)
ms:contentKeyID: 49302207
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pubblicare il database delle posizioni

 

_**Ultima modifica dell'argomento:** 2012-10-30_

Le nuove posizioni aggiunte al database delle posizioni non vengono rese disponibili per il client finché non vengono pubblicate.

Per informazioni dettagliate, vedere la documentazione di Lync Server Management Shell relativa al cmdlet seguente:

  - **Publish-CsLisConfiguration**

Se si utilizzano gateway ELIN (Emergency Location Identification Number), è necessario inoltre caricare i numeri ELIN nel database ALI (Automatic Location Identification) del gestore della rete PSTN (Public Switched Telephone Network). Il gestore della rete PSTN può richiedere di utilizzare un formato specifico per i record ELIN. Contattarlo per informazioni dettagliate. È possibile esportare i record dal database del servizio Informazioni percorso e formattarli in base alle esigenze.

## Per pubblicare il database delle posizioni

  - Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

  - Per pubblicare il database delle posizioni, eseguire il cmdlet seguente.
    
        Publish-CsLisConfiguration

